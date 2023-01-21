# Guide Template

The format of guide-based articles is content-dependent. Given the type of content, some formats likely work better than others. For a few examples using different formats, see the [Examples](#examples) section below.

You can use the following basic template to get started writing a guide article:

```
# Title of the guide

Include an overview that describes what the purpose of the article is and what a user can expect from the article.

Note that the title of your guide should begin with a verb (for example, "Embed Zoom into a website"). Avoid titles beginning with "How to".

## First item (Heading 2)

Provide information about the first item. Any subheadings should use **Heading 3** format. Subheadings can include things like requirements, prerequisites for the step, documentation, or other information.

### Subheading (Heading 3)

## Second item (Heading 2)

## Third item (Heading 2)
```

## Examples

The following are some examples of guide articles and different formats based on content:

### Extend and OAuth access token's expiration

```
# Extend an OAuth access token's expiration

An OAuth access token's one hour expiration cannot be extended. You can, however, refresh the token so to keep an active OAuth access token.

## Refresh an OAuth access token

Once you have an active [OAuth access and refresh token](https://marketplace.zoom.us/docs/guides/auth/oauth#getting-access-token), make a POST request to the `https://zoom.us/oauth/token` URL with the following values:

### Query parameters

| Parameter | Value |
| --------------- | ----- |
| `grant_type` | `refresh_token` |
| `refresh_token` | Your OAuth refresh token. |

### Authorization header

| Header | Value | Example |
| -------------------- | ----- | ------- |
| *Authorization* | The `Basic` string followed by your [Base64-encoded](https://www.base64encode.org/) Client ID and Client Secret value. When you encode the Client ID and Client Secret values, separate them with a colon (`:`) character (for example, `Client_ID:Client_Secret`). | `Authorization: Basic Q2xpZW50X0lEOkNsaWVudF9TZWNyZXQ=` |

## OAuth refresh tokens

OAuth refresh tokens expire after 15 years. However, you **must** use the latest refresh token for a new refresh request. If you use an older refresh token to make a refresh request, you will receive an `Invalid Token` error.
```

### Embed Zoom into a website

```
# Embed Zoom into a website

There are two Web-based Software Development Kits (SDK) that let you embed Zoom into a website.

## Embed Zoom Meetings and Webinars with the Web Client SDK

To embed Zoom Meetings and Zoom Webinars into your website, use the [Web Client SDK](https://marketplace.zoom.us/docs/sdk/native-sdks/web). The Web Client SDK has two installation methods that support both basic HTML or JavaScript sites, as well as sites built with frontend frameworks like [Angular](https://angular.io/), [React](https://reactjs.org/), and [Vue.js](https://vuejs.org/).

### Use cases

* Embedding the Zoom Meeting and Webinar experience inside your website.
* Allowing users with or without a Zoom account to join meetings and webinars inside your website.

### Limitations

* Currently only supports 360p video quality.
* Currently lacks some features from the Zoom Client.
* Currently cannot be used to start meetings on behalf of Zoom users outside your account.
* Currently has limited customization.

### Implementation

* For bcasic HTML or JavaScript, import the Web SDK by linking the CDN scripts and styles in your `index.html` file.
* For frontend frameworks, import the Web SDK using [`npm`](https://www.npmjs.com/).

### Resources

* [Web Client SDK documentation](https://marketplace.zoom.us/docs/sdk/native-sdks/web)
* [Tutorials](https://medium.com/zoom-developer-blog/zoom-web-sdk-with-angular-6b080a6be38c)
* [Client Web SDK developer community](https://devforum.zoom.us/c/client-web-sdk)

#### Sample apps

* [Web app](https://github.com/zoom/sample-app-web)
* [Angular](https://github.com/zoom/websdk-sample-angular)
* [React](https://github.com/zoom/websdk-sample-react)
* [Vue.js](https://github.com/zoom/websdk-sample-vuejs)
* [Node.js](https://github.com/zoom/websdk-sample-signature-node.js)

## Accessing raw audio and video streams with the Web Video SDK

To access raw audio and video streams, use the [Web Video SDK](https://marketplace.zoom.us/docs/sdk/video/web). The Web Video SDK is a standalone developer product that utilizes Zoom's video and audio infrastructure for your website. Think of video and audio streaming as a service.

You cannot join Zoom Meetings or Webinars with the Fully Customizable SDK.

### Use case

Creating custom user experiences inside your website with audio and video streaming. For example, a multiplayer racing game where users can see and hear each other.

### Implementation

For frontend frameworks (for example, Angular), [download the Web Video SDK and Sample App via a Zoom App Marketplace Video SDK App](https://marketplace.zoom.us/docs/sdk/video/introduction).

### Resources

* [Web Video SDK documentation](https://marketplace.zoom.us/docs/sdk/video/web)
* [Web Video SDK developer community](https://devforum.zoom.us/c/web-video-sdk)
```

### Verify the Zoom macOS SDK was correctly added to your project

```
# Verify the Zoom macOS SDK was correctly added to your project

*Last verified on macOS SDK version 5.4.54528.1230*

The [Zoom macOS Software Development Kit (SDK)](https://marketplace.zoom.us/docs/sdk/native-sdks/macos) is more complex in comparison to our other SDKs. As a result, importing this SDK can be error prone, and can cause issues if incorrectly imported.

This guide covers:

* How to add the SDK to your Xcode project.
* Verifying that the SDK has been correctly added.

Before getting started, you will need:

* A Zoom developer account.
* Your Zoom Client SDK developer credentials.
* [Xcode 10](https://developer.apple.com/support/xcode/).
* [The macOS Zoom SDK](https://marketplace.zoom.us/docs/sdk/native-sdks/macos#downloading-and-using-the-zoom-mac-sdk).

## Integrating the SDK

To integrate the macOS SDK, perform the following actions:

### Verify the SDK files

After you download the macOS Zoom Client SDK, navigate to the `ZoomSDK` folder. Verify that all of the following files are present:

* `zmb.bundle`
* `zmLoader.bundle`
* `zWebService.bundle`
* `zVideoApp.bundle`
* `zSDKRes.bundle`
* `zKBCrypto.bundle`
* `zData.bundle`
* `zChatApp.bundle`
* `zAutoUpdate.bundle`
* `xmpp_framework.framework`
* `viperex.bundle`
* `viper.framework`
* `util.framework`
* `tp.framework`
* `ssb_sdkk.bundle`
* `protobuf.framework`
* `nydus.framework`
* `mphost.app`
* `mcm.bundle`
* `libssl.dylib`
* `libjson.dylib`
* `libcrypto.dylib`
* `curl64.framework`
* `cmmlib.framework`
* `capHost.app`
* `asproxy.framework`
* `aomhost.app`
* `aomagent.bundle`
* `annoter.bundle`
* `airhost.app`
* `ZoomSDKVideoUI.framework`
* `ZoomSDKChatUI.framework`
* `ZoomSDK.framework`
* `ZCommonUI.framework`
* `SDK_Transcode.app`
* `RingtoneRes.bundle`
* `CptHost.app`

If any of these files are missing, download a new copy of the SDK package.

### Import the files to your project

Import these files to your project. While there are multiple way of doing this. However, this guide will add the files via the **General** tab in the project's settings:

1. Click on the plus icon (**+**) under the **Embedded Binaries** section.
2. Navigate to the `ZoomSDK` folder.
3. Select all of the SDK files and add them to the project. The files should now appear in the **Embedded Binaries** section.
4. Navigate to the **Build Phases** tab. Depending on your project's settings, you may need to add a **Copy Files** phase if one is not present.
5. Add all of the SDK files to this phase with the **Frameworks** destination selected.

### Add files to Link Binary With Libraries

Add the following files to the **Link Binary With Libraries** phase:

* `ZoomSDK.framework`
* `libssl.dylib`
* `libjson.dylib`
* `libcrypto.dylib`

You can safely remove SDK files from other build phases because they are not required.

## Verification

Now that you have added all of the SDK files to your project, you must ensure that the code can reference the SDK and the project can be built.

To do this, first import the `ZoomSDK` into your `AppDelegate`:

For the Swift language:

```
import ZoomSDK
```

For the Objective-C language:

```
#import <ZoomSDK/ZoomSDK.h>
```

If this does **not** produce any errors, you should be able to build and run the project to verify that everything is in working order.

Any errors encountered in this step probably means that your project has some incorrect build settings. For more information, see the [Troubleshooting build settings](#troubleshooting-build-settings) section below.

## Troubleshooting build settings

There are a few places where build settings are likely to require some manual configuration if you have not previously added frameworks with this method.

To resolve build setting issues, perform the following steps:

1. Confirm the location of the references to the SDK files in Xcode. To do this, right-click any SDK file, then select **Show in Finder** from the menu.

2. Copy the file's absolute file path. This should also contain the rest of the SDK files, but you do not need to verify this if you have not modified the folder in any way.

3. Navigate to your project's **Build Settings** tab and find the **Framework Search Paths** and **Library Search Paths** settings. If you do not see the correct file path, paste the copied file path to both of these settings. You can use `${PROJECT_DIR}` to represent the root directory of your project.

4. Navigate back to the **General** tab. Right-click any of the SDK files and click the **Show in Finder** option. This should now display the updated file path.
```