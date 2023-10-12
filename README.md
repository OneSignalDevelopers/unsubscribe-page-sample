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
4. Navigate to one of the two demos

<img width="1176" alt="Screenshot 2023-10-12 at 11 26 56 AM" src="https://github.com/OneSignalDevelopers/email-unsubscribe-pages-sample/assets/1715082/f6c0e9e5-6364-46ad-8673-02e3aeceeb6a">


## Custom Unsubscribe Form Demo

The [Unsubscribe Form demo](./unsubscribe-form.html) showcases implementing a custom email unsubscribe feature using OneSignal's API. The HTML and JavaScript code below demonstrates the essential components:

### HTML Structure

The HTML is a simple form with a single "Unsubscribe" button. The form's `action` and `method` attributes will be dynamically set using JavaScript.

```html
<body>
  <div class="header">
    <h1>Custom Unsubscribe Form</h1>
  </div>
  <div class="content">
    <form id="onesignal_custom_unsubscribe_form">
      <button type="submit">Unsubscribe</button>
    </form>
  </div>
</body>
```

### JavaScript Logic

The JavaScript code performs the following tasks:

1. **URL Parsing**: Extracts `app_id`, `notification_id`, and `token` from the URL's query parameters.
2. **Form Configuration**: Dynamically sets the form's `action` and `method` attributes.

```javascript
document.addEventListener("DOMContentLoaded", () => {
  const formEl = document.getElementById("onesignal_custom_unsubscribe_form");
  formEl.setAttribute("action", unsubscribeURL(window.location.href));
  formEl.setAttribute("method", "post");
});
```

### How It Works

1. When the page loads, the `DOMContentLoaded` event triggers.
2. The JavaScript function `unsubscribeURL` parses the current URL to construct the OneSignal API endpoint for unsubscribing.
3. The form's `action` attribute is then set to this API endpoint, and the `method` is set to "post".

Integrating this code into your project enables you to create a custom unsubscribe feature that leverages OneSignal's API for email management.

## Custom Unsubscribe Button Demo

The [Unsubscribe Button demo](./unsubscribe-button.html) illustrates implementing a custom email unsubscribe feature using a button and OneSignal's API. Below are the key components:

### HTML Structure

The HTML layout consists of a single "Unsubscribe" button. Unlike the previous example that used a form, this example triggers the unsubscribe action directly via a button click.

```html
<body>
  <div class="header">
    <h1>Custom Unsubscribe Button</h1>
  </div>
  <div class="content">
    <button
      id="onesignal_custom_unsubscribe_btn"
      type="button"
      class="unsubscribe-button"
    >
      Unsubscribe
    </button>
  </div>
</body>
```

### JavaScript Logic

The JavaScript code performs several tasks:

1. **URL Parsing**: Extracts `app_id`, `notification_id`, and `token` from the URL's query parameters.
2. **Button Event Handling**: Adds a click event listener to the button to trigger the unsubscribe action.

```javascript
const onClick = (event) =>
    fetch(unsubscribeURL(window.location.href), {
      method: "POST",
    })
      .then((res) => {
        switch (res.status) {
          case 200:
            return console.log("ACK Unsubscription Reqeuest")
          case 400:
            return console.wann("Handle client request error")
          case 500:
            return console.warn("Fatal server error")
        }
      })
      .catch((error) => console.error("Fatal error occurred", error.message))

document.addEventListener("DOMContentLoaded", () => {
const buttonEl = document.getElementById("onesignal_custom_unsubscribe_btn");
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
    try {
      const unsubscribeURL = new URL(href)
      const appID = unsubscribeURL.searchParams.get("app_id")
      const notificationID =
        unsubscribeURL.searchParams.get("notification_id")
      const unsubscribeToken = unsubscribeURL.searchParams.get("token")
      return `https://api.onesignal.com/apps/${appID}/notifications/${notificationID}/unsubscribe?token=${unsubscribeToken}`
    } catch (error) {
      console.error(`Failed to parse '${href}'`, error.message)
      return null
    }
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
