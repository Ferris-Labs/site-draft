## Telegram Notifications
* **Source**: https://telegram.org/
* **Icon Support**: Yes
* **Attachment Support**: Yes
* **Message Format**: Text
* **Message Limit**: 4096 Characters per message

### Account Setup
Telegram is slightly more complicated then some of the other notification services, so here is quick breakdown of what you need to know and do in order to send Notifications through it using this tool.

At the very start (if you don't have an account already), you will need to connect with a phone.  The site uses your phone number as it's credential to let you into your account. So download and install the phone app first via [Android](https://telegram.org/dl/android) or [Apple](https://telegram.org/dl/ios).

Once you're set up, it can be a bit easier to just use their web interface [here](https://telegram.org/dl/webogram) with a PC (especially for development); but this part is up to you.

#### Bot Setup
Telegram notifications require you to [create a bot](https://api.telegram.org). It's only after this is done that you will gain a vital piece of information Apprise needs called the **Token Identifier** (or **bot_token**).

To do this you will have to open a communication (inside Telegram) to the **[BotFather](https://botsfortelegram.com/project/the-bot-father/)**.  He is available to all users signed up to the platform. Once you've got a dialog box open to him:
1. Type: ```/newbot```
2. Answer the questions it asks after doing this (which get the name of it, etc).
3. When you've completed step 2, you will be provided a *bot_token* that looks something like this: ```123456789:alphanumeric_characters```.
4. Type ```/start``` now in the same dialog box to enable and instantiate your brand new bot.

The good news is this process only has to be done once. Once you get your **bot_token**, hold on to it and no longer worry about having to repeat this process again. It's through this bot that Apprise is able to send notifications onto Telegram to different users.

#### Chat ID Conundrum

----
**2021.12.23 Update**: Recently the developers of Telegram have made it easier to acquire this ID using their own built in tool [explained here](https://www.alphr.com/find-chat-id-telegram/).  Thank you `@mattpackwood` for this tip!

----
Behind the scenes, Telegram notifies users by their **{chat_id}** and not their _easy-to-remember_ user name. 
Unfortunately (at this time) Telegram doesn't make it intuitive to get this **{chat_id}** without simple tricks and workarounds that can be found through Googling or just simply talking to their support team.

However, Apprise can make this task a bit easier if the intention is to just private message yourself. If this is the case, simply send a private message to this new bot you just created (above).  That's it!

By doing this, Apprise is able to automatically to detect _your_ **{chat_id}** from the message sent to the bot. Doing this also allows you to greatly simplify the Apprise URL to read:
* **tgram**://**{bot_token}**/

When using the short form of the Telegram/Apprise URL and the bot owner (probably you) is successfully detected, the **{chat_id}** it detected will appear in the logs after the notification is sent.  Ideally you should take this and update your Apprise URL to explicitly reference this in the future.
* **tgram**://**{bot_token}**/**{chat_id}**

**Note**: you can also just go ahead and acquire the **{chat_id}** yourself after first messaging yourself as per the instructions above.  Afterwards, you just need to visit `https://api.telegram.org/bot{bot_token}/getUpdates`.
 *  *Note:* the keyword `bot` must sit in-front of the actual **{bot_token}** that you were given by the BotFather. 
 * The result will contain the message you sent; in addition to this there is a section entitled `chat` with the `id` identified here. This is the **{chat_id}** you can use to directly message using Apprise.

### Syntax
The following syntax is valid:
* **tgram**://**{bot_token}**/
   * **Note**: As already identified above: Apprise is clever enough to determine the chat_id of the bot owner (you) _only if you've sent it at least 1 private message to it_ first.

* **tgram**://**{bot_token}**/**{chat_id}**/
* **tgram**://**{bot_token}**/**{chat_id1}**/**{chat_id2}**/**{chat_id3}**/


If you want to see the icon/image associated with the notification, you can have it come through by adding a **?image=yes** to your URL string like so:
* **tgram**://**{bot_token}**/**?image=Yes**
* **tgram**://**{bot_token}**/**{chat_id}**/**?image=Yes**
* **tgram**://**{bot_token}**/**{chat_id1}**/**{chat_id2}**/**{chat_id3}**/**?image=Yes**

### Parameter Breakdown
| Variable    | Required | Description
| ----------- | -------- | -----------
| bot_token   | Yes      | The token that identifies the bot you created through the *[BotFather](https://botsfortelegram.com/project/the-bot-father/)*
| chat_id     | Yes      | Identify the users you want your bot to deliver your notifications to. You must specify at least 1 *chat_id*. If you do not specify a chat_id, the notification script will attempt to detect the bot owner's (you) chat_id and use that.
| image       | No       | You can optionally append the argument of **?image=Yes** to the end of your URL to have a Telegram message generated before the actual notice which uploads the image associated with it.  Due to the services limitations, Telegram doesn't allow you to post an image inline with a text message. But you can send a message that just contains an image. If this flag is set to true, *apprise* will send an image notification followed by the notice itself.  Since receiving 2 messages for every 1 notice could be annoying to some, this has been made an option that defaults to being disabled.
| format      | No       | The default value of this is _text_.  But if you plan on managing the format yourself, you can optionally set this to _markdown_ or _html_ as well.
| silent      | No       | A `yes/no` flag allowing you to send the notification in a silent fashion. By default this is set to `no`.
| preview     | No       | A `yes/no` flag allowing you to display webpage previews of your post.  By default this is set to `no`.

#### Example
Send a telegram notification to lead2gold:
```bash
# Assuming our {bot_token} is 123456789:abcdefg_hijklmnop
# Assuming the {chat_id} belonging to lead2gold is 12315544
apprise -vv -t "Test Message Title" -b "Test Message Body" \
   tgram://123456789:abcdefg_hijklmnop/12315544/
```