# Angular Coding Standard

*A work in progress coding standard to be followed for writing Angular code*

## Index

1. [Controllers](#controllers)
1. [Services](#services)
1. [Directives](#directives)
1. [Filters](#filters)
1. [Templates Partials](#templates-partials)


## Controllers

  - Do not manipulate DOM in your controllers. Use directives instead.
  - The naming of the controller is done using the controller's functionality.
  - The controllers are named UpperCamelCase and suffix substring `Ctrl` in the end. E.g: `AdminMenuCtrl`, `HotelStaffCtrl`, `ZestCtrl`, etc.
  - The controllers should not be defined as globals. Use array syntax for controller definitions:

    ```javascript
    // bad
    var AdminMenuCtrl = function ($scope, $rootScope, AdminMenuSrv) {

    }

    // good
    Admin.controller('AdminMenuCtrl', [
    	'$scope',
    	'$rootScope',
    	'AdminMenuSrv',
    	function ($scope, $rootScope, AdminMenuSrv) {

    	}
    ]);
    ```

  - Use the original names of the controller's dependencies.

  	```javascript
  	// bad
    Admin.controller('AdminMenuCtrl', [
    	'$scope',
    	'$rootScope',
    	'AdminMenuSrv',
    	function (s, rs, ams) {

    	}
    ]);

    // good
    Admin.controller('AdminMenuCtrl', [
    	'$scope',
    	'$rootScope',
    	'AdminMenuSrv',
    	function ($scope, $rootScope, AdminMenuSrv) {

    	}
    ]);
    ```

  - Make the controllers as lean as possible. Abstract commonly used functions into a service.
  - Communicate within different controllers using method invocation (possible when children wants to communicate with parent) or `$emit`, `$broadcast` and `$on` methods. The emitted and broadcasted messages should be kept to a minimum.
  - Make a list of all messages which are passed using `$emit`, `$broadcast` and manage it carefully because of name collisions and possible bugs.

**[back to top](#index)**


## Services

  - The services are named UpperCamelCase and suffix substring `Srv` in the end. E.g: `AdminMenuSrv`, `HotelStaffSrv`, `ZestSrv`, etc.
  - Encapsulate business logic in services.
  - For data services always create getters and setters rather than digging in Controllers:

  	```javascript
    Admin.factory('AdminMenuSrv', [
    	'$q',
    	'$http',
    	function ($q, $http) {
    		var factory = {};

    		var factory.data = [];

    		factory.get = function(url, options) {

    		};

    		factory.set = function(url, params, options) {

    		};

    		factory.hasPromoUpsell = function() {

    		}

    		factory.addMenu = function(parent, name, options) {
    		  
    		}

    		return factory;
    	}
    ]);
    ```

**[back to top](#index)**


## Directive

  - Name your directives with lowerCamelCase.
  - Use `scope` instead of `$scope` in your link function.
  - Use custom prefixes for your directives to prevent name collisions with third-party libraries.
  - Do not use ng or ui prefixes since they are reserved for AngularJS and AngularJS UI usage.
  - Use directives as attributes or elements instead of comments or classes, this will make your code more readable.
  - Use `$scope.$on('$destroy', fn)` for cleaning up. This is especially useful when you're wrapping third-party plugins as directives.

**[back to top](#index)**


## Filters

  - Name your filters with lowerCamelCase.
  - Make your filters as light as possible. They are called often during the `$digest` loop so creating a slow filter will slow down your app.
  - Do a single thing in your filters, keep them simple. More complex manipulations can be achieved by piping existing filters.

**[back to top](#index)**


## Templates Partials
  
  - Name your templates with lowerCamelCase.
  - Name ui-states partials based on their parent-child relationship, e.g:

  	+ staycard.html
  	+ staycard.guestcard.html
    + staycard.reservations.html
    + reservations.details.html
    + details.payment.html
    + details.wakeUpCall.html

  - Use `ng-bind` or `ng-cloak` instead of simple `{{ }}` to prevent flashing content.
  - Avoid writing complex expressions in the templates. Rather use methods or boolean properties in $scope.
  - When you need to set the `src` of an image dynamically use `ng-src` instead of src with `{{}}` template.

**[back to top](#index)**
