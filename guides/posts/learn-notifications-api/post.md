---
title: Interactive Guide To Notifications API
description: If a web app needs to send notifications to the user at the system level, the Notifications API is used. The API uses the browser to display notifications outside the page.
publishedDate: 2022-01-20T19:10:30.765Z
lastModifiedDate: 2022-01-20T19:10:30.765Z
authors:
    - ahmadBilal
categories:
    - interactive
tags:
    - notifications-api
coverImage: ''
draft: false
---

<Lead>

In Web Applications, you may need to display notifications to the user which do not requier the user to be active on your page. The Web Notifications API allows developers to implement this feature.

</Lead>

## Notifications API

The Web Notifications API allows web apps to send system-level notifications to the user. These notifications are shown outside the browsing context viewport, and are visible even if the user has moved to another page or app.

## Browser Support

It is supported by almost all modern browsers apart from Safari on IOS. Old browsers like Internet Explorer also lack the support for it.

## Availability

You can quickly check for browser support using the following snippet:

```js
if ('Notification' in window) {
	// Do something with notifications here
}
```

## Usage

Many web applications utilize this API to send notifications, including Slack, Facebook and other chat applications. This API designed to be cross platform and compatible with existing notification systems.

To display a notification, you need to do two things:

1. Ask the user for permission to display notifications.
2. Create and display the notification.

### Get Permission

The API provides the `Notification.requestPermission()` method which does what it says; asks the user for permission. Once the permission is granted, the choice is saved for atleast a whole session.

This method should be trigerred explicitly as a result of some user action such as a button click. Here is how you can use the method in your React application.

```js
const showNotification = () => {
	Notification.requestPermission().then(result => {
		if (result === 'granted') {
			// Show the notification here
		}
	});
};

// Inside your component
<Button
	onClick={() => {
		showNotification();
	}}
>
	Show Notification
</Button>;
```

The code above will spawn a dialog box asking the user to allow notifications.

### Show Notifications

Once the user grants permission, you can show the notifications using the `Notification()` constructor. Simply create a new `Notification` instance, and specify its parameters like title, body, icon, etc. Let's add it to our function.

```js
const getPermission = () => {
	Notification.requestPermission().then(result => {
		if (result === 'granted') {
			new Notification('Title', {
				body: 'This is an example notification.'
			});
		}
	});
};
```

Click the **Show Notification** button below to try it yourself. Make sure your browser is allowed to show notifications.

<LearnNotificationsAPI />

It will look like this:

![Notification generated by the API](https://raw.githubusercontent.com/RapidAPI/DevRel-Stack-Data/production/guides/posts/learn-notifications-api/images/notification.png)

## Wrap Up

This guide was a brief tour of the Notification API, and we hope that now you can use it in your awesome projects.