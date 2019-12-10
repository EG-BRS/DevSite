---
description: Basics on creating plugins for Xena.
---

# Creating plugins

Xena gives app developers easy access to adding elements to the Xena UI via plugins. These plugins can be of different types, e.g. a widget, tab, button, menu etc. A plugin consist of four things:

* **Title** This is the title of the plugin. This title is used as a title on widgets, tabs, buttons, menus etc.
* **Type** The type of a plugin describes which type of view the plugin is related to, f.eks. “ArticleDetails”, “OrderList” etc.
* **Placement** The placement of the plugin depends of the Type above. Some types have different placement options than others, eg. some types have “Widget”, “DetailsTab”, “StatisticTab” etc.
* **External URL** 
   If the placement requires content\(eg. widgets and tabs\) then the content is fetched from this URL. If the placement is an action\(eg. buttons, menues etc\) this URL is called when the user interacts with the plugin. Each plugin has a list of possible parameters, f.eks. the ID of the user whom acts with the plugin. Note the this URL is required to be via HTTPS.

## Styling the plugins

If you want to reuse Xena’s look’n’feel inside your plugin you can reference a subset of our stylesheet designed for plugins. Please review our design guide to learn more.

```markup

<link href="https://my.xena.biz/Content/css/xena-plugin.css" rel="stylesheet" />
```

{% page-ref page="../../user-interface/styleguide/" %}

## Interact with Xena frontend.
Xena provides the possibility to open Xena modules inside Xena from a plugin. 
To interact the plugin should include this small snippet of JavaScript in `<head>` tag.

```markup
<script src="https://my.xena.biz/scripts/xena.plugin.js"></script>
```

### Alert
`openAlert` has two optional parameters `message` and `title`. When called an alert dialog will be shown in Xena.
Syntax: `Xena.openAlert(message: string = '', title: string = '')`

**Example**
```
Xena.openAlert('You have reached todays limit', 'Wooops!');
```
![Example of an alert inside Xena](https://i.imgur.com/8fxVOfu.png)

### Confirm
`openConfirm` has one required and two optional parameters. The first parameter is the callback from which you will receive `true` if the user clicks "OK" and `false` if the user clicks "Cancel" or closes the confirm box.
Syntax: `Xena.openConfirm(callback: (result: boolean) => any, message: string = '', title: string = '')`

**Example**
```
Xena.openConfirm(function(result) {
	console.log('User confirmed', result);
}, 'Can you confirm this? :-)', 'Please confirm');
```
![enter image description here](https://i.imgur.com/fUl3IGG.png)

### Popup
`openPopup` has two required and one optional parameter. The first parameter is the callback for when the popup is closed. Either by the user or by your plugin. When the user closes the plugin from within Xena (via ESC-key) the callback with be called with null as the result argument: `callback(null)`.
Inside your plugin you can call `closePopup`with an optional parameter. This parameter can be used to send a result from you modal page to your page that initiated the modal.

Syntax: `Xena.openPopup(callback: (result: any) => any, url: string, title: string = '')`

Syntax: `Xena.closePopup(result: any = null)`

**Example**

Plugin page
```
Xena.openPopup(function(result) {
	console.log('Result:', result);
}, '{link-to-your-iframe}', 'Plugin Iframe in Modal');
```
Plugin iFrame page
```
Xena.closePopup({ status:  'Closed from iframe' });
```
![enter image description here](https://i.imgur.com/dk9HbLS.png)
When closing the modal on the button tied to the `Xena.closePopup` example the Plugin page will console.log the following `Result: {status: "Closed from iframe"}`.

### Sizing plugins
The content of any plugin should always be responsive! So make sure that your plugins work with any width.
Xena will automatically try to calculate the height of the plugins. But it is possible to overwrite this calculation by overwriting `Xena.getHeight`.

Syntax: `Xena.getHeight: () => number`
**Example**
```
Xena.getHeight = function() {
  return 200;
}
```
