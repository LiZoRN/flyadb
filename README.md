FlyAdb
======

# Runtime Description

![](https://github.com/LiZoRN/flyadb/doc/image/runtime.jpg)

1. Case: 
The case could be runned by cmd or TAT . And It shall be loose coupling with any other Frontends.
2. Automator: 
This module is a Python wrapper of Android uiautomator and monkeyrunner testing framework. Uiautomator backend  works on Android 4.1+ simply with Android device attached via adb, no need to install anything on Android device. 
Monkeyrunner libs is not supported yet. Automator will parse the cmd and invoke the adb or rpcclient(uiautomator)/monkeyrunner to Device.
3. Device: 
Device process the cmd by adbd, monkey, or rpcServer which is a Task Registered with  UIAutomator Methods.


# Static Structure

![](https://github.com/LiZoRN/flyadb/doc/image/staticstruct.jpg)
 
1. The yellow color modules is supported as Libs, contain uiautomator and monkeyrunner:
	JsonRPCServer: A Listening Task that registered the uiautomator Method.
	JsonRPCClient: Remote Procedure Call the uiautomator Method by JSON
	 Adb: adb interface and some atomic interface that ONLY  ADB USED
	AutomatorDevice: Realize the IDevice Interface and wrapper android device that CONNECTED BY UIAUTOMATOR
	MonkeyUser: Realize the IDevice Interface and wrapper android device that CONNECTED BY MONKEYRUNNER
2. The Creen color modules is supported as mod that wrapper the test module:
	Common: Some common method and the backend Factory, log, config etc.
	AppConfig: Read the configure file of appinfo, the heterogeneity of the product shall be unified here.
	 Module: Test module libs that should be supported and used as component.
3. Case: Junit Style test case that Composited with test modules. The description of the method :
	SetUp: Prepare each test condition here. The test will run this method prior to each test. Such as “enter some activity”
	TearDown: Recovery test condition here. The test will invoke that method after each test. Such as “back_to_home()”
	testModule: implement test case .
	SetUpClass: Prepare the whole test condition here. It will be called prior to all test case.
	TearDown Class: Get and calculate the test result here. It will be called after all test finished.

