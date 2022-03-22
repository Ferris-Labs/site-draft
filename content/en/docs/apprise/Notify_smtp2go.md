## SMTP2Go Notifications
* **Source**: https://www.smtp2go.com/
* **Icon Support**: No
* **Attachment Support**: Yes
* **Message Format**: HTML
* **Message Limit**: 32768 Characters per message

### Account Setup
You can create an account for free [on their website](https://www.smtp2go.com/).

The next step is to simply generate an **API Key** associated with your account (on your Dashboard) [here](https://app.smtp2go.com/settings/apikeys/)/

### Syntax
Valid syntax is as follows:
* `smtp2go://{user}@{domain}/{apikey}/`
* `smtp2go://{user}@{domain}/{apikey}/{email}`
* `smtp2go://{user}@{domain}/{apikey}/{email1}/{email2}/{emailN}`

You can adjust what the Name associated with the From email is set to as well:
* `smtp2go://{user}@{domain}/{apikey}/?from=Luke%20Skywalker`

### Parameter Breakdown
| Variable    | Required | Description
| ----------- | -------- | -----------
| apikey      | Yes      | The API Key associated with your SMTP2Go account. You can acquire your API key from your dashboard [here](https://app.smtp2go.com/settings/apikeys/).
| domain      | Yes      | The domain associated with the sending email account
| user        | Yes      | The user gets paired with the domain you specify on the URL to make up the **From** email address your recipients receive their email from.
| email       | No       | You can specify as many email addresses as you wish. Each address you identify here will represent the **To**.
| from        | No       | This allows you to identify the name associated with the **From** email address when delivering your email.
| to          | No       | This is an alias to the email variable. You can chain as many (To) emails as you want here separating each with a comma and/or space.
| cc          | No       | Identify users you wish to send as a Carbon Copy
| bcc        | No       | Identify users you wish to send as a Blind Carbon Copy

#### Example
Send a SMTP2Go notification to the email address bill.gates@microsoft.com
```bash
# Assuming the {domain} we set up with our SMTP2Go account is example.com
# Assuming our {apikey} is  api-60F0DD0AB5BA11ABA421F23C91C88EF4
# We already know our To {email} is bill.gates@microsoft.com
# Assuming we want our email to come from noreply@example.com
apprise smtp2go:///noreply@example.com/api-60F0DD0AB5BA11ABA421F23C91C88EF4/bill.gates@microsoft.com
```