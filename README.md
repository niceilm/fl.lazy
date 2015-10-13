# fl.lazy
https://oclazyload.readme.io/ helper

## with ui-router
```
angular.module('someApp', [
  'ui.router',
  'fl.lazy'
]).config(['$stateProvider', '$lazyLoadHelperProvider', function($stateProvider, $lazyLoadHelperProvider){
  var modules = {
    grid: [
      {name: 'ui.grid', files: ['lib/angular-ui-grid/ui-grid.js', 'lib/angular-ui-grid/ui-grid.css']},
      {name: 'ui.grid.infiniteScroll', files: 'lib/angular-ui-grid/ui-grid.js'},
      {name: 'ui.grid.pagination', files: 'lib/angular-ui-grid/ui-grid.js'},
      {name: 'ui.grid.edit', files: 'lib/angular-ui-grid/ui-grid.js'},
      {name: 'ui.grid.cellNav', files: 'lib/angular-ui-grid/ui-grid.js'},
      {name: 'ui.grid.autoResize', files: 'lib/angular-ui-grid/ui-grid.js'},
      {name: 'ui.grid.resizeColumns', files: 'lib/angular-ui-grid/ui-grid.js'},
      {name: 'ui.grid.selection', files: 'lib/angular-ui-grid/ui-grid.js'}
    ],
    infiniteScroll: {name: 'infinite-scroll', files: 'lib/ngInfiniteScroll/ng-infinite-scroll.js'}
  };

  $lazyLoadHelperProvider.setOptions({
    urlArg : new Date().getTime(),
    modules : modules,
    filePath: "/",
    resolve:{
      someResolve:["$timeout", function($timeout){
        console.log("wait some time");
        return $timeout(function(){
        }, 1000);
      }]
    }
  });

  $stateProvider
    .state('home', {
      url: '/home',
      templateUrl: 'views/home.tpl',
      controller: 'HomeController',
      lazyModules: ['controllers/HomeController.js', modules.infiniteScroll]
    })

    .state('login', {
      url: '/login',
      templateUrl: 'views/login.tpl',
      controller: 'LoginController',
      lazyModules: 'controllers/LoginController.js'
    })
}]);
```

## with filter
```
    <md-dialog-content layout="column">
      <ng-include src="'views/form.tpl'|normalizeFileUrl"></ng-include>
    </md-dialog-content>

```
# Test

## install karma
```
npm install -g karma-cli karma-jasmine karma-chrome-launcher
bower install
```

## test
```
karma start karma.conf.js
```