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

This repository is a comprehensive guide for implementing custom email unsubscribe features using OneSignal's API. Aimed at developers, it provides two examples to demonstrate how you can provide users with a seamless and secure unsubscribe process.

1. **Custom Unsubscribe Form**: This example uses a simple HTML form with a single "Unsubscribe" button. The form's `action` and `method` attributes are dynamically set using JavaScript, which constructs the appropriate OneSignal API endpoint based on URL query parameters.

2. **Custom Unsubscribe Button**: Unlike the form-based approach, this example triggers the unsubscribe action directly via a button click. JavaScript adds a click event listener to the button, making a POST request to the OneSignal API endpoint for unsubscribing.

Both examples are designed to be easily integrated into your existing projects and come with detailed explanations and code snippets to get you up and running quickly.

## Usage

1. Clone this repo, `git clone https://github.com/OneSignalDevelopers/email-unsubscribe-pages-sample`
2. Navigate to the repo, `cd ~/path-of-repo`
3. Start a simple server, `npx http-server .`
4. Send email (see [this guide](#guide_explaining_how_to_build_email_template) to learn how setup email with custom unsubscribe link)
5. Click unsubscribe link


The unsubscribe button will unsubscribe you when clicked.

## Custom Unsubscribe Demo

The [button demo](./unsubscribe-button.html) illustrates implementing a custom email unsubscribe feature using a button and OneSignal's API. Below are the key components:

<img width="1176" alt="unsubscribe-button" src="https://github.com/OneSignalDevelopers/email-unsubscribe-pages-sample/assets/1715082/5589cbb9-17a1-44f4-b13c-38af83b92d05">

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
const onClick = (event) =>
  fetch(unsubscribeURL(window.location.href), {
    method: "POST",
  })
    .then((res) => {
        // ...response handling
    })

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

The URL structure is of the form

`<Base URL>?app_id=<App ID>&notification_id=<Notification ID>&token=<JWT>`

- **Base URL**: `https://examplesite.com/unsubscription-form.html` - This is the location of your custom unsubscribe page.
- **Query Parameters**:
  - `app_id`: The ID of your OneSignal application.
  - `notification_id`: The ID of the specific notification.
  - `token`: A security token for the unsubscribe action.

### JavaScript Logic

The JavaScript code constructs the URL OneSignal needs to unsubscribe the user from email.

```js
const unsubscribeURL = (href) => {
  const unsubscribeURL = new URL(href)
  const appID = unsubscribeURL.searchParams.get("app_id")
  const notificationID =
    unsubscribeURL.searchParams.get("notification_id")
  const unsubscribeToken = unsubscribeURL.searchParams.get("token")
  return `https://api.onesignal.com/apps/${appID}/notifications/${notificationID}/unsubscribe?token=${unsubscribeToken}`
}
```

### How It Works

1. **Email Link**: The user receives an email containing the unsubscribe link.
2. **Click Action**: When the user clicks the link, they are directed to your custom unsubscribe page, and the query parameters `app_id`, `notification_id`, `token` are passed along.
3. **Page Load**: Upon loading, the `DOMContentLoaded` event triggers the JavaScript code.
4. **URL Parsing**: The function `unsubscribeURL` extracts the query parameters to construct the OneSignal API endpoint for unsubscribing.
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
