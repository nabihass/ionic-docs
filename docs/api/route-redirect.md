---
title: "ion-route-redirect"
---

import Props from '@site/static/auto-generated/route-redirect/props.md';
import Events from '@site/static/auto-generated/route-redirect/events.md';
import Methods from '@site/static/auto-generated/route-redirect/methods.md';
import Parts from '@site/static/auto-generated/route-redirect/parts.md';
import CustomProps from '@site/static/auto-generated/route-redirect/custom-props.md';
import Slots from '@site/static/auto-generated/route-redirect/slots.md';

<head>
  <title>ion-route-redirect Plugin: Redirect 'from' a URL 'to' Another URL</title>
  <meta name="description" content="ion-route-redirect is used with as a direct child of an ion-router and redirects 'from' a URL 'to' another URL. Read to learn about the route redirect plugin." />
</head>

import EncapsulationPill from '@components/page/api/EncapsulationPill';


A route redirect can only be used with an `ion-router` as a direct child of it.

:::note
 Note: this component should only be used with vanilla and Stencil JavaScript projects. For Angular projects, use [`ion-router-outlet`](router-outlet.md) and the Angular router.
:::


The route redirect has two configurable properties:
 - `from`
 - `to`

It redirects "from" a URL "to" another URL. When the defined `ion-route-redirect` rule matches, the router will redirect from the path specified in the `from` property to the path in the `to` property. In order for a redirect to occur the `from` path needs to be an exact match to the navigated URL.


## Multiple Route Redirects

An arbitrary number of redirect routes can be defined inside an `ion-router`, but only one can match.

A route redirect will never call another redirect after its own redirect, since this could lead to infinite loops.

Take the following two redirects:

```html
<ion-router>
  <ion-route-redirect from="/admin" to="/login"></ion-route-redirect>
  <ion-route-redirect from="/login" to="/admin"></ion-route-redirect>
</ion-router>
```

If the user navigates to `/admin` the router will redirect to `/login` and stop there. It will never evaluate more than one redirect.




## Usage

```html
<!-- Redirects when the user navigates to `/admin` but
will NOT redirect if the user navigates to `/admin/posts` -->
<ion-route-redirect from="/admin" to="/login"></ion-route-redirect>

<!-- By adding the wilcard character (*), the redirect will match
any subpath of admin -->
<ion-route-redirect from="/admin/*" to="/login"></ion-route-redirect>
```

### Route Redirects as Guards

Redirection routes can work as guards to prevent users from navigating to certain areas of an application based on a given condition, such as if the user is authenticated or not.

A route redirect can be added and removed dynamically to redirect (or guard) some routes from being accessed. In the following example, all urls `*` will be redirected to the `/login` url if `isLoggedIn` is `false`.

```tsx
const isLoggedIn = false;

const router = document.querySelector('ion-router');
const routeRedirect = document.createElement('ion-route-redirect');
routeRedirect.setAttribute('from', '*');
routeRedirect.setAttribute('to', '/login');

if (!isLoggedIn) {
  router.appendChild(routeRedirect);
}
```

Alternatively, the value of `to` can be modified based on a condition. In the following example, the route redirect will check if the user is logged in and redirect to the `/login` url if not.

```html
<ion-route-redirect id="tutorialRedirect" from="*"></ion-route-redirect>
```

```javascript
const isLoggedIn = false;
const routeRedirect = document.querySelector('#tutorialRedirect');

routeRedirect.setAttribute('to', isLoggedIn ? undefined : '/login');
```

## Properties
<Props />

## Events
<Events />

## Methods
<Methods />

## CSS Shadow Parts
<Parts />

## CSS Custom Properties
<CustomProps />

## Slots
<Slots />