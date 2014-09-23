![angular](slides/fronteers/img/square.png "angular")


## Search app
```javascript
(function(angular) {
	'use strict';

	var searchApp = angular.module('Search');

	searchApp.config( ... );
	searchApp.value('searchServiceURL', ... );
	searchApp.controller('SearchResultsCtrl', ... );
	searchApp.directive('searchForm', ... );
	searchApp.directive('autoSuggest', ... );
	searchApp.factory('Autosuggest', ... );
} (angular));
```

Note:
Module voorbeeld search


### Configuratie

```javascript
...

searchApp.config(['$routeProvider',
	function ($routeProvider) {
		$routeProvider.when('/search', {
			templateUrl: 'modules/search/templates/search.html',
			controller: 'SearchCtrl'
		});
		$routeProvider.when('/search/:query', {
			templateUrl: 'modules/search/templates/results.html',
			controller: 'SearchResultsCtrl',
			reloadOnSearch: false
		});
	}
]);

...
```

Note:
Configuratie van module, elke module is in dit project een pagina


## Social Media app 'core'
```javascript
...

var socMedApp = angular.module('socialMediaProject', [
	// Downloaded plugins:
	'plugin_1',
	'plugin_2',
	// Project modules:
	'module_1',
	'module_2',
	'module_3'
]);

...
```


### Config
```javascript
...

socMedApp.config(['$routeProvider',
	function ($routeProvider) {
		$routeProvider.otherwise({
			templateUrl: 'modules/socmed/templates/404.html',
			controller: '404Ctrl'
		});
	}
]);

...
```


### Directive
```javascript
...

socMedApp.directive('spinner', function () {
	return {
		restrict: 'E',
		replace: true,
		templateUrl: 'modules/socmed/templates/spinner.html'
	};
});

...
```


### Filter
```javascript
...

socMedApp.filter('flatten', function () {
	return function (i) {
		if (i) {
			i = i.replace(/\s/g, '-').replace('.', '').toLowerCase();
			return i;
		}
	};
});

...
```


### Overig
```javascript
...

socMedApp.value('localeSupported', [
	'en-US'
]);

socMedApp.controller('404Ctrl', [function () {}]);

...
```
