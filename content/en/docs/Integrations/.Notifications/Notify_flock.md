## Flock Notifications
* **Source**: https://flock.com/
* **Icon Support**: Yes
* **Message Format**: Text
* **Message Limit**: 32768 Characters per message

### Account Setup
Flock has a lot of similarities to Slack.  Flock notifications require an *incoming-webhook* or a *app/bot* it can connect to. 

## Incoming Webhook

You can generate an Incoming webhook from [here](https://dev.flock.com/webhooks](https://dev.flock.com/webhooks). Just follow the wizard to pre-determine the channel(s) you want your message to broadcast to. When you've completed this process you will receive a URL that looks something like this:
```https://api.flock.com/hooks/sendMessage/134b8gh0-eba0-4fa9-ab9c-257ced0e8221```

This effectively equates to:
```https://api.flock.com/hooks/sendMessage/{token}```

**Note:** Apprise supports this URL _as-is_ (_as of v0.7.7_); you no longer need to parse the URL any further.  However there is slightly less overhead (internally) if you do.

In this example the token is `134b8gh0-eba0-4fa9-ab9c-257ced0e8221`

## Bot
Bots are a bit more difficult and presume that you followed their instructions on setting on up [your own app](https://docs.flock.com/display/flockos/Creating+an+App#CreatinganApp-HowdoIcreateaFlockOSapp?).  Just like a webhook, you'll get your own **{token}** provided to you that allows you to message people and channels directly.

### Syntax
Valid syntaxes with an *incoming webhook* are:
* `https://api.flock.com/hooks/sendMessage/{token}`
* flock://**{token}**/
* flock://**{botname}**@**{token}**/

Valid syntaxes with an *application / bot* are:
**Note:** the **userid** and **channelid** belong to the actual encoded id and not the public displayed value.  For instance; if you have a channel called #general, it will have an encoded id associated with it that might look something like **g:abcd1234defg**. Users are identified in a similar fashion but are prefixed with **u:** instead of **g:**. These are the values you must specify here:
* flock://**{token}**/**u:userid**
* flock://**{botname}**@**{token}**/**u:{user}**
* flock://**{botname}**@**{token}**/**u:{user1}**/**u:{user2}**/**u:{userN}**/
* flock://**{botname}**@**{token}**/**g:{channel}**
* flock://**{token}**/**g:{channel}**
* flock://**{botname}**@**{token}**/**g:{channel1}**/**g:{channel2}**/**g:{channelN}**/
* flock://**{botname}**@**{token}**/**g:{channel}**/**u:{user}**/


### Parameter Breakdown
| Variable    | Required | Description
| ----------- | -------- | -----------
| token      | Yes      | The first part of 3 tokens provided to you after creating a *incoming-webhook* and or an *application/bot*
| channel     | No       | Channels must be prefixed with a hash tag **#** or **g:**.  They must represent the encoded id of the channel name (not the human readable reference) You can specify as many channels as you want by delimiting each of them by a forward slash (/) in the url.
| user     | No          | Users must be prefixed with an at symbol **@** or **u:**! They must represent the encoded id of the user name (not the human readable reference) You can specify as many users as you want by delimiting each of them by a forward slash (/) in the url.
| botname     | No       | Identify the name of the bot that should issue the message.  If one isn't specified then the default is to just use your account (associated with the *incoming-webhook*).
| image       | No       | Associate an image with the message. By default this is enabled.

#### Example
Send a flock notification to our channel #nuxref (which is identified as `g:abcd1234efgh`):
```bash
# Assuming our {token} is 134b8gh0-eba0-4fa9-ab9c-257ced0e8221
# our channel nuxref is represented as g:abcd1234efgh
apprise -vv -t "Test Message Title" -b "Test Message Body" \
   flock:///134b8gh0-eba0-4fa9-ab9c-257ced0e8221/g:abcd1234efgh
```
