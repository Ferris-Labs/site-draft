## Twist Notifications
* **Source**: https://twist.com
* **Icon Support**: No
* **Message Format**: Text
* **Message Limit**: 1000 Characters per Message

[Sign in](https://twist.com/login) or [create an account](https://twist.com/signup) with the [Twist service](https://twist.com) if you don't already have one.

The main thing with the Twist service is you always authenticate with an **{email}** and a **{password}**. Apprise can work with twist just knowing these two values as well.

### Syntax
Valid authentication syntaxes are as follows:
* **twist**://**{password}**:**{email}**
* **twist**://**{email}**/**{password}**

**Note:** If not channel is specified then by default the **#General** channel is messaged.

You can also message one or more channels too:
* **twist**://**{password}**:**{email}**/#**{channel}**
* **twist**://**{email}**/**{password}**/#**{channel}**
* **twist**://**{password}**:**{email}**/#**{channel1}**/#**{channel2}**
* **twist**://**{email}**/**{password}**/#**{channel1}**/#**{channel2}**

Twist always associates your account with a *default team*.  Apprise determines this for you and by default notifies the channels you specify from within it. However, since it is possible to have your login/password associated with more then one **Team**. You can use the colon (:) as a delimiter to explicitly identify which team/channel you wish to message.

* **twist**://**{password}**:**{email}**/#**{team}**:**{channel}**
* **twist**://**{email}**/**{password}**/#**{team}**:**{channel}**

### Parameter Breakdown
| Variable    | Required | Description
| ----------- | -------- | -----------
| email       | Yes      | This is the email address you associated with your Twist account when you signed up.
| password    | Yes      | This is the password you set when you signed up with Twist
| channel     | No       | This is the channel you wish to notify.  If you don't specify one then the *#General* channel will be used by default from within your default team.  You can optionally use a colon (:) placed in front of the channel name to force the message to a specific team (if you are part of more then one).

#### Example
Send a Twist notification to the channel #general associated with our default team.
```bash
# Assume:
#  - our {email} is test@example.com
#  - our {password} is abc123
#  - The {channel} is #general
apprise -vv -t "Test Message Title" -b "Test Message Body" \
   twist://abc123:test@example.com/#general
```
