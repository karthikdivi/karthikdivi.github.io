---
title: Adding (click) on anchor tag instead link in Angular
description: If you want to invoke some function on a user click you should first look for Buttons, But for what ever the reason (some times for styling) if you want to use an anchor tag you may want to stop the default behaviour of anchor tag. Otherwise If you use # in href it refreshes the current page and if you put nothing it takes you to home
tags: angular, anchor, click
created: 2018-08-31
---

If you want to invoke some function on a user click you should first look for Buttons, But for what ever the reason (some times for styling) if you want to use an anchor tag you may want to stop the default behaviour of anchor tag. Otherwise If you use # in href it refreshes the current page and if you put nothing it takes you to home. The following code shows you how to stop the default behaviour and calls the function. 

```javascript
<a ng-click="$event.preventDefault(); your_function()" href />
```
