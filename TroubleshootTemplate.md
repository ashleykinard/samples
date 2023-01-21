# Troubleshooting Template

Use the following template to quickly get started writing a troubleshooting article:

```
# Troubleshooting Article Name

Describe the problem. Write a brief overview of the issue, such as how a user might find themselves in this situation or a reason why this issue happens.

## First problem statement (Heading 2)

Describe the solution. Keep it simple, straightforward, and concise (for example "Nothing happens when I begin broadcasting").

If you provide guided steps to resolve the problem (for example, 1, 2, 3), try to keep it around five steps. If an article requires more than five steps, consider creating a new document that's specific to that solution.

## Second problem statement (Heading 2)

### A subtopic related to the second problem (Heading 3)

## Third issue statement (Heading 2)

1. Step one to do the thing.
2. Step two to get the other thing done.
3. Step to solve the problem.
```

## Example

The following is an example troubleshooting article:

```
# Troubleshooting iOS screen sharing

The following article covers some of the common problems that you may encounter when attempting to implement the screen sharing functionality into your [Zoom iOS SDK](https://marketplace.zoom.us/docs/sdk/native-sdks/iOS/overview) app. These scenarios include information and solutions to help you resolve these problems.

## Nothing happens when I begin broadcasting

This may be the result of an incorrect [App Group ID](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_application-groups). The ID must be valid and set in the following locations in [Xcode](https://developer.apple.com/xcode/):

* Pass the ID as a string value into your `MobileRTCSDKInitContext` object when you initialize the SDK:

    ```python
    let mobileInitContext = MobileRTCSDKInitContext()

    mobileInitContext.appGroupId = 'group.com.yourTeam.yourAppGroupID'
    ```

* Pass the ID as a string value in the [Broadcast Extension](https://developer.apple.com/app-extensions/) target's `MobileRTCScreenShareService` object. This is usually located in the `SampleHandler` class:

    ```
    self.screenShareService = MobileRTCScreenShareService()

    screenShareService?.appGroup = 'group.com.yourTeam.yourAppGroupID'
    ```

* Set the ID in the **Signing & Capabilities** tab of your main target.

* Set the ID in the **Signing & Capabilities** tab of your **Broadcast Extension** target.

The App Group ID must be identical in each of these locations. If any one of these values is different, then the screen share function will not display in a meeting.

## I am using the sample application but I still cannot broadcast

As of SDK package version 5.4.54802.0124, screen sharing via broadcasting is functional. However, the default `group.zoom.us.MobileRTCSampleExtensionReplayKit` [App Group ID](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_application-groups) value will not work.

To resolve this issue, you must:

* [Provide your own App Group ID in specific objects and targets](#nothing-happens-when-i-begin-broadcasting) in Xcode.

* Ensure that you set the correct provisioning profile settings.

## I do not want to use a Broadcast Extension but I would like to broadcast it to the meeting

The SDK uses the [**ReplayKit**](https://developer.apple.com/documentation/replaykit) framework to send video and audio data from the device. Without using a **Broadcast Extension**, the SDK cannot broadcast.

## I am getting build errors after importing the MobileRTC and MobileRTCScreenShare frameworks

* Import the **MobileRTC** framework into your main target and not in the **Broadcast Extension** target. Make sure it is set to the `Embed & Sign` value.

* Import the **MobileRTCScreenShare** framework into your **Broadcast Extension** target and not your main target. Make sure it is set to the `Do not embed` value.

## I get errors after importing the MobileRTCScreenShare framework in my Broadcast Extension target

Make certain that you have imported the following required frameworks into your **Broadcast Extension** target and that they are set to the `Do not embed` value:

* [**CoreGraphics**](https://developer.apple.com/documentation/coregraphics/)
* [**CoreMedia**](https://developer.apple.com/documentation/coremedia/)
* [**CoreVideo**](https://developer.apple.com/documentation/corevideo/)
* [**ReplayKit**](https://developer.apple.com/documentation/replaykit)
* [**VideoToolbox**](https://developer.apple.com/documentation/videotoolbox/)

### Objective-C language

If you are using Objective-C in your **Broadcast Extension** target, make certain that your `SampleHandler` source file uses the `SampleHandler.mm` file name and not the `SampleHandler.m` file name.

### Swift language

If you are using Swift in your **Broadcast Extension** target, make certain that you add the `-lc++` value to the **Other linker flags** build setting.

## I do not see my app in the broadcast selection

Refer to the [Nothing happens when I begin broadcasting](#nothing-happens-when-i-begin-broadcasting) section.
```