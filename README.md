# ClientGatewayAccess

One-stop, static API entry point for integrating with both microservices that run on the `mim OE` runtime (`Runtime`) and backend microservices (`Backend`) that run in the traditional cloud.

---

`ClientGatewayAccess` organizes APIs into two categories:

- **`Runtime`** — microservices that **run on the `mim OE` runtime**.  
  These can run locally on devices *or* on cloud instances (e.g., AWS/GCP VMs) that host the runtime and act like runtime-enabled nodes.
- **`Backend`** — **traditional backend microservices** that run in the cloud.  
  These **do not** use the `mim OE` runtime.

This API is used by the *mimik Access* app and is available for integration in third-party applications.

---

## Usage

All functions are `static` and called directly:

```swift
// Runtime microservice call (mim OE-based)
let nodes = try await ClientGatewayAccess.Runtime.discoverNodes()

// Traditional backend microservice call (no mim OE)
let profile = try await ClientGatewayAccess.Backend.fetchUserProfile()
```

---

## Notes

- All APIs are asynchronous (`async`) and safe to call from concurrent contexts.  
- Some operations require authentication or prior runtime initialization.  

---

## Runtime

APIs for interacting with **runtime microservices** from a `mimik Access` client or third-party apps.


Runtime microservices run on the **`mim OE` runtime**.  
They may run:

- **On devices** (typical case)  
- **On cloud instances** (e.g., AWS/GCP VMs) that host the runtime and behave as runtime-enabled nodes  

Examples include:

- Content sharing via beams (`mBeam`)  
- Node discovery (`mSuperdrive`)  
- File storage (`mDrive`)  

Each runtime microservice provides a namespace of `static` methods for endpoint calls.

---


## Backend

APIs for integrating with **traditional mimik backend microservices**.


Backend microservices run in the mimik cloud and **do not use the `mim OE` runtime**.  
They provide user- and app-centric functionality such as:

- User profile management (`mPO`)  
- Friend relationships (`mFD`)  
- Thumbnail storage (`mTS`)  

Each backend microservice exposes a namespace of `static` methods for API operations.

---


## 🚀 Getting Started

The fastest way to get started:

1. Follow the onboarding tutorial  
   📘 [Step-by-Step Tutorial](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/02-index)

2. Add the required pods to your `Podfile`:
 
   ```ruby
   platform :ios, '16.0'
   source 'https://github.com/CocoaPods/Specs.git'
   source 'https://github.com/mimikgit/cocoapod-edge-specs.git'

   use_frameworks!
   inhibit_all_warnings!

   def mimik
     pod 'EdgeCore'
     pod 'mim-OE-ai-SE-iOS-developer'
     pod 'EdgeService'
   end

   target 'YourAppTarget' do
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

3. Get your mim OE license key from the [mimik Developer Console](https://developer.mimik.com/console)

---

## 💡 Key Concepts

**mim OE** (Operating Environment) is the runtime platform powering edge microservices and AI workloads. It can run on iOS devices, simulators, or macOS using Catalyst. The Client Library gives you direct control over:

- Service deployment
- Runtime lifecycle
- AI model execution
- Secure communication and auth

---

## ✨ Features Overview

The mimik Client Library provides a unified API to:

### 🔧 Initialize and Control mim OE
- Start, stop, and monitor the mim OE runtime
- Configure logging, runtime health, and startup parameters

### 🔐 Authenticate Developers and Users
- OAuth2-compliant developer and user login
- Support for token exchange, scopes, signup/login flows
- Handle account recovery, password changes, and deletions

### 🌍 Discover & Orchestrate Edge Nodes
- Auto-discover available edge nodes
- Route requests across hybrid clusters
- Register and manage services

### 📦 Deploy & Manage Microservices
- Deploy microservices or full use-case workflows
- Package using container-style config and update dynamically
- Scale, tear down, or update services via API

### 🤖 Unified AI Model Integration
- List available AI models across device, edge, and cloud
- Use a single interface to prompt vision and language models

### 🔁 Stream AI Prompts & Responses
- Send prompts and receive streaming replies
- Handle user-initiated prompt cancellations cleanly

### 📋 Standardized AI Outputs
- Unified output handling via `AssistantOutput`
- Supports chat UI, system automation, and batch processing

---

## 📦 Pod Distribution

Use the table below to choose the CocoaPods that best match your use case:

| Pod | Includes | AI Support | Recommended For |
|-----|----------|------------|------------------|
| [`EdgeCore`](https://github.com/mimikgit/cocoapod-EdgeCore) | Core |  | Always include |
| [`mim-OE-SE-iOS-developer`](https://github.com/mimikgit/cocoapod-mim-OE-SE-iOS-developer) | Core + mim OE | ❌ | Lightweight, non-AI apps |
| [`mim-OE-ai-SE-iOS-developer`](https://github.com/mimikgit/cocoapod-mim-OE-ai-SE-iOS-developer) | Core + mim OE + AI | ✅ | Vision/Language AI support |
| [`EdgeService`](https://github.com/mimikgit/cocoapod-EdgeService) | Deployment tools |  | For managing custom microservices |

> **✅ Recommended Default:** Add `EdgeCore` and `mim-OE-ai-SE-iOS-developer` to your Podfile.

---

## 📱 Supported Platforms

- **iOS Devices:** iOS 16.0+
- **iOS Simulators:** iOS 16.0+
- **Mac Catalyst:** macOS 14.0+

---

## 📄 Documentation

- **API Reference (EdgeCore):**  
  [EdgeClient Reference](https://mimikgit.github.io/cocoapod-EdgeCore/documentation/edgecore/edgeclient)  
  [EdgeEngineClient Protocol](https://mimikgit.github.io/cocoapod-EdgeCore/documentation/edgecore/edgeengineclient)

- **EdgeService Reference:**  
  [ClientGatewayAccess Docs](https://mimikgit.github.io/cocoapod-EdgeService/documentation/edgeservice)

- All APIs are also documented in Xcode with built-in method and struct descriptions.

---

## 🧪 Tutorials by Use Case

### ▶️ Get Started
- [Understanding the mimik Client Library for iOS](https://devdocs.mimik.com/key-concepts/10-index)

### 🛠️ Build Apps
- [Creating a Simple iOS App Using an Edge Microservice](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/01-index)
- [Integrating the mimik Client Library into Your iOS Project](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/02-index)

### ⚙️ Work with Runtime
- [Working with mim OE in an iOS Project](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/03-index)

### 📦 Manage Microservices
- [Deploying Edge Microservices](https://devdocs.mimik.com/tutorials/01-submenu/02-submenu/04-index)

---

## 📜 Licensing

To initialize `mim-OE-ai-SE-iOS-developer`, obtain a license key at:  
🔐 [mimik Developer Console](https://developer.mimik.com/console)

For enterprise projects or commercial distribution, contact:  
💼 [mimik Support](https://mimik.com/contact-us/)

---

## 👤 Author

[mimik](https://mimik.com)  
Learn more at [mimik Developer Documentation](https://devdocs.mimik.com)
