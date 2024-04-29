# Appium

一、框架组成

Appium Core - defines the core APIs

Drivers - implement connectivity to specific platforms

Clients - implement Appium's API in specific languages

Plugins - change or extend Appium's core functionality



二、目标

打造移动设备自动化标准。Appium's initial goals were to develop an automation standard for mobile apps (iOS and Android).

UI 自动化的实现依赖于 WebDriver protocol。Appium introduces a universal UI automation interface is by implementing the WebDriver protocol.

Appium driver 根据 WebDriver protocol 通过集成不同平台的自动化工具并调用从而实现自动化控制功能。The Appium driver that supports iOS app automation is called the XCUITest Driver because ultimately what it does is convert the WebDriver protocol to XCUITest library calls.



三、相关技术

Appium is an _HTTP server_

Your test code (in its programming language) - owned by you&#x20;

The Appium client library - owned by Appium&#x20;

The Selenium client library - owned by Selenium&#x20;

The network (local or Internet) The Appium server - owned by Appium&#x20;

The Appium XCUITest driver - owned by Appium&#x20;

WebDriverAgent - owned by Appium&#x20;

Xcode - owned by Apple&#x20;

XCUITest - owned by Apple&#x20;

iOS itself - owned by Apple&#x20;

macOS (where Xcode and iOS simulators run) - owned by Apple



四、流程

服务器上插着设备，客户端发送 HTTP 请求过去，实现自动化控制。

标准命令集流程：

Find Element&#x20;

Click Element&#x20;

Get Page Source&#x20;

Take Screenshot







