---
description: Basics on creating plugins for Xena.
---

# Creating plugins

Xena gives app developers easy access to adding elements to the Xena UI via plugins. These plugins can be of different types, e.g. a widget, tab, button, menu etc. A plugin consist of four things:

* **Title** This is the title of the plugin. This title is used as a title on widgets, tabs, buttons, menus etc.
* **Type** The type of a plugin describes which type of view the plugin is related to, f.eks. “ArticleDetails”, “OrderList” etc.
* **Placement** The placement of the plugin depends of the Type above. Some types have different placement options than others, eg. some types have “Widget”, “DetailsTab”, “StatisticTab” etc.
* **External URL**    If the placement requires content\(eg. widgets and tabs\) then the content is fetched from this URL. If the placement is an action\(eg. buttons, menues etc\) this URL is called when the user interacts with the plugin. Each plugin has a list of possible parameters, f.eks. the ID of the user whom acts with the plugin. Note the this URL is required to be via HTTPS.

### Styling the plugins

If you want to reuse Xena’s look’n’feel inside your plugin you can reference a subset of our stylesheet designed for plugins. Please review our design guide to learn more.

```markup
<link href="https://my.xena.biz/Content/css/xena-plugin.css" rel="stylesheet" />
```

{% page-ref page="../../user-interface/styleguide/" %}

### Sizing plugins

When using plugins in Xena it can be desirable to adjust the height of widgets, tabs etc to the height of the content provided from the App. This can be done using JavaScript provided by Xena.

The content of any plugin should always be responsive! So make sure that your plugins work with any width. To make the plugins height match that of your content, include this small snippet of JavaScript in your HTML just before the closing `</body>` tag.

```markup
<script src="https://my.xena.biz/scripts/xena.plugin.js"></script>
```

If you later to manually update the height of your plugin, this JavaScript function is available:

```javascript
Xena.updateHeight();
```

