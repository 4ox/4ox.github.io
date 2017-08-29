---
layout: post
title:  "GET URL의 파라미터를 가져오는 함수"
date:   2015-10-13 12:00:00 +0900
categories: javascript
---

# GET URL의 파라미터를 가져오는 한줄 함수
```javascript
//get url parameter
var p={};location.search.split(/\?|&/).map(function(s){s=s.split("=");if(s[0])p[s[0]]=s[1];});
```

# 위 함수 응용 파라미터와 쿠키를 가져오고 세팅할수 있는 함수
```javascript
var y = (function(){	
	//location search 와 document cookie 처리
	function json( str ){
		var json={};
		str.split( /\?|&|;/ ).map(function( str ){
			var arr = str.split("=");
			if( arr[0] ){
				json[ arr[0].trim() ] = arr[1].trim();
			}
		});
		return json;
	}

	//Parameter
	var param = json( location.search );
	function getParam( key ){
		return key ? param[ key ] : param;
	}

	//Cookie
	var cookie;
	function getCookie( key ){
		cookie = json( document.cookie );
		return key ? cookie[ key ] : cookie;
	}
	function setCookie(key,value,expire){
		var date = new Date();
		date.setDate( date.getDate()+expire );
		document.cookie = key + "=" + escape( value ) + ( ( expire == null ) ? "" : ";expires=" + date.toUTCString() );
		cookie = getCookie();
	}

	//Return Function
	return {
		getParam : getParam
		, getCookie : getCookie
		, setCookie : setCookie
	}
})();
```

