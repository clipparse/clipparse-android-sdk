# Data handled by the ClipParse Android SDK

Applies to version 1.0.0 and later. Last updated: November 2026.

This page lists what the SDK sends from a device and to whom, so you can fill in Google Play's Data safety form and your own privacy policy. It describes the SDK only: your app's other data practices are yours to declare. You remain responsible for the accuracy of your Data safety form.

ClipParse acts as your processor (service provider) under the [Data Processing Agreement](https://clipparse.com/dpa). It does not sell the data it receives through the SDK, and uses it only to provide the service. The ClipParse [privacy policy](https://clipparse.com/privacy) is the reference for retention periods and for the processors ClipParse uses.

## What the SDK sends

### To the ClipParse API (`api.clipparse.com`)

| Data | Why | Stored by ClipParse |
| --- | --- | --- |
| The post link passed to `extract` | To extract the recipe | Yes, in request logs |
| The post's caption | To extract the recipe | No: processed in memory only |
| Your API key | To authenticate your app | No: the request is recorded against your account, not the key itself |
| The SDK's version and platform (`android`) | Debugging and support | Yes, in request logs |
| Your app's package name | To identify the calling app | Yes, in request logs |

The package name and the SDK version identify your app, not the person using it.

As with any request over the internet, the API's hosting platform records the device's IP address and user agent in its infrastructure logs. ClipParse's application does not read or store them, and they are not used to locate or identify anyone.

Retention periods for request logs and infrastructure logs are in the [privacy policy](https://clipparse.com/privacy).

### To Instagram

For Instagram links, the device requests the public post, at its public address, from Instagram directly. Instagram receives what any visit to a public page sends: the address of the post, the device's IP address and its standard request headers. The SDK adds nothing that identifies the user or your app. The IP address and headers of that request are not sent to ClipParse.

The SDK sets no cookies. If your app installs an app-wide cookie handler, it applies to this request as to any other.

Recipe thumbnails are returned as links. If your app displays one, the image loads from TikTok's or Instagram's servers, under your app's own networking.

## What the SDK does not do

- It collects no device identifiers, no advertising ID and no location.
- It contains no analytics or advertising code, and does not track users.
- It stores nothing on the device.
- It requests one permission, `INTERNET`.
- It sends nothing until your app calls `extract`.

## For the Data safety form

How the SDK's data maps to the form's categories. See [Google Play's guidance](https://support.google.com/googleplay/android-developer/answer/10787469) for the definitions.

| Form question | For the SDK |
| --- | --- |
| Data collected | The post link, typically one the user submits, and the post's caption (both *App activity → Other user-generated content*) |
| Processed ephemerally | The post link: no, it is kept in request logs. The caption: yes, it is processed in memory only |
| Purpose | *App functionality* |
| Data shared with ClipParse | Not sharing: ClipParse processes the data on your behalf, as a service provider |
| Data sent to Instagram | The device requests the public post from Instagram directly. Whether this counts as sharing depends on how the link reaches your app: see the user-initiated action exemption in Google's guidance |
| Encrypted in transit | Yes, every request uses HTTPS |

Google Play counts data as collected once it leaves the device, including data that is only processed in memory, which is why the caption is listed. The API key, the package name and the SDK version are not data about your users, so they are not.

Whether the collection is required or optional, and how users can request deletion, depend on your app. Deletion requests for data that reached ClipParse through your app are handled as the privacy policy describes.

Questions: contact@clipparse.com
