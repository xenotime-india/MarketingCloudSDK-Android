---
layout: page
title: "Customize Notification Handling"
subtitle: "How to Customize Notification Handling"
category: notifications
date: 2018-09-24 12:00:00
order: 1
---
The SDK allows customizations of notifications via the [NotificationCustomizationOptions]({{ site.baseurl }}/javadocs/6.0/reference/com/salesforce/marketingcloud/notifications/NotificationCustomizationOptions.html) class.  The example shown in the [Initialize the SDK]({{ site.baseurl}}/sdk-implementation/implement-sdk-google.html#3--initialize-the-sdk) portion of the documentation requires only that the `Small Icon Resource ID` be provided to the SDK.  This is the minimum configuration for showing notifications with the Marketing Cloud Mobile Push SDK.  See [Google's documentation regarding Status Bar Icons](https://developer.android.com/guide/practices/ui_guidelines/icon_design_status_bar).

You can customize notifications further by providing a Launch Intent Provider and/or instructing the SDK what action to take when a notification is tapped.  See the [Simplified Customization](#simplified-customization) section below.  You may also take complete control of the notification.  See the [Full Control Customization](#full-control-customization) section at the end of this page.

The [NotificationMessage]({{ site.baseurl}}/javadocs/6.0/reference/com/salesforce/marketingcloud/notifications/NotificationMessage.html) class can be leveraged to facilitate customizations like "Deep Linking" or handling Custom Keys.

### Simplified Customization ###
[NotificationCustomizationOptions]({{ site.baseurl }}/javadocs/6.0/reference/com/salesforce/marketingcloud/notifications/NotificationCustomizationOptions.html) can be created with a [NotificationChannelIdProvider]({{ site.baseurl }}/javadocs/6.0/reference/com/salesforce/marketingcloud/notifications/NotificationManager.NotificationChannelIdProvider.html) to customize the channel for a [NotificationMessage]({{ site.baseurl }}/javadocs/6.0/reference/com/salesforce/marketingcloud/notifications/NotificationMessage.html) and a [NotificationLaunchIntentProvider]({{ site.baseurl }}/javadocs/6.0/reference/com/salesforce/marketingcloud/notifications/NotificationManager.NotificationLaunchIntentProvider.html) to customize the action that will be taken when a [NotificationMessage]({{ site.baseurl }}/javadocs/6.0/reference/com/salesforce/marketingcloud/notifications/NotificationMessage.html) is tapped in addition to your application's Notification Icon.

<script src="https://gist.github.com/sfmc-mobilepushsdk/d3a632e2601bc482804e710158c15bc2.js"></script>

---

### Full Control Customization ###

When providing a builder to the [NotificationCustomizationOptions]({{ site.baseurl }}/javadocs/6.0/reference/com/salesforce/marketingcloud/notifications/NotificationCustomizationOptions.html) you will be responsible for all aspects of the notification's display properties and tap actions.  This includes Notification Channel creation, Launch Intent action, etc.  You can access the [NotificationCompat.Builder]({{ site.baseurl }}/javadocs/6.0/reference/com/salesforce/marketingcloud/notifications/NotificationManager.html#getDefaultNotificationBuilder(android.content.Context,%20com.salesforce.marketingcloud.notifications.NotificationMessage,%20java.lang.String,%20int)) that would have been used by the SDK and leverage that as a baseline to modify.  You may also have the SDK [create a default NotificationChannel]({{ site.baseurl }}/javadocs/6.0/reference/com/salesforce/marketingcloud/notifications/NotificationManager.html#createDefaultNotificationChannel(android.content.Context)) for your application.

> NOTE: You must wrap your `PendingIntent` in the SDK's analytics helper method [NotificationManager.redirectForAnalytics()]({{ site.baseurl }}/javadocs/{{ site.currentMajorMinor }}/reference/com/salesforce/marketingcloud/notifications/NotificationManager.html#redirectIntentForAnalytics(android.content.Context,%20android.app.PendingIntent,%20com.salesforce.marketingcloud.notifications.NotificationMessage,%20boolean)) if you wish to have the Marketing Cloud collect notification open analytics for your notifications.

<script src="https://gist.github.com/sfmc-mobilepushsdk/63df5dd27ce472bc76213b3cfe7b03d6.js"></script>