#Authenticatie


```javascript
var sessionModule = angular.module('Session', ['ngRoute']);
sessionModule.config(['$routeProvider',
	function ($routeProvider) {
		$routeProvider.when('/login', {
			templateUrl: 'modules/session/templates/login-page.html'
		});
		$routeProvider.when('/logout', {
			templateUrl: 'modules/session/templates/login-page.html',
			controller: 'LogoutCtrl'
		});
	}
]);
```


```javascript
sessionModule.controller('LogoutCtrl', ['$scope', 'AuthService', '$location', '$rootScope',
	function ($scope, AuthService, $location, $rootScope) {
		$scope.currentPage = 'Logout';
		AuthService.logout();
		$location.path('/login');
	}
]);

sessionModule.constant('USER_ROLES', {
	user: 'user'
});
```


```javascript
sessionModule.directive('loginForm', function () {
	...
});

sessionModule.value('sessionServiceURL', {
	login: '/login',
	logout: '/login'
});
```


```javascript
sessionModule.factory('AuthService', ['$http', '$cookieStore', 'UserSession', 'sessionServiceURL',
	function ($http, $cookieStore, UserSession, serviceUrl) {
		return {
			login: function (credentials) {
				return $http({
					method: 'POST',
					url: serviceUrl.login,
					data: credentials,
					isArray: false
				})
				.success(function (data/*, status, headers, config*/) {
					UserSession.create(data['uid']);
				});
			},
			isAuthenticated: function () {
				return UserSession.hasSession();
			},
			isAuthorized: function (authorizedRoles) {
				if (!angular.isArray(authorizedRoles)) {
					authorizedRoles = [authorizedRoles];
				}
				return (this.isAuthenticated() &&
					authorizedRoles.indexOf(UserSession.userRole) !== -1);
			},
			logout: function () {
				UserSession.destroy();
			}
		};
	}
]);
```


```javascript
sessionModule.service('UserSession', ['$cookieStore',
	function ($cookieStore) {
		this.create = function (userId) {
			this.id = userId;
			this.userRole = 'user'; // there is only 1 role for now
			$cookieStore.put('uid', userId);
		};
		this.destroy = function () {
			this.id = null;
			this.userRole = null;
			$cookieStore.remove('uid');
		};
		this.hasSession = function () {
			// !! because zero could be a valid id
			if (!this.id && !!$cookieStore.get('uid')) {
				this.id = $cookieStore.get('uid');
				this.userRole = 'user';
			}
			return !!this.id;
		};
		return this;
	}
]);

```