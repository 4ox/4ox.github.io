---
layout: post
title:  "Get Paramter from URL"
date:   2015-10-13 12:00:00 +0900
categories: javascript
---

Import parameters with a single line function

```javascript
//get url parameter
var p={};location.search.split(/\?|&/).map(function(s){s=s.split("=");if(s[0])p[s[0]]=s[1];});
```

