# ocaml-cordova-plugin-list

This repository contains the plugin list of bindings in OCaml to cordova plugins using js_of_ocaml.

## What's cordova and js_of_ocaml ?

Cordova allows you to develop hybrid mobile application using web technologies such as HTML, CSS and Javascript. For more informations, see [the official website](https://cordova.apache.org/).
Through cordova plugins, you can access to the native components. To learn how to make cordova plugins, see [the official tutorial](https://cordova.apache.org/docs/en/latest/guide/hybrid/plugins/index.html).
You can find the official cordova plugin list [here](https://cordova.apache.org/plugins/).

Js\_of\_ocaml provides a compiler from ocaml to javascript. It's a way to develop Cordova application using ocaml. For more info, see [the ocsigen project](http://ocsigen.org/) which contains js\_of\_ocaml.

## How to contribute.

The name of the binding repository need to be:
ocaml-**name** where name is the official cordova plugin name.
For example, the binding to cordova-plugin-camera is in the ocaml-cordova-plugin-camera repository.

This convention is not respected for 'non-official' plugin such as [Toast](https://github.com/EddyVerbruggen/Toast-PhoneGap-Plugin) which is officially in the cordova-plugin-x-toast. The binding repository is cordova-plugin-toast. Same for the [Touch ID](https://github.com/leecrossley/cordova-plugin-touchid) plugin whose the official plugin is cordova-universal-touchid.

You can contribute by testing the plugins, especially on Windows Phone and ios devices.

## Improvements (contribute !!)

* For the moment, there are no ocaml documentations: we redirect you in the original plugin documentation and/or write comments in ml and mli files. We would like to have a full documentation for ocaml users. The goal is the ocaml developer would not know he's using a javascript binding.

* The structure of the bindings is not well defined. For the moment, each binding to a cordova plugin has his own github repository, defining his own class type. It would be better to have a single file containing a single module named (for example) *cordova*. Each plugin will be a submodule.

* For the moment, you also need to add manually the original cordova plugin with
```
cordova plugin add [plugin_name]
```
It could be interesting to analyse the source code of the cordova application (written in OCaml), detect used plugins and automatically run the cordova plugin add command.

* The binding is very low-level: it uses the Js types and all bindings to Javascript types. It would be more useful and elegant to abstract the js_of_ocaml library use: the developer would be allowed to use 'standard' ocaml types instead of Js types. For example, a plugin which needs a Js.js_string Js.t could have an interface with a 'standard' string type. The developer would not know he's using a binding to javascript.

If you have any idea, please contact me.

## Bindings list

* [ActivityIndicator](https://github.com/Initsogar/cordova-activityindicator)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-activityindicator
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-activityindicator-example **Not developed**
* Binding to cordova object:
	* Source files: https://github.com/dannywillems/ocaml-cordova
	* Example: https://github.com/dannywillems/ocaml-cordova-example
* [Camera](https://github.com/apache/cordova-plugin-camera):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-camera
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-camera-example
* [Clipboard](https://github.com/VersoSolutions/CordovaClipboard)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-clipboard
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-clipboard-example
* [Device](https://github.com/apache/cordova-plugin-device):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-device
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-device-example
* [Device-motion](https://github.com/apache/cordova-plugin-device-motion):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-device-motion
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-device-motion-example
* [Device-orientation](https://github.com/apache/cordova-plugin-device-orientation):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-device-orientation
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-device-orientation-example
* [File](https://github.com/apache/cordova-plugin-file):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-file
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-file-example
* [Geolocation](https://github.com/apache/cordova-plugin-geolocation):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-geolocation
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-geolocation-example
* [Inappbrowser](https://github.com/apache/cordova-plugin-inappbrowser):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-inappbrowser
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-inappbrowser-example
* [Insomnia](https://github.com/EddyVerbruggen/Insomnia-PhoneGap-Plugin):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-insomnia
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-insomnia-example
* [QRScanner](https://github.com/bitpay/cordova-plugin-qrscanner): **Only iOS !!!**
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-qrscanner
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-qrscanner-example
* [StatusBar](https://github.com/apache/cordova-plugin-statusBar):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-statusbar
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-statusbar-example
* [Toast](https://github.com/EddyVerbruggen/Toast-PhoneGap-Plugin):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-toast
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-toast-example
* [Touch ID](https://github.com/leecrossley/cordova-plugin-touchid)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-touchid
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-touchid-example
* [Vibration](https://github.com/apache/cordova-plugin-vibration):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-vibration
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-vibration-example

### In development

* [Barcode Scanner](https://github.com/phonegap/phonegap-plugin-barcodescanner)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-barcodescanner
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-barcodescanner-example
* [Calendar](https://github.com/EddyVerbruggen/Calendar-PhoneGap-Plugin)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-calendar
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-calendar-example
* [Contacts](https://github.com/apache/cordova-plugin-contacts)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-contacts
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-contacts-example
* [Dialogs](https://github.com/apache/cordova-plugin-dialogs):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-dialogs
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-dialogs-example
* [File opener](https://github.com/pwlin/cordova-plugin-file-opener2)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-file-opener
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-file-opener-example
* [File-transfer](https://github.com/apache/cordova-plugin-file-transfer):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-file-transfer
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-file-transfer-example
* [Globalization](https://github.com/apache/cordova-plugin-globalization):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-globalization
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-globalization-example
* [Image Picker](https://github.com/wymsee/cordova-imagePicker)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-image-picker
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-image-picker-example
* [Loading Spinner](https://github.com/mobimentum/phonegap-plugin-loading-spinner)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-loading-spinner
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-loading-spinner-example
* [Local notifications](https://github.com/katzer/cordova-plugin-local-notifications/)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-locale-notifications
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-locale-notifications-example
* [Media](https://github.com/apache/cordova-plugin-media):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-media
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-media-example
* [Media-capture](https://github.com/apache/cordova-plugin-media-capture):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-media-capture
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-media-capture-example
* [Network-information](https://github.com/apache/cordova-plugin-network-information):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-network-information
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-media-network-information-example
* [Progress](https://github.com/leecrossley/cordova-plugin-progress)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-progress
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-progress-example
* [Push notifications](https://github.com/phonegap/phonegap-plugin-push)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-push-notifications
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-push-notifications-example
* [SMS](https://github.com/cordova-sms/cordova-sms-plugin)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-sms
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-sms-example
* [SQLite](https://github.com/litehelpers/Cordova-sqlite-storage)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-sqlite
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-sqlite-example
* [Video](https://github.com/moust/cordova-plugin-videoplayer)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-videoplayer
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-videoplayer-example

### Not planned

* [Console](https://github.com/apache/cordova-plugin-console):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-console
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-console-example
