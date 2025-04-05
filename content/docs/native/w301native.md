---
title: "Native Concept"
description: "Quick note for native apps concept"
summary: ""
date: 2025-03-19T19:53:05+08:00
lastmod: 2025-03-19T19:53:05+08:00
draft: false
weight: 301
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Concepts

Desktop and mobile apps are native apps. They runs faster as they are closer to the system, skipping the browser and are able to operate offline. The way of developing is different than web apps.

#### Progressive Web Apps (PWA) 

This is not a developement framework but a concept. PWA is a web-based app that behaves like a native app. It runs within a web browser, like a website, but can also be installed on a device's home screen, appearing as a native app.

Use PWA when you need cross-platform compatibility, or require offline functionality, all while avoiding the cost and complexity of native app development and don’t need deep OS integrations like file system access.

#### Hybrid Mobile Apps

These tools wrap web apps into mobile apps.

### Native Apps

#### Android Studio (Andriod Apps)

Android Studio is the official IDE for Android app development, built by Google.
It provides tools to develop, test, and deploy native Android applications. Uses Java and Kotlin as the primary programming languages, gradle as the build system, XML for UI layout design.

### Cross Platform Frameworks

#### Kotlin (Android First)

Kotlin language is powerful for cross-platform logic but not perfect for fully shared UI. For a 100% shared UI experience, Flutter, React Native or Electron are better choices. Kotlin is suitable for Andriod-first apps but want to share some logic.

| Framework | Platforms	| UI Code Shared? |	Notes |
| - | - | - | - |
| Kotlin Multiplatform (KMP) | Android, iOS, Desktop, Web |	❌ | Shares only logic, UI must be written per platform. |
| Jetpack Compose | Android | ✅ | Google’s recommended UI framework. |
| Compose for Desktop | Windows, macOS, Linux | ✅ | Based on Jetpack Compose. |
| Compose for Web | Web (Wasm/JS) | Partial	| Experimental, works with HTML/CSS. |
| Ktor | Backend | ✅ | Server-side Kotlin framework. |

[Kotlin Pokedex Example](https://github.com/mrcsxsiq/Kotlin-Pokedex)

{{< callout context="tip" title="Tips" icon="outline/rocket" >}}

Some popular apps created by Kotlin are Airbnb, Uber, Netflix.

{{< /callout >}}

#### Java (Desktop Apps)

Java Swing is a traditional UI library for Java application. While JavaFX is a modern GUI framework for building cross-platform desktop applications using Java. Supports CSS styling, making it feel like a web-based UI.

#### .NET (Microsoft C# Based)

.NET is Microsoft's ecosystem for building high-performance, cross-platform apps with C#. It is a solid choice for enterprise apps, but for full cross-platform development, alternatives like Flutter (Dart) or React Native (JavaScript) might be better if you need wider adoption and faster development.

| Technology | Platforms | UI Framework | Best For |
| - | - | - | - |
| WinUI (Windows App SDK) | Windows 10+ | XAML | Modern Windows apps, successor to WPF & UWP |
| MAUI (Multi-platform App UI) | Windows, macOS, iOS, Android | XAML | Modern cross-platform apps, successor of Xamarin.Forms |
| WPF (Windows Presentation Foundation)	| Windows only | XAML | Traditional Windows desktop apps |
| WinForms | Windows only | WinForms Designer | Simple Windows desktop apps |
| ASP.NET Blazor | Web, PWA, Mobile (via Blazor Hybrid) | HTML/CSS | Web apps with C# instead of JavaScript for backend |
| Blazor Hybrid	| Web & Windows | Web UI | Embed Blazor apps inside native apps |
| ASP.NET Core MVC | Web | HTML/CSS | Traditional web apps with C# instead of JavaScript |


{{< callout context="tip" title="Tips" icon="outline/rocket" >}}

Some popular website made by .NET are Stack Overflow, W3Schools. Performance desktop apps Forza Horizon, Unity is made by .NET.

{{< /callout >}}


#### Qt (Complex and Embedded Applications)

Qt (pronounced "cute") is a cross-platform application development framework that allows developement of Windows, macOS, Linux, Android, iOS, and embedded systems using single codebase. Qt is written in C++. Python (PyQt / PySide) bindings is supported to use Qt with Python instead of C++. Qt also comes with a set of rich libraries and API that handle GUI, networking, databases, multimedia, 3D graphics, and more. It provides a flexible UI framework, Qt Widgets & Qt Quick (QML) a powerful UI frameworks. 

{{< callout context="tip" title="Tips" icon="outline/rocket" >}}

Some popular apps created by Qt are VirtualBox, VLC media player, Spotify, and Google Earth, TeamViewer and Telegram.

{{< /callout >}}

#### Flutter (UI-Focused and Rapid Developement)

Flutter is a new open-source UI toolkit developed by Google for building natively compiled applications like Android, iOS, Web, Windows, macOS, Linux, and embedded from a single codebase. It uses Dart as its programming language which is similar to javascript, optimized for UI performance.

Flutter renders everything using its own rendering engine (Skia) to draw UI instead of native components. Flutter UI Styling is a widget-based UI system and fully customizable. Flutter has Material Design (Android) and Cupertino (iOS) widgets for native-like styling.

[Flutter Pokedex Example](https://github.com/hungps/flutter_pokedex)

{{< callout context="tip" title="Tips" icon="outline/rocket" >}}

Some popular apps created by Flutter are Google Earth, PUBG Mobile, WeChat, etc.

{{< /callout >}}

### Web-Based Frameworks

These apps mimic a web app, but it takes an overhead.

#### React Native

React Native allows you to write a single codebase for Web, Windows, MacOS, iOS and Android. Renders UI using native components .Uses Flexbox-based CSS-like styling and can integrate third-party UI libraries like NativeBase or React Native Paper.

{{< callout context="tip" title="Tips" icon="outline/rocket" >}}

Some popular apps created by React Native are Facebook, Instagram, Whatsapp.

{{< /callout >}}

#### Electron (Hybrid Desktop Native)

A JavaScript framework for building native applications on Windows, macOS, Linux with the same codebase using web technologies. Created by GitHub. Uses Chromium as the rendering engine and Node.js for backend functionality.

{{< callout context="tip" title="Tips" icon="outline/rocket" >}}

Some popular apps created by Electron are VS Code, Discord, Figma.

{{< /callout >}}

#### Tauri (Hybrid Desktop Native)

A lightweight alternative to Electron that doesn’t bundle Chromium. Uses the user’s existing browser engine (WebView), making it much smaller and faster.  Built with Rust for high performance and security on the backend. Smaller app size (~3MB) compared to Electron’s 100+MB.

#### Ionic (Hybrid Mobile Native)

Provides ready-made UI components (buttons, menus, modals, etc.) that look and feel native. Works with Angular, React, and Vue. Can be used with Capacitor or Cordova to access native device features (camera, GPS, etc.).

#### Capacitor (Hybrid Mobile Native)

Capacitor is a modern alternative to Cordova created by the Ionic team. Provides native API access (camera, geolocation, file system, etc.). Can also be used for Progressive Web Apps (PWAs).

#### Cordova

Cordova (formerly PhoneGap) is an older tool that also allows web developers to build mobile apps. Slower and more outdated compared to Capacitor.

Use Ionic + Capacitor for modern hybrid apps.

### Apple Apps

Swift is the programming language used for iOS and macOS apps replacing Objective-C. Apple develope using Xcode IDE.

#### SwiftUI

The cross-platform framework for building iOS, macOS, ans other apple system apps. Modern approach and easier to use. Able to live preview in Xcode.

#### AppKit

AppKit is the traditional framework only for macOS, used for decades and are mature for macOS. More complex but have better performance.