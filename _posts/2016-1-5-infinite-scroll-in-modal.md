---
layout: post
title: Infinite scroll inside a modal
---

[ngInfiniteScroll](http://sroze.github.io/ngInfiniteScroll/) is a great library that helps you do an infinite scroll in just a few minutes.

Recently I needed to do an infinite scroll inside a modal. There were 2 issues with this : 

1) the page behind the modal was scrolling _(that wass an easy one)_  
2) the infinite scroll was "linked" to the scroll event of the main page and not to the content I was having in the modal

The fix is a very simple one, but took me a little bit to find it, because (for now) it is not yet in the official documentation of `ngInfiniteScroll`.

#### First of all let's fix the background that keeps scrolling 

When a modal is launched, the body element of the page will have a class called `.modal-open`. So let's tell it to stay still when our modal is shown : 

```css
body.modal-open {
  overflow: hidden;
}
```

Ok, that's done! But as I've said before, the infinite scroll was attached to the body element (on-scroll). And now our background page doesn't scroll anymore.

#### So let's fix the scrolling inside our modal

In order to tell `ngInfiniteScroll` that we want to load our items based on a specific parent, we'll have to use a new directive added in v1.0.1 : `infinite-scroll-container`.


```html
<div id="myList" infinite-scroll="getMoreItems()" infinite-scroll-container="'#myList'">
	<div ng-repeat="item in items">
		<h2>{{ item.firstName + ' ' + item.lastName }}</h2>
	</div>
</div>
```

So, this way we've informed `ngInfiniteScroll` that it should use the `#myList` container as parent when it comes to check if it should load new items or not. 

And that's all. Now everything is working as it should :+1:

> Answer found thanks to : [Joseph Lai](https://github.com/JTLai) & [Samuel Roze](https://github.com/sroze)

> PS: current stable version of `ngInfiniteScroll` is `1.0.0` so I used the master version.
