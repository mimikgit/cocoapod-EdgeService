# ``EdgeService``

mimik Client Library provides a programmatic way to work with the edgeEngine Runtime to access information about the mobile device on which the application is running.

@Metadata {
    @CallToAction(purpose: link, url: "https://github.com/mimikgit/cocoapod-EdgeService")
    @PageKind(article)
    @PageColor(orange)
}


## Overview

The purpose of the **mimik Client Library for iOS** is to provide a programmatic way to work with the edgeEngine Runtime to access information about the mobile device on which the application is running, as well as mobile devices running within a cluster of mobile devices that are hosting the edgeEngine Runtime. Also, to allow developers to use edge microservices running within a particular cluster.

The **mimik Client Library for iOS suite** consists of three individual cocoapod components:

    - EdgeCore
    - EdgeEngineDeveloper (or EdgeEngine for enterprise solutions) 
    - EdgeService

By leveraging the **`EdgeCore cocoapod component`**, developers can build applications compatible with the edgeEngine Runtime.

Additionally, this component provides utility APIs that help developers with core operations such as Authentication, edgeEngine Runtime Setup, deployment of edge microservices and handling of network calls.

Furthermore, the **`EdgeEngineDeveloper (or EdgeEngine for enterprise solutions) cocoapod component`** provides edgeEngine Runtime lifecycle control API, as well as vendoring the actual edgeEngine Runtime binary into the iOS project.

Expanding the client library ecosystem is the **`EdgeService cocoapod component`**, providing API for integrating mimik edge and backend microservices.


## Supported Platforms, Targets
* `iOS Devices running iOS 15+`
* `iOS Simulators running iOS 15+`
* `iOS Mac Catalyst running macOS 12.0`


## Requirements
```
iOS 15.0+
```

## Installation

To install `EdgeCore` and `EdgeEngineDeveloper (or EdgeEngine for enterprise solutions)` cocoapods simply add the following lines to your Podfile:

> **_NOTE:_** Developers wanting to use their **developer edge license** from [mimik developer console](https://developer.mimik.com/console) should specify  [EdgeEngineDeveloper](https://github.com/mimikgit/cocoapod-EdgeEngineDeveloper) cocoapod in their `Podfile`.

> **_NOTE:_** Enterprise developers should specify [EdgeEngine](https://github.com/mimikgit/cocoapod-EdgeEngine) cocoapod in their `Podfile` and use the **full edge license** they received from [mimik support](https://developer.mimik.com/support/).


```swift
platform :ios, '15.0'
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/mimikgit/cocoapod-edge-specs.git'

use_frameworks!
inhibit_all_warnings!

def mimik
  pod 'EdgeCore'
  pod 'EdgeEngineDeveloper'
  pod 'EdgeService'
  ### or pod 'EdgeEngine' (see the two notes above)
end

target '{target}' do
  mimik()
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['ENABLE_BITCODE'] = 'NO'
      config.build_settings['VALID_ARCHS'] = '$(ARCHS_STANDARD_64_BIT)'
      config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '15.0'
      config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
    end
  end
end
```

## Tutorials

After installation, try the following tutorials:

- [Integrating the mimik Client Library into an iOS project](https://devdocs.mimik.com/tutorials/11-index)
- [Working with edgeEngine in an iOS project](https://devdocs.mimik.com/tutorials/12-index)
- [Working with edge microservices in an iOS project](https://devdocs.mimik.com/tutorials/13-index)
- [Creating a Simple iOS Application that Uses an edge microservice](https://devdocs.mimik.com/tutorials/10-index)


## Documentation

`EdgeCore/EdgeClient` API reference documentation can be found  [online](https://mimikgit.github.io/cocoapod-EdgeCore/documentation/edgecore/edgeclient) or as a [zip file](https://github.com/mimikgit/cocoapod-EdgeCore/tree/main/EdgeCore.doccarchive.zip).

`EdgeEngineClient` platform protocol API reference documentation can also be found [online](https://mimikgit.github.io/cocoapod-EdgeCore/documentation/edgecore/edgeengineclient).

`EdgeServiceClient` API reference documentation can also be found [online](https://mimikgit.github.io/cocoapod-EdgeService/documentation/edgeservice/edgeserviceclient) or as a [zip file](https://github.com/mimikgit/cocoapod-EdgeService/tree/main/EdgeService.doccarchive.zip).

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

## mimik client libraries

Explore all mimik client libraries [available on Github](https://github.com/search?q=cocoapod-Edge).

Cocoapod sets:

* [EdgeClientLibraryDeveloper = (EdgeCore + EdgeEngineDeveloper)](https://github.com/mimikgit/cocoapod-EdgeClientLibraryDeveloper)
* [EdgeClientLibrary = (EdgeCore + EdgeEngine)](https://github.com/mimikgit/cocoapod-EdgeClientLibrary)
 
Cocoapod individual pods:
 
* [EdgeCore](https://github.com/mimikgit/cocoapod-EdgeCore)
* [EdgeEngineDeveloper](https://github.com/mimikgit/cocoapod-EdgeEngineDeveloper)
* [EdgeEngine](https://github.com/mimikgit/cocoapod-EdgeEngine)
* [EdgeService](https://github.com/mimikgit/cocoapod-EdgeService)


## Author

[mimik Technology, Inc.](https://mimik.com)

More details about how the edgeEngine platform revolutionizes computing with the hybrid-cloud approach are at [mimik Developer Documentation](https://devdocs.mimik.com).


## License

Developers can get their developer edge license by following this [tutorial](https://devdocs.mimik.com/tutorials/02-index).

For details about a full edge license please contact [mimik support](https://mimik.com/contact-us/).
