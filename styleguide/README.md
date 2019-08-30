---
description: Learn how to build views with good UX.
---

# Design Guide

Xena strives for a unified and simple look. This help us build a UI that is easy to use and have recognizable patterns. Because Xena is used by a wide variety of businesses we have to take backward compatibility into consideration.

Xenas layout and classes are _based_ on Bootstrap version 3.3. For icons we use Font Awesome 5 Pro. And we have our own styling as well.

If you want to reuse Xena’s look’n’feel in your plugins, you can reference a subset of our stylesheet designed for plugins:

```markup
<link href="https://my.xena.biz/Content/css/xena-plugin.css" rel="stylesheet" />
```

This design guide is about the Xena Plugin Stylesheet.

## Create good UX in Xena

Using Bootstrap – or any other design framework – help styling components quickly and consistently. But it is not a user experience framework. The following will help you use the provided design to create a good user experience in Xena.

#### **Primary action**

There can be many buttons and links in a view, but only one primary action.

* Don’t: Do not give every button the styling for a primary button.
* Do: Clearly highlight the primary action the user can perform. All other buttons are not as important.

#### **Colors for buttons and alerts**

For most part, only the default styling and the primary button styling is needed. However, careful use of colors can in some cases communicate urgency or importance to the user.

* Don’t: Do not use different colors for the sake of decoration.
* Do: Use "danger" colors when performing a delete action or something an action failed. Use "success" colors when a job or action was completed successfully.

#### **Accessible on all devices**

Xena is available on computers, tablets and smartphones. It can be a challenge to accommodate much information on a small screen. Take this into consideration when you design your app, plugin or integration.

* Don’t: Do not make the UI dependent on hovering.
* Do: Make views and actions accessible to users using their fingers and users with mouse and keyboard.

