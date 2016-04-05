# ocaml-cordova-plugin-list

This repository contains the plugin list of bindings in OCaml to cordova plugins using js_of_ocaml and gen_js_api.

## What's cordova, js_of_ocaml and gen_js_api ?

Cordova allows you to develop hybrid mobile application using web technologies such as HTML, CSS and Javascript. For more informations, see [the official website](https://cordova.apache.org/).
Through cordova plugins, you can access to the native components. To learn how to make cordova plugins, see [the official tutorial](https://cordova.apache.org/docs/en/latest/guide/hybrid/plugins/index.html).
You can find the official cordova plugin list [here](https://cordova.apache.org/plugins/).

Js\_of\_ocaml provides a compiler from ocaml to javascript. It's a way to develop Cordova application using ocaml. For more info, see [the ocsigen project](http://ocsigen.org/) which contains js\_of\_ocaml.

Gen_js_api:
```
gen_js_api aims at simplifying the creation of OCaml bindings for Javascript
libraries. It must currently be used with the js_of_ocaml compiler, although
other ways to run OCaml code "against" Javascript might be supported later
withthe same binding definitions (for instance, Bucklescript, or direct
embedding of a JS engine in a native OCaml application).
```
Source: [gen_js_api repository](https://github.com/lexifi/gen_js_api)

## How to contribute.

The name of the binding repository needs to be: ocaml-**name** where name is the official cordova plugin name.
For example, the binding to cordova-plugin-camera is in the ocaml-cordova-plugin-camera repository.

This convention is not respected for 'non-official' plugin such as [Toast](https://github.com/EddyVerbruggen/Toast-PhoneGap-Plugin) which is officially in the cordova-plugin-x-toast. The binding repository is cordova-plugin-toast. Same for the [Touch ID](https://github.com/leecrossley/cordova-plugin-touchid) plugin whose the official plugin is cordova-universal-touchid.

You can contribute by testing the plugins, especially on Windows Phone and ios devices.

Every plugins has an example application. Some are not done because we do not have time to do it (or we do not have any idea how to try it). Do not hesitate to develop them or test them. Those which don't have any example application were not tested but the code compiles.

## How does it work ?

The majority of bindings has two branches: js_of_ocaml and gen_js_api (master).

* The js_of_ocaml branch was the first done binding. It can be used on **compiler <= 4.02.3**. The weakness is the binding is **low-level** and depends on the **js_of_ocaml** library. You need to use Js type given by js_of_ocaml to use it. This binding is not provided for each plugin because **we do not recommend** to use this tag.

* The gen_js_api branch (= master) is the second binding and uses only gen_js_api. It allows you to use **any ocaml to javascript compiler** and has **high level binding**: you use 'standard' ocaml type such as string instead of Js.string type. The weakness is gen_js_api needs **compiler >= 4.03.0**.

**We recommend to use gen_js_api for simplicity and maintainability because we focus on the gen_js_api development.**

For the gen_js_api binding, we only provide the mli file. You need to use gen_js_api to get the ml file and compile the mli and ml files as said in the [gen_js_api use instruction](https://github.com/LexiFi/gen_js_api/blob/master/INSTALL_AND_USE.md).

## Improvements/To-do (contribute !!)

* For the moment, there are no ocaml documentations: we redirect you in the original plugin documentation and/or write comments in ml and mli files. We would like to have a full documentation for ocaml users.

* When a function has an optional parameter in javascript, we created two functions with a different name which binds to the same function in javascript (to avoid the unit at the end). After using the bindings, we find it is more convenient to use the unit at the end instead of a new function with a different name. We need to change the interface to have function with optional parameters in OCaml.

* Javascript function has sometimes a lot of parameters. Do we add labels for the bindings ?

* The structure of the bindings is not well defined. For the moment, each binding to a cordova plugin has his own github repository, defining his own class. It would be better to have a single file containing a single module named (for example) *cordova*. Each plugin will be a submodule. We must think about dead code optimizer.

* We could improve some plugins by using the cordova object. For example, some
  files destination are only available on ios devices and for the moment, the
  file plugin allows you to use them on android devices which gives null.

* For the moment, you also need to add manually the original cordova plugin with
```
cordova plugin add [plugin_name]
```
It could be interesting to analyse the source code of the cordova application (written in OCaml), detect used plugins and automatically run the cordova plugin add command. Use [merlin](https://github.com/the-lambda-church/merlin) method to analyse the code ?

If you have any idea, please contact us.

## Bindings list

* [ActivityIndicator](https://github.com/Initsogar/cordova-activityindicator):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-activityindicator
* [Barcode Scanner](https://github.com/phonegap/phonegap-plugin-barcodescanner):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-barcodescanner
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-barcodescanner-example
* Binding to cordova object:
	* Source files: https://github.com/dannywillems/ocaml-cordova
	* Example: https://github.com/dannywillems/ocaml-cordova-example
* [Camera](https://github.com/apache/cordova-plugin-camera):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-camera
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-camera-example
* [Clipboard](https://github.com/VersoSolutions/CordovaClipboard):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-clipboard
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-clipboard-example
* [Contacts](https://github.com/apache/cordova-plugin-contacts):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-contacts **Partial**
* [Device](https://github.com/apache/cordova-plugin-device):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-device
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-device-example
* [Device-motion](https://github.com/apache/cordova-plugin-device-motion):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-device-motion
* [Device-orientation](https://github.com/apache/cordova-plugin-device-orientation):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-device-orientation
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-device-orientation-example
* [Dialogs](https://github.com/apache/cordova-plugin-dialogs):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-dialogs
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-dialogs-example
* [File](https://github.com/apache/cordova-plugin-file):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-file
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-file-example
* [File opener](https://github.com/pwlin/cordova-plugin-file-opener2):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-file-opener
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-file-opener-example
* [Geolocation](https://github.com/apache/cordova-plugin-geolocation):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-geolocation
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-geolocation-example
* [Globalization](https://github.com/apache/cordova-plugin-globalization):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-globalization
* [Image Picker](https://github.com/wymsee/cordova-imagePicker):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-image-picker
* [Inappbrowser](https://github.com/apache/cordova-plugin-inappbrowser):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-inappbrowser
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-inappbrowser-example
* [Insomnia](https://github.com/EddyVerbruggen/Insomnia-PhoneGap-Plugin):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-insomnia
* [Loading Spinner](https://github.com/mobimentum/phonegap-plugin-loading-spinner):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-loading-spinner
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-loading-spinner-example
* [Media](https://github.com/apache/cordova-plugin-media):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-media
* [Media-capture](https://github.com/apache/cordova-plugin-media-capture):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-media-capture
* [Network-information](https://github.com/apache/cordova-plugin-network-information):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-network-information
* [Progress](https://github.com/leecrossley/cordova-plugin-progress): **Only iOS !!!**
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-progress
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-progress-example
* [Push notifications](https://github.com/phonegap/phonegap-plugin-push):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-push-notifications **Partial**
* [QRScanner](https://github.com/bitpay/cordova-plugin-qrscanner): **Only iOS !!!**
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-qrscanner
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-qrscanner-example
* [Screen orientation](https://github.com/gbenvenuti/cordova-plugin-screen-orientation):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-screen-orientation
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-screen-orientation-example
* [SMS](https://github.com/cordova-sms/cordova-sms-plugin):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-sms
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-sms-example
* [SplashScreen](https://github.com/apache/cordova-plugin-splashscreen)
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-splashscreen
* [StatusBar](https://github.com/apache/cordova-plugin-statusBar):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-statusbar
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-statusbar-example
* [Toast](https://github.com/EddyVerbruggen/Toast-PhoneGap-Plugin):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-toast
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-toast-example
* [Touch ID](https://github.com/leecrossley/cordova-plugin-touchid): **Only iOS !!**
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-touchid
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-touchid-example
* [Vibration](https://github.com/apache/cordova-plugin-vibration):
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-vibration
	* Example: https://github.com/dannywillems/ocaml-cordova-plugin-vibration-example
* [Video](https://github.com/moust/cordova-plugin-videoplayer): **Android only**
	* Source files: https://github.com/dannywillems/ocaml-cordova-plugin-videoplayer

### In development

* [Calendar](https://github.com/EddyVerbruggen/Calendar-PhoneGap-Plugin):
* [Facebook] (https://github.com/jeduan/cordova-plugin-facebook4)
* [File-transfer](https://github.com/apache/cordova-plugin-file-transfer):
* [Local notifications](https://github.com/katzer/cordova-plugin-local-notifications/):

### Not planned

* [Console](https://github.com/apache/cordova-plugin-console):

* [SQLite](https://github.com/litehelpers/Cordova-sqlite-storage):

## Maintainers

* Danny Willems
  * Twitter: [@dwillems42](https://twitter.com/dwillems42)
  * Github: https://github.com/dannywillems
  * Email: contact@danny-willems.be
  * Website: [danny-willems.be](https://danny-willems.be)
