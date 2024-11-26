# ``mimik Client Library``

**mimik Client Library** provides a programmatic interface for the mim OE Runtime (formerly known as edgeEngine), enabling its startup and integration into iOS projects.

## Overview

The purpose of the **mimik Client Library** is to provide a programmatic interface for working with the mim OE Runtime (formerly known as edgeEngine), accessing information about mobile device clusters, using on-device lightweight RESTful API microservices, and optionally integrating with mimik AI components.

These components provide various APIs that help developers with core operations, such as setting up the mim OE Runtime (formerly known as edgeEngine), authenticating developers, deploying edge microservices, and optionally integrating with [mimik ai](https://devdocs.mimik.com/tutorials/02-submenu/02-submenu/01-index).

## mimik Client Library cocoapods

Bundle configurations: developers have the option to choose from new bundling combinations for more tailored deployment: with or without AI Runtime. Integrate mim OE into your project with the choice of including or omitting the AI runtime, based on your application’s needs.

* [EdgeCore](https://github.com/mimikgit/cocoapod-EdgeCore) (required)
* [mim-OE-ai-SE-iOS-developer](https://github.com/mimikgit/cocoapod-mim-OE-ai-SE-iOS-developer) (with AI Runtime)
* [mim-OE-SE-iOS-developer](https://github.com/mimikgit/cocoapod-mim-OE-SE-iOS-developer) (without AI)
* [EdgeService](https://github.com/mimikgit/cocoapod-EdgeService) (optional)

Generally speaking, developers only need to add the **`mim-OE-ai-SE-iOS-developer`** and **EdgeCore** cocoapods to their projects. **EdgeService** is optional.

## Supported Platforms, Targets
* `iOS Devices running iOS 16+`
* `iOS Simulators running iOS 16+`
* `iOS Mac Catalyst running macOS 14.0`


## Requirements
```
iOS 16.0+
```

## Installation

To get started, simply incorporate a configuration such as this to your Podfile:


```swift
platform :ios, '16.0'
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/mimikgit/cocoapod-edge-specs.git'

use_frameworks!
inhibit_all_warnings!

def mimik
  pod 'EdgeCore'
  pod 'EdgeService'
  pod 'mim-OE-ai-SE-iOS-developer'
end

target '{target}' do
  mimik()
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['VALID_ARCHS'] = '$(ARCHS_STANDARD_64_BIT)'
      config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '16.0'
      config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
    end
  end
end
```

> **_NOTE:_** Developers can get their **developer edge license** for initializing [mim-OE-ai-SE-iOS-developer](https://github.com/mimikgit/cocoapod-mimOE-SE-iOS-developer) at the [mimik developer console](https://developer.mimik.com/console).

> **_NOTE:_** Enterprise project developers should request their **enterprise edge license** from [mimik support](https://developer.mimik.com/support/).


## Documentation

`EdgeCore/EdgeClient` API reference documentation can be found  [here](https://mimikgit.github.io/cocoapod-EdgeCore/documentation/edgecore/edgeclient). Alternatively a docc archive file can be downloaded as a [zip file](https://github.com/mimikgit/cocoapod-EdgeCore/tree/main/EdgeCore.doccarchive.zip) and opened locally in Xcode.

`EdgeEngineClient` platform protocol API reference documentation is [here](https://mimikgit.github.io/cocoapod-EdgeCore/documentation/edgecore/edgeengineclient).

`EdgeService` API references are available [here](https://mimikgit.github.io/cocoapod-EdgeService/documentation/edgeservice/).

## EdgeServiceClient

Provides API for integrating mimik edge and backend microservices.

> **To enable EdgeServiceClient** API in the project, add [EdgeService](https://github.com/mimikgit/cocoapod-EdgeService) cocoapod to your `Podfile`.

### Profile - mPO backend microservice

- ``EdgeServiceClient/Backend/mPO/addUserProfileNotificationsConsent(service:authorization:consent:)``
- ``EdgeServiceClient/Backend/mPO/deleteUserProfileNotificationsConsent(service:authorization:consentId:)``
- ``EdgeServiceClient/Backend/mPO/findUser(service:authorization:email:)``
- ``EdgeServiceClient/Backend/mPO/updateUserProfile(service:authorization:update:)``
- ``EdgeServiceClient/Backend/mPO/updateUserProfileAttributes(service:authorization:attributes:)``
- ``EdgeServiceClient/Backend/mPO/updateUserProfileProperties(service:authorization:parameters:)``
- ``EdgeServiceClient/Backend/mPO/userProfile(service:authorization:)``
- ``EdgeServiceClient/Backend/mPO/addressSuggestions(service:authorization:address:maxSuggestions:language:countries:geoLocation:geoFence:)``
- ``EdgeServiceClient/Backend/mPO/places(service:authorization:address:maxPlaces:language:countries:geoLocation:geoFence:)``

### Friends - mFD backend microservice

- ``EdgeServiceClient/Backend/mFD/acceptFriendship(service:authorization:friendId:)``
- ``EdgeServiceClient/Backend/mFD/cancelFriendship(service:authorization:friendId:)``
- ``EdgeServiceClient/Backend/mFD/friends(service:authorization:)``
- ``EdgeServiceClient/Backend/mFD/receivedFriendRequests(service:authorization:)``
- ``EdgeServiceClient/Backend/mFD/requestFriendship(service:authorization:friendId:)``
- ``EdgeServiceClient/Backend/mFD/sentFriendRequests(service:authorization:)``


### Beams - mBeam edge microservice

- ``EdgeServiceClient/Microservice/mBeam/beamTokens(userAccessToken:edgeEngineFullPathUrl:microservice:ownerCode:)``
- ``EdgeServiceClient/Microservice/mBeam/beams(userAccessToken:edgeEngineFullPathUrl:microservice:ownerCode:)``
- ``EdgeServiceClient/Microservice/mBeam/create(beam:userAccessToken:edgeEngineFullPathUrl:edgeAccessToken:microservice:ownerCode:)``
- ``EdgeServiceClient/Microservice/mBeam/deleteBeam(id:userAccessToken:edgeEngineFullPathUrl:microservice:ownerCode:)``
- ``EdgeServiceClient/Microservice/mBeam/deleteBeamToken(id:userAccessToken:edgeEngineFullPathUrl:microservice:ownerCode:)``
- ``EdgeServiceClient/Microservice/mBeam/openBeam(id:userAccessToken:edgeEngineFullPathUrl:edgeAccessToken:microservice:ownerCode:)``
- ``EdgeServiceClient/Microservice/mBeam/updateBeam(id:userAccessToken:edgeEngineFullPathUrl:microservice:ownerCode:status:)``
- ``EdgeServiceClient/Microservice/mBeam/updateBeamToken(id:userAccessToken:edgeEngineFullPathUrl:microservice:ownerCode:status:)``

### Drive - mDrive edge microservice

- ``EdgeServiceClient/Microservice/mDrive/create(file:userAccessToken:edgeEngineFullPathUrl:microservice:driveOwnerCode:)``
- ``EdgeServiceClient/Microservice/mDrive/delete(file:userAccessToken:edgeEngineFullPathUrl:microservice:driveOwnerCode:)``
- ``EdgeServiceClient/Microservice/mDrive/fileWith(localId:userAccessToken:edgeEngineFullPathUrl:microservice:)``
- ``EdgeServiceClient/Microservice/mDrive/files(userAccessToken:edgeEngineFullPathUrl:microservice:)``

### Device Clusters - mSuperdrive edge microservice

- ``EdgeServiceClient/Microservice/mSuperdrive/accountNodes(userAccessToken:edgeEngineFullPathUrl:microservice:edgeAccessToken:)``
- ``EdgeServiceClient/Microservice/mSuperdrive/friendNodes(userAccessToken:edgeEngineFullPathUrl:edgeAccessToken:microservice:)``
- ``EdgeServiceClient/Microservice/mSuperdrive/nearbyNodes(userAccessToken:edgeEngineFullPathUrl:microservice:edgeAccessToken:)``
- ``EdgeServiceClient/Microservice/mSuperdrive/nodePresenceCheck(nodeId:userAccessToken:edgeEngineFullPathUrl:edgeAccessToken:microservice:)``


## Tutorials

After installation, try the following tutorials:

- [Understanding the mimik Client Library for iOS](https://devdocs.mimik.com/key-concepts/10-index).
- [Creating a Simple iOS Application that Uses an edge microservice](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/01-index).
- [Integrating the mimik Client Library into an iOS project](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/02-index).
- [Working with mimOE in an iOS project](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/03-index).
- [Working with edge microservices in an iOS project](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/04-index).


## Author

[mimik Technology, Inc.](https://mimik.com)

More details about how the edgeEngine platform revolutionizes computing with the hybrid-cloud approach are at [mimik Developer Documentation](https://devdocs.mimik.com).


## License

Developers can get their developer edge license by following this [tutorial](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/03-index).

For details about an enterprise edge license please contact [mimik support](https://mimik.com/contact-us/).
