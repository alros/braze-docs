---
nav_title: Integration
article_title: Content Card Integration for Web
page_order: 0
platform: Web
channel: content cards
page_type: reference
description: "This article covers Content Card integration for Web, including Content Card data models, standard feed UI options, and additional card methods."

---

# Content Card integration

## Data models {#data-models}

The Braze Web SDK supports several unique Content Card card types, [ab.ClassicCard](https://js.appboycdn.com/web-sdk/latest/doc/ab.ClassicCard.html), [ab.Banner](https://js.appboycdn.com/web-sdk/latest/doc/ab.Banner.html), [ab.CaptionedImage](https://js.appboycdn.com/web-sdk/latest/doc/ab.CaptionedImage.html) which share a base model, [ab.Card](https://js.appboycdn.com/web-sdk/latest/doc/ab.Card.html).

## Content Card integration

The Braze Web SDK includes a Content Cards feed UI to speed up your integration efforts. If you would prefer to build your own UI instead, see [custom UI]({{site.baseurl}}/developer_guide/platform_integration_guides/web/content_cards/customization/custom_ui/).

### Standard feed UI

To use the included Content Cards UI, you'll need to specify where to show the feed on your website. 

In this example, we have a `<div id="feed"></div>` in which we want to place the Content Cards feed. 

We'll use three buttons to hide, show, or toggle (hide or show based on its current state) the feed.

```html

<button id="toggle" type="button">Toggle Cards Feed</button>
<button id="hide" type="button">Hide Cards Feed</button>
<button id="show" type="button">Show Cards Feed</button>

<nav>
    <h1>Your Personalized Feed</h1>
    <div id="feed"></div>
</nav>

<script>
   // we'll assume we have window.appboy
   // you can also use our npm integration instead:
   // import braze from "@braze/web-sdk";
    
   const toggle = document.getElementById("toggle");
   const hide = document.getElementById("hide");
   const show = document.getElementById("show");
   const feed = document.getElementById("feed");
    
   toggle.onclick = function(){
      appboy.display.toggleContentCards(feed);    
   }
    
   hide.onclick = function(){
      appboy.display.hideContentCards();
   }
    
   show.onclick = function(){
      appboy.display.showContentCards(feed);    
   }
</script>
```

When using the `toggleContentCards(parentNode, filterFunction)` and `showContentCards(parentNode, filterFunction)` methods, if no arguments are provided, all Content Cards will be shown in a fixed-position sidebar on the right-hand side of the page. Otherwise, the feed will be placed in the specified `parentNode` option.

|Parameters | Description |
|---|---|
|`parentNode` | The HTML node to render the Content Cards into. If the parent node already has a Braze Content Cards view as a direct descendant, the existing Content Cards will be replaced. For example, you should pass in `document.querySelector(".my-container")`.|
|`filterFunction` | A filter or sort function for cards displayed in this view. Invoked with the array of `ab.Card` objects, sorted by `{pinned, date}`. Expected to return an array of sorted `ab.Card` objects to render for this user. If omitted, all cards will be displayed. |
{: .reset-td-br-1 .reset-td-br-2}

[See the JS docs](https://js.appboycdn.com/web-sdk/latest/doc/module-display.html#.toggleContentCards) for more information on Content Card toggling.

## Additional card methods

|Method | Description | Link|
|---|---|---|
|`logCardImpressions`| Logs an impression event for the given list of cards. This is required when using a customized UI and not the Braze UI.| [JS Docs for logCardImpressions](https://js.appboycdn.com/web-sdk/latest/doc/modules/appboy.html#logcardimpressions)|
|`logCardClick`| Logs an click event for a given card. This is required when using a customized UI and not the Braze UI.| [JS Docs for logCardClick](https://js.appboycdn.com/web-sdk/latest/doc/modules/appboy.html#logcardclick)|
|`showContentCards`| Display the user's Content Cards. | [JS Docs for showContentCards](https://js.appboycdn.com/web-sdk/latest/doc/module-display.html#.showContentCards)|
|`hideContentCards`| Hide any Braze Content Cards currently showing. | [JS Docs for hideContentCards](https://js.appboycdn.com/web-sdk/latest/doc/module-display.html#.hideContentCards)
|`toggleContentCards`| Display the user's Content Cards. | [JS Docs for toggleContentCards](https://js.appboycdn.com/web-sdk/latest/doc/module-display.html#.toggleContentCards)
|`getCachedContentCards()`|Get all currently available cards from the last Content Cards refresh.| [JS Docs for getCachedContentCards](https://js.appboycdn.com/web-sdk/latest/doc/module-appboy.html#.getCachedContentCards)|
|`subscribeToContentCardsUpdates(subscriber)`| Subscribe to Content Cards updates. <br> The subscriber callback will be called whenever Content Cards are updated. |  [JS Docs for subscribeToContentCardsUpdates](https://js.appboycdn.com/web-sdk/latest/doc/module-appboy.html#.subscribeToContentCardsUpdates)|
|`dismissCard()`|Dismiss the card programmatically (available in v2.4.1).| [JS Docs for dismissCard](https://js.appboycdn.com/web-sdk/latest/doc/ab.Card.html#dismissCard)|
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}