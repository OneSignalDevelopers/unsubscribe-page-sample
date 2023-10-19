<div align="center">
  <a href="https://documentation.onesignal.com/docs/onboarding-with-onesignal" target="_blank">Quickstart</a>
  <span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
  <a href="https://onesignal.com/" target="_blank">Website</a>
  <span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
  <a href="https://documentation.onesignal.com/docs" target="_blank">Docs</a>
  <span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
  <a href="https://github.com/OneSignalDevelopers" target="_blank">Examples</a>
  <br />
 <br />
</div>

![OneSignal](https://github.com/OneSignalDevelopers/.github/blob/main/assets/onesignal-banner.png?raw=true)

# Custom Email Unsubscribe Pages Sample

This repository is a comprehensive guide for implementing custom email unsubscribe features using OneSignal's API. Aimed at developers, it demonstrates how you can provide users with a seamless and secure unsubscribe process. The example is designed to be easily integrated into your existing projects and comes with detailed explanations and code snippets to get you up and running quickly.

## Usage

1. Clone this repo, `git clone https://github.com/OneSignalDevelopers/custom-email-unsubscribe-page-sample`
2. Navigate to the repo, `cd ~/path-of-repo`
3. Start a simple server, `npx http-server .`
4. Send email (see [this guide](#guide_explaining_how_to_build_email_template) to learn how setup email with custom unsubscribe link)
5. Click the unsubscribe link

<img width="1014" alt="Unsubscribe button" src="https://github.com/OneSignalDevelopers/custom-email-unsubscribe-page-sample/assets/1715082/bdc12473-254d-48c3-bcc9-26a112ff66b1">


The unsubscribe button will unsubscribe you when clicked.

## Custom Unsubscribe Demo

This [demo](./unsubscribe.html) demonstrates implementing OneSignal's **Custom Email Unsubscribe Page** feature using a button and OneSignal's API. Below are the key components:

### HTML Structure

The HTML layout consists of a single "Unsubscribe" button. Unlike the previous example that used a form, this example triggers the unsubscribe action directly via a button click.

```html
<body>
  <h1>Custom Unsubscribe Button</h1>
  <button type="button">
    Unsubscribe
  </button>
</body>
```

### JavaScript Logic

The JavaScript code adds a click event listener to the button to trigger the unsubscribe request.

```javascript
const onClick = (event) => {
  const { unsubscribeURL } = unsubscribeURL(window.location.href)
  fetch(unsubscribeURL, {
    method: "POST",
  }).then((res) => {
    // ... request handling
  })
}

document.addEventListener("DOMContentLoaded", () => {
  const buttonEl = document.getElementById("unsubscribe_button");
  buttonEl.addEventListener("click", onClick);
});
```

### How It Works

1. Upon page load, the `DOMContentLoaded` event is triggered.
2. The JavaScript function `unsubscribeURL` constructs the OneSignal API endpoint to unsubscribe the user from email.
3. A click event listener is added to the button. When clicked, it makes a POST request to the API endpoint.

By incorporating this code, you can create a custom unsubscribe feature directly interacting with OneSignal's API through a button click.

## URL Structure

The URL structure for the API endpoint is of the form

`<Base URL>?app_id=<App ID>&notification_id=<Notification ID>&email=<User Email>&language=<User Language>&token=<JWT>`

- **Base URL**: `https://examplesite.com/unsubscribe` - This is the location of your custom unsubscribe page.
- **Query Parameters**:
  - `app_id`: The ID of your OneSignal application.
  - `notification_id`: The ID of the specific notification.
  - `token`: A security token for the unsubscribe action.
  - `email`: The email address tied to the subscription
  - `language`: The user's language preference

### JavaScript Logic

The JavaScript code constructs the URL OneSignal needs to unsubscribe the user from the email.

```js
const unsubscribeURL = (href) => {
  const unsubscribeURL = new URL(href)
  const appID = unsubscribeURL.searchParams.get("app_id")
  const notificationID =
    unsubscribeURL.searchParams.get("notification_id")
  const unsubscribeToken = unsubscribeURL.searchParams.get("token")
  const language = url.searchParams.get("language")
  const email = url.searchParams.get("email")
  return {
    unsubscribeURL: `https://api.onesignal.com/apps/${appID}/notifications/${notificationID}/unsubscribe?token=${unsubscribeToken}`,
    meta: { language, email },
  }
}
```

### How It Works

1. **Email Link**: The user receives an email containing the unsubscribe link.
2. **Click Action**: When the user clicks the link, they are directed to your custom unsubscribe page, and the query parameters `app_id`, `notification_id`, `token` are passed along.
3. **Page Load**: Upon loading, the `DOMContentLoaded` event triggers the JavaScript code.
4. **URL Parsing**: The function `unsubscribeURL` extracts the query parameters to construct the OneSignal API endpoint for unsubscribing and its supporting metadata.
5. **Button Configuration**:
   - The form's action attribute is set to this API endpoint in the form example.
   - In the button example, a click event listener is added to the button to make a POST request to this API endpoint.

## ❤️ Developer Community

For additional resources, please join the [OneSignal Developer Community](https://onesignal.com/onesignal-developers).

Get in touch with us or learn more about OneSignal through the channels below.

* [Follow us on Twitter](https://twitter.com/onesignaldevs) to never miss any updates from the OneSignal team, ecosystem & community
* [Join us on Discord](https://discord.gg/EP7gf6Uz7G) to be a part of the OneSignal Developers community, showcase your work and connect with other OneSignal developers
* [Read the OneSignal Blog](https://onesignal.com/blog/) for the latest announcements, tutorials, in-depth articles & more.
* [Subscribe to us on YouTube](https://www.youtube.com/channel/UCe63d5EDQsSkOov-bIE_8Aw/featured) for walkthroughs, courses, talks, workshops & more.
* [Follow us on Twitch](https://www.twitch.tv/onesignaldevelopers) for live streams, office hours, support & more.

**Show your support** and give a ⭐️ if this project helped you :-)
