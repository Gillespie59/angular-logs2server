# angular-logs2server

This new angular module will give the possibility to send to your server all client exceptions thrown by Angular or by your own JavaScript code. 

## How to use it ?

First, you have to import the main JS file in your HTML

```javascript
<script type="text/javascript" src="angular-log2server.js"></script>
```

Then, you need to import the new AngularJS module in your AngularJS application :

```javascript
angular.module('myapp', ['logs2server']);
```

## Structure of the data sent to the server

The log2server AngularJS module will send to your server, via a POST request, a JSON object : 

```javascript
{
	exception: the original exception (string),
	cause: the cause of the original exception (string),
	navigator: {
		appCodeName: the result of $window.navigator.appCodeName (string),
		appName: the result of $window.navigator.appName (string),
		appVersion: the result of $window.navigator.appVersion (string),
		cookieEnabled: the result of $window.navigator.cookieEnabled (boolean),
		hardwareConcurrency: the result of $window.navigator.hardwareConcurrency (integer),
		language: the result of $window.navigator.language (string),
		languages: the result of $window.navigator.languages (Array<string>),
		maxTouchPoints: the result of $window.navigator.maxTouchPoints (integer),
		onLine: the result of $window.navigator.onLine (boolean),
		platform: the result of $window.navigator.platform (string),
		product: the result of $window.navigator.product (string),
		productSub: the result of $window.navigator.productSub (string),
		userAgent: the result of $window.navigator.userAgent (string),
		vendor: the result of $window.navigator.vendor (string),
		vendorSub: the result of $window.navigator.vendorSub (string)
	},
	location: {
		absUrl: the result of $location.absUrl() (string),
		hash: the result of $location.hash() (string),
		host: the result of $location.host() (string),
		path: the result of $location.path() (string),
		port: the result of $location.port() (string),
		protocol: the result of $location.protocol() (string),
		url: the result of $location.url() (string)
	}

}
```

## How to configure logs2server

The logs2server module define a new Provider (log2serverConfigService) you can use in the config phase for your application, in order to configure this module. 

You can configure two things : 
- The URL of your REST API (the setServerURL method)
- A flag to enable/disabled the default behiavor of the exceptionHandler service (the setDefaultExceptionHandler method)

```javascript
(function(){
	'use strict';

	angular.module('test7').config(RouterConfig);

	RouterConfig.$inject = ['log2serverConfigServiceProvider'];
	function RouterConfig(log2serverConfigServiceProvider) {
		log2serverConfigServiceProvider.setServerURL("/try");
		log2serverConfigServiceProvider.setDefaultExceptionHandler(false);
	}
})();

```
