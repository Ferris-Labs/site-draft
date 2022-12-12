## IFTTT (If This Than That) Notifications
* **Source**: https://ifttt.com/
* **Icon Support**: No
* **Message Format**: Text
* **Message Limit**: 32768 Characters per message

### Account Setup
Creating a IFTTT account is easy.  Visit there website and create your free account.

Once you're hooked up, you'll want to visit [this URL](https://ifttt.com/services/maker_webhooks/settings) on Webhooks.  This will be the gateway Apprise will use to signal any Applets you create.  When you visit this page it will give you your API key in the form of a URL. 

The URL might something like this:
```https://maker.ifttt.com/use/b1lUk7b9LpGakJARKBwRIZ```

This effectively equates to:
```https://maker.ifttt.com/use/{WebhookID}```

In the above example the **WebhookID** is ```b1lUk7b9LpGakJARKBwRIZ```. You will need this value!

**Note:** Apprise supports this URL _as-is_ (_as of v0.7.7_); you no longer need to parse the URL any further.  However there is slightly less overhead (internally) if you do.

### Syntax
Valid syntaxes are as follows:
* `https://maker.ifttt.com/use/{WebhookID}`
* **ifttt**://**{WebhookID}**@**{Event}**/
* **ifttt**://**{WebhookID}**@**{Event1}**/**{Event2}**/**{EventN}**/
* **ifttt**://**{WebhookID}**@**{Event}**/**?+NewArg=ArgValue**
* **ifttt**://**{WebhookID}**@**{Event}**/**?-value3**

By default these are the the assign default template entries:
* **{value1}** : The **title** will go here
* **{value2}** : The **body** will go here
* **{value3}** : The **message type** will go here (it will read either _info_, _warning_, _critical_, or _success_)

### Parameter Breakdown
| Variable    | Required | Description
| ----------- | -------- | -----------
| WebhookID   | Yes      | Your webhooks API Key you got from [the settings area of the webhooks service itself](https://ifttt.com/services/maker_webhooks)
| Event       | Yes      | This is the **Event Name** you assigned to the Applet you created. You must at least pass in one of these. This is the event plan on triggering through the webhook.
| +Arg=Val    | No       | Add an additional **{Arg}** into the payload and assign it the value of **{Val}**. It's very important that your argument starts with a plus (**+**) symbol in order to use this option.
| -Arg        | No       | This is useful if you want to eliminate one of the pre-defined arguments discussed below.  You might want to include **?-value1&-value2** to just pass **value3** in the payload. It's very important that your argument starts with a hyphen/minus (**-**) symbol in order to use this option. As mentioned above, your payload will ALWAYS include **value1**, **value2**, and **value3** in it unless you specify otherwise.

#### Examples
Send a IFTTT notification:
```bash
# Assuming our {WebhookID} is b1lUk7b9LpGakJARKBwRIZ
# Assuming our {Event} is sms_message
# Assuming you want {value1} to read "My Title"
# Assuming you want {value2} to read "My Body"
# Assuming you want {value3} to read "info"
apprise -vv -t "My Title" -b "My Value" \
   ifttt:///b1lUk7b9LpGakJARKBwRIZ@sms_message
```

Now I realize not everyone will want to use the default **{valueX}** entries defined.  In fact, you may want to just use apprise to turn on a light switch and set some complete different value like **{switch}** to '_on_'.   Here is how you could accomplish this:
```
# Send {switch} a value of 'on'
# Assuming our {WebhookID} is b1lUk7b9LpGakJARKBwRIZ
# Assuming our {Event} is my_light
# Any argument prefixed with a minus/hyphen (-) eliminates an
# argument from our payload.  Since we know value1, value2, and
# value3 are present in every payload, we eliminate them.
#
# Now we use a plus (+) symbol in front of an argument to tell
# the remote server we want to include a new option called
# switch and set it's value to 'on'
apprise -vv -b "" ifttt:///b1lUk7b9LpGakJARKBwRIZ@my_light/?-value1&-value2&-value3&+switch=on
```

**Thoughts**: The +/- options are relatively new, but it still feels like this plugin could be made even easier to use. If you have any idea's please open a ticket and let me know your ideas!
