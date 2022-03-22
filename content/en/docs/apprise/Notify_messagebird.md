## MessageBird
* **Source**: https://messagebird.com
* **Icon Support**: No
* **Message Format**: Text
* **Message Limit**: 160 Characters per message

### Account Setup
To use MessageBird, you will need to acquire your _API Key_. This is accessible via the [MessageBird Dashboard](https://dashboard.messagebird.com/en/user/index).

### Syntax
Valid syntaxes are as follows:
* **msgbird**://**{ApiKey}**/**{FromPhoneNo}**
* **msgbird**://**{ApiKey}**/**{FromPhoneNo}**/**{ToPhoneNo}**
* **msgbird**://**{ApiKey}**/**{FromPhoneNo}**/**{ToPhoneNo1}**/**{ToPhoneNo2}**/**{ToPhoneNoN}**

### Parameter Breakdown
| Variable        | Required | Description
| --------------- | -------- | -----------
| ApiKey         | Yes      | The _API Key_ associated with your MessageBird account.  This is available to you via the [MessageBird Dashboard](https://dashboard.messagebird.com/en/user/index).
| FromPhoneNo     | Yes      | A from phone number MUST include the country codes dialling prefix as well when placed.  This field is also very friendly and supports brackets, spaces and hyphens in the event you want to format the number in an easy to read fashion. This MUST be the the number you registered with your *MessageBird* account.
| ToPhoneNo     | No      | A to phone number MUST include the country codes dialling prefix as well when placed.  This field is also very friendly and supports brackets, spaces and hyphens in the event you want to format the number in an easy to read fashion. If no *ToPhoneNo* is specified, then the *FromPhoneNo* is notified instead.

#### Example
Send a MessageBird Notification as an SMS:
```bash
# Assuming our {APIKey} is gank339l7jk3cjaE
# Assuming our {FromPhoneNo} - is in the US somewhere making our country code +1
#                            - identifies as 1-123-555-1223
apprise -vv -t "Test Message Title" -b "Test Message Body" \
   msgbird://gank339l7jk3cjaE/11235551223

# the following would also have worked (spaces, brackets,
# dashes are accepted in a phone no field):
apprise -vv -t "Test Message Title" -b "Test Message Body" \
   msgbird://gank339l7jk3cjaE/1-(123) 555-1223
```