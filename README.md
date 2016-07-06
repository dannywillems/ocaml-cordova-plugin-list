# ocaml-cordova-plugin-list

<a href="url"><img src="https://raw.githubusercontent.com/dannywillems/ocaml-cordova-plugin-list/master/res/ocaml-cordova.png" align="center" height="220" width="501" ></a>

[![Join the chat at https://gitter.im/dannywillems/ocaml-cordova-plugin-list](https://badges.gitter.im/dannywillems/ocaml-cordova-plugin-list.svg)](https://gitter.im/dannywillems/ocaml-cordova-plugin-list?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

This repository contains the plugin list of bindings in OCaml to Cordova plugins using js_of_ocaml and gen_js_api.

- [ocaml-cordova-plugin-list](#ocaml-cordova-plugin-list)
  * [What are Cordova, js_of_ocaml and gen_js_api?](#what-are-cordova-js_of_ocaml-and-gen_js_api)
  * [How does it work?](#how-does-it-work)
  * [How can I use a binding?](#how-can-i-use-a-binding)
  * [What about documentation for each bindings?](#what-about-documentation-for-each-bindings)
  * [Bindings list](#bindings-list)
    + [In development](#in-development)
    + [Not planned](#not-planned)
  * [MISC](#misc)
    * [Be careful!](#be-careful)
    + [Help me! I need a binding but it is not listed!](#help-me-i-need-a-binding-but-it-is-not-listed)
    + [I did a binding to a Cordova plugin which are not listed or not yet done.](#i-did-a-binding-to-a-cordova-plugin-which-are-not-listed-or-not-yet-done)
    + [Improvements and To-do](#improvements-and-to-do)
  * [Maintainers](#maintainers)

## What are Cordova, js_of_ocaml and gen_js_api?

* [Cordova](https://cordova.apache.org) allows you to develop hybrid mobile applications using web technologies such as HTML, CSS and Javascript. For more informations, see [the official website](https://cordova.apache.org/).
Through Cordova plugins, you can access to the native components. To learn how to make Cordova plugins, see [the official tutorial](https://cordova.apache.org/docs/en/latest/guide/hybrid/plugins/index.html).
You can find the official Cordova plugin list [here](https://cordova.apache.org/plugins/).

* [js\_of\_ocaml](https://ocsigen.org/js_of_ocaml) provides a compiler from OCaml to Javascript. Since Cordova applications use Javascript, js\_of\_ocaml provides a way to develop mobile application using OCaml. For more info, see [the Ocsigen project](http://ocsigen.org/) which contains js\_of\_ocaml.

* [gen_js_api](https://github.com/lexifi/gen_js_api) aims at simplifying the creation of OCaml bindings for Javascript libraries. It must currently be used with the js_of_ocaml compiler, although other ways to run OCaml code "against" Javascript might be supported later withthe same binding definitions (for instance, Bucklescript, or direct embedding of a JS engine in a native OCaml application).

## How does it work?

Some bindings has two branches: gen_js_api (master) and js_of_ocaml.

* The gen_js_api branch (= master) uses only gen_js_api. It will allow you to use **any OCaml to javascript compiler** and has **high level binding**: you use «standard» OCaml types such as string instead of Js.js_string type. The weakness is gen_js_api needs **compiler >= 4.03.0**.

* **DEPRECATED**. The js_of_ocaml branch was the first done binding. It can be used on **compiler >= 4.00.0**. The weakness is the binding is **low-level** and depends on the **js_of_ocaml** library. You need to use Js types given by js_of_ocaml to use it. Bindings are not provided for each plugin.

**Use gen_js_api for simplicity and maintainability because js_of_ocaml branch is no longer supported.**

## How can I use a binding?

**Needs compiler >= 4.03.0**

This repository contains all opam repositories of the bindings (each binding has one repository for some reasons). It is **recommended** to add this repository as a remote opam package provider with
```Shell
opam repository add cordova https://github.com/dannywillems/ocaml-cordova-plugin-list.git
```

Each binding can now be installed. For example, the binding to the camera plugin is `cordova-plugin-camera`. So, if you want to install the camera binding, you need to use
```
opam install cordova-plugin-camera
```

The appropriate opam package is given in the appropriate Github repository (list is given [below](#bindings-list)).

If the plugin needs the binding to the standard js library such as [device-motion](https://github.com/dannywillems/ocaml-cordova-plugin-device-motion), you need to pin the [ocaml-js-stdlib](https://github.com/dannywillems/ocaml-js-stdlib) first.
If the plugin needs it, it is mentionned in the Github repository.

If you don't want to add this repository, you can manually pin each repository.

## What about documentation for each bindings?

Bindings interface are very closed to initial plugins Javascript interface. For
example, for the cordova-plugin-camera allowing you to take a picture through
*navigator.camera.getPicture* Javascript function, you use *Cordova_camera.get_picture*
OCaml function.
The equivalent OCaml code to
```Javascript
var success_callback = function(success) {
	console.log(success);
}

var error_callback = function(error) {
	console.log(error);
}

var options = {quality: 25; destinationType: Camera.DestinationType.DATA_URL}

navigator.camera.getPicture(success_callback, error_callback, options)
```
is
```OCaml
let success_callback success = Jsoo_lib.console_log success in

let error_callback error = Jsoo_lib.console_log error in

let options =
	Cordova_camera.create_options
		~quality:25
		~destination_type:Cordova_camera.Data_url
		()
	in

Cordova_camera.get_picture success_callback error_callback ~opt:options ()
```

(supposing Jsoo_lib.console_log is the binding to console.log function, see
[jsoo_lib](https://github.com/dannywillems/jsoo-lib)). Most functions are
implemented with optional arguments and these arguments are at the end of the
arguments list, so unit is often mandatory.

As the OCaml interface is very closed to Javascript interface, no OCaml
documentation is done yet. **Feel free to contribute**

Bindings which don't have example application are not tested. Please give a
feedback about it and open issues if it's the case.

## Bindings list

* [ActivityIndicator](https://github.com/Initsogar/cordova-activityindicator): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-activity-indicator.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-activity-indicator)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-activity-indicator
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-activity-indicator-example
* [Barcode Scanner](https://github.com/phonegap/phonegap-plugin-barcodescanner): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-barcode-scanner.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-barcode-scanner)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-barcode-scanner
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-barcode-scanner-example
* [Battery](https://github.com/apache/cordova-plugin-battery-status): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-battery-status.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-battery-status)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-battery-status
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-battery-status-example
* Binding to cordova object: [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova)
	* Source files: https://github.com/dannywillems/ocaml-cordova
	* Example: https://github.com/dannywillems/ocaml-cordova-example
* [Camera](https://github.com/apache/cordova-plugin-camera): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-camera.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-camera)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-camera
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-camera-example
* [Clipboard](https://github.com/VersoSolutions/CordovaClipboard): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-clipboard.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-clipboard)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-clipboard
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-clipboard-example
* [Contacts](https://github.com/apache/cordova-plugin-contacts): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-contacts.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-contacts)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-contacts **Partial, not released**
* [Date Picker](https://github.com/VitaliiBlagodir/cordova-plugin-datepicker): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-datepicker.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-datepicker)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-datepicker
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-datepicker-example
* [Device](https://github.com/apache/cordova-plugin-device): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-device.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-device)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-device
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-device-example
* [Device-motion](https://github.com/apache/cordova-plugin-device-motion): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-device-motion.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-device-motion)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-device-motion
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-device-motion-example
* [Device-orientation](https://github.com/apache/cordova-plugin-device-orientation): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-device-orientation.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-device-orientation)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-device-orientation
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-device-orientation-example
* [Dialogs](https://github.com/apache/cordova-plugin-dialogs): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-dialogs.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-dialogs)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-dialogs
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-dialogs-example
* [Email composer](https://github.com/katzer/cordova-plugin-email-composer): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-email-composer.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-email-composer)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-email-composer
* [File](https://github.com/apache/cordova-plugin-file): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-file.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-file)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-file
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-file-example
* [File opener](https://github.com/pwlin/cordova-plugin-file-opener2):[![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-file-opener.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-file-opener)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-file-opener
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-file-opener-example
* [File-transfer](https://github.com/apache/cordova-plugin-file-transfer):[![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-file-transfer.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-file-transfer)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-file-transfer
* [Geolocation](https://github.com/apache/cordova-plugin-geolocation): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-geolocation.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-geolocation)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-geolocation
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-geolocation-example
* [Globalization](https://github.com/apache/cordova-plugin-globalization): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-globalization.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-globalization)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-globalization
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-globalization-example
* [Keyboard](https://github.com/cjpearson/cordova-plugin-keyboard): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-keyboard.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-keyboard)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-keyboard
* [Image Picker](https://github.com/wymsee/cordova-imagePicker): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-image-picker.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-image-picker)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-image-picker
* [Inappbrowser](https://github.com/apache/cordova-plugin-inappbrowser): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-inappbrowser.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-inappbrowser)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-inappbrowser
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-inappbrowser-example
* [Insomnia](https://github.com/EddyVerbruggen/Insomnia-PhoneGap-Plugin):[![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-insomnia.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-insomnia)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-insomnia
* [Loading Spinner](https://github.com/mobimentum/phonegap-plugin-loading-spinner): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-loading-spinner.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-loading-spinner) **Deprecated: working on Cordova < 4**
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-loading-spinner
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-loading-spinner-example
* [Media](https://github.com/apache/cordova-plugin-media): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-media.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-media)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-media
* [Media-capture](https://github.com/apache/cordova-plugin-media-capture): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-media-capture.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-media-capture)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-media-capture
* [Network-information](https://github.com/apache/cordova-plugin-network-information): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-network-information.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-network-information)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-network-information
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-network-information-example
* [Progress](https://github.com/leecrossley/cordova-plugin-progress): **Only iOS!!!** [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-progress.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-progress)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-progress
* [Push notifications](https://github.com/phonegap/phonegap-plugin-push): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-push.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-push)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-push **Not tested**
* [QRScanner](https://github.com/bitpay/cordova-plugin-qrscanner): **Only iOS!!!** [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-qrscanner.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-qrscanner)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-qrscanner
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-qrscanner-example
* [Screen orientation](https://github.com/gbenvenuti/cordova-plugin-screen-orientation): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-screen-orientation.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-screen-orientation)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-screen-orientation
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-screen-orientation-example
* [SIM Card](https://github.com/pbakondy/cordova-plugin-sim): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-sim-card.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-sim-card)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-sim-card
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-sim-card-example
* [SMS](https://github.com/cordova-sms/cordova-sms-plugin): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-sms.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-sms)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-sms
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-sms-example
* [Social Sharing](https://github.com/EddyVerbruggen/SocialSharing-PhoneGap-Plugin) [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-sms.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-sms)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-social-sharing **Partial**
* [SplashScreen](https://github.com/apache/cordova-plugin-splashscreen): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-splashscreen.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-splashscreen)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-splashscreen
* [StatusBar](https://github.com/apache/cordova-plugin-statusBar): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-statusbar.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-statusbar)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-statusbar
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-statusbar-example
* [Toast](https://github.com/EddyVerbruggen/Toast-PhoneGap-Plugin): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-toast.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-toast)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-toast
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-toast-example
* [Touch ID](https://github.com/leecrossley/cordova-plugin-touchid): **Only iOS!!** [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-touchid.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-touchid)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-touchid
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-touchid-example
* [Vibration](https://github.com/apache/cordova-plugin-vibration): [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-vibration.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-vibration)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-vibration
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-vibration-example
* [Videoplayer](https://github.com/moust/cordova-plugin-videoplayer): **Android only** [![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-videoplayer.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-videoplayer)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-videoplayer

### In development

* [Calendar](https://github.com/EddyVerbruggen/Calendar-PhoneGap-Plugin)
* [Facebook] (https://github.com/jeduan/cordova-plugin-facebook4)
* [Hot code push](https://github.com/nordnet/cordova-hot-code-push)
* [Local notifications](https://github.com/katzer/cordova-plugin-local-notifications/)
* [Google Maps](https://github.com/mapsplugin/cordova-plugin-googlemaps)
* [PayPal](https://github.com/paypal/PayPal-Cordova-Plugin)

### Not planned

* [Bluetooth Serial](https://github.com/don/BluetoothSerial)
* [Console](https://github.com/apache/cordova-plugin-console):
* [Custom URL Scheme](https://github.com/EddyVerbruggen/Custom-URL-scheme)
* [SQLite](https://github.com/litehelpers/Cordova-sqlite-storage):

## MISC

### Be careful!

Most of bindings create new objects which are only available when the
deviceready event fires. You need to have as first lines:
```OCaml
let on_device_ready () =
	(* Your code using plugins here *)

let _ = Cordova.Event.device_ready on_device_ready
```

The module *Cordova* comes from the [bindings to the cordova object](https://github.com/dannywillems/ocaml-cordova) so you need to add it for each project. This module can be installed with
```
opam install cordova
```

### Help me! I need a binding but it is not listed!

Simply make a pull request and add it in the TO-DO section. Other people could be also interested.

### I did a binding to a Cordova plugin which are not listed or not yet done.

It will be a pleasure to add your binding to the list. Don't forget to add a license to your repository: LGPL or less restrictive (MIT, Apache, etc) is recommended. GPL will not be accepted because is too much restrictive.

Here some *plugin market* for inspiration
* [Telerik market](http://plugins.telerik.com/cordova): Cordova and NativeScript
  plugin market. Can be a source of inspiration.
* [PlugReg](http://www.plugreg.com/): list of Cordova plugins.

### Improvements and To-do

* Create a bindings plugin market like Cordova plugins have [here](https://cordova.apache.org/plugins/).
* For the moment, there are no OCaml documentations: we redirect you in the original plugin documentation and/or write comments in ml and mli files. We would like to have a full documentation for OCaml users.
* We could improve some plugins by using the cordova object. For example, some
  files destination are only available on ios devices and for the moment, the
  file plugin allows you to use them on android devices which gives null.
* For the moment, you also need to add manually the original Cordova plugin with
```
cordova plugin add [plugin_name]
```
It could be interesting to analyse the source code of the Cordova application (written in OCaml), detect used plugins and automatically run the cordova plugin add command. Use [merlin](https://github.com/the-lambda-church/merlin) method to analyse the code?

* A binary like *cordova* to create new Cordova project in OCaml and simplify when the user wants to add a plugin.

## Maintainers

* Danny Willems
  * Twitter: [@dwillems42](https://twitter.com/dwillems42)
  * Github: https://github.com/dannywillems
  * Email: contact@danny-willems.be
  * Website: [danny-willems.be](https://danny-willems.be)

## Related projects

* [OCaml for web programming](https://github.com/dannywillems/ocaml-for-web-programming)
* [Jsoo_lib](https://github.com/dannywillems/jsoo-lib)
* [ocaml-materializecss](https://github.com/dannywillems/ocaml-materializecss)
* [Ocsigen](https://ocsigen.org)
