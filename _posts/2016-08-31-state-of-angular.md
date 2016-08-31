---
layout: post
title: "The State of Angular in 2016"
comments: true
category:
---

I saw some haughtily titled articles ([The State of Javascript in 2016](https://medium.com/javascript-and-opinions/state-of-the-art-javascript-in-2016-ab67fc68eb0b#.i9nbs2snf) by Francois Ward and [The State of Javascript: Front-End Frameworks](https://medium.com/@sachagreif/the-state-of-javascript-front-end-frameworks-1a2d8a61510#.wixfq9jkh) by Sacha Greif) and they struck me. I cannot talk with the same breadth and authority on Angular or JavaScript but I do know--from having to hack together a project in Angular 1 in less than 2 days just now--a little bit about the "health" of Angular.

Its actually looking good.

## tl;dr
+ Components have drastically simplified workflow and organization for Angular 1 apps
+ Google's new component router is currently broken and the old router is unusable for components.
+ It is entirely necessary to use the beta version of angular-ui-router for component routing.
+ es6 style imports have vastly simplified things in terms of organization and file-structure, however, it is still very unclear and inconsistent between libraries when to import a variable, whether or not that variable represents a module name (is a string) or an actual angular module, (e.g. [this issue for the new ui-router](https://github.com/angular-ui/ui-router/issues/2506)).
+ exporting modules using es6 syntax is also weird since module "names" are exported.
+ Angular doesn't exactly jive with classes for controllers and controller classes are not supported by third party dependency injection libraries (such as ng-annotate).
+ Using libraries like [ng-forward](https://github.com/ngUpgraders/ng-forward) (which is no longer maintained) or [ng-metadata](https://github.com/ngParty/ng-metadata) (which is pure Typescript) can reconcile Angular 1's weird way of handling modules with es6 and allow you to use new JS features but do not actually make Angular 1 apps "Angular 2 ready" as much as they claim, especially if you app relies heavily on libraries like "Angular Material" or "UI-bootstrap"

## The story
So my sister needed a survey app since all the ones online were ad supported and sucky, I vaguely remembered forking a survey app about a year ago and modifying it here and there (for some market research on an app that didn't happen) so I offered to modify my app for her.

The app needed drastic changes (it was using Grunt and Bower, dark days) and noticeably simply didn't work (maybe because I was working on Windows, who knows?), so I figured I would make a day of it and refactor it. Not so hard, right?

## Problems immediately: module loading
I found an Angular 1 es6 starter repo and began my genius work of copying and pasting their webpack configuration wholesale, splitting the views and controllers into components, adding import and export statements and glancing at documentation. When everything was mostly in order, I decided to bring the app back to life one piece at a time in the router and immediately into this gloriously descriptive error:

```
angular.js:68Uncaught Error: [$injector:modulerr] Failed to instantiate module pollingApp due to:
Error: [$injector:modulerr] Failed to instantiate module {"_invokeQueue":[],"_configBlocks":[],"_runBlocks":[],"requires":["edit","login","main","nav","result","survey"],"name":"components"} due to:
Error: [ng:areq] Argument 'module' is not a function, got Object
```

Angular's error messages are terrible. This error, back in the day, was thrown if a module's array of dependencies was malformed but with es6 modules it adds a layer of confusion. A Google search of this exact problem will produce not a lot in the way of how or why this is the case. Although you may come across [this stack exchange post](http://stackoverflow.com/questions/30794824/error-ngareq-argument-module-is-not-a-function-got-object).

It turns out Angular modules are not CommonJS modules at all and that you have to export a module's ```name``` attribute so Angular can handle it with its internal module system. Has this always been the case? Bizarre.

*Note: this issue applies to a number of Angular libraries as well. If you've ever wondered indefinitely whether to load the module then add it as a string to your angular module dependencies or to import a variable and add that to your dependencies or import a variable and then add its ```name``` attribute to your dependencies this is why. However, it looks like a few major libraries are on board with supporting es6 modules, e.g. [ui-router](https://github.com/angular-ui/ui-router/issues/2506)*

## The official component router is broken
Components. Are. Great. Components are the future (nevermind that Angular components somewhat resemble Backbone views). Refactoring old Angular controllers and views into components is not too difficult, --even an enjoyable, task. However, it may not be immediately apparent how these new components jive with Angular's router(s) (there are currently three official routers). At this time, they don't, at least officially, since [the new component router has been deprecated and they are working on a new API]((http://stackoverflow.com/questions/33652668/angular-1-5-and-new-component-router)).

Whatever the state of Angular's router, the new UI-router (angular-ui-router@1.0.0-beta.1) handles components beautifully with a very simple api. It needs little in the way of explanation:

    const routes = function($stateProvider, $urlRouterProvider) {
      /* @ngInject */

      $stateProvider
        .state('edit', {
          url: '/edit',
          component: 'editComponent'
      });

      $stateProvider
        .state('main', {
          url: '/main',
          component: 'mainComponent'
      });

      $stateProvider
        .state('result', {
          url: '/result',
          component: 'resultComponent'
      });

      $urlRouterProvider.otherwise('main');
    }

    export default routes;


It is clear this is the solution for component routing at this time.

## Why not ng-forward or ng-metadata?

Interesting. I spent a fair amount of time working on two ng-forward projects with the intent to carry them over to Angular 2. It is true that ng-forward handles a lot of Angular's weirdness in terms of module loading (it automagically handles and loads the ```name``` attribute when you load your dependencies). I found that I could think in pure JavaScript more frequently, break away from Angular's services (like ```$http```) and use vanilla JS libraries, and used those projects to explore making decorators and using other es6-7 features. However, two points made using ng-forward a deal breaker:

1. not one of the components I made for those projects, as far as I am aware, is usable by a pure Angular app.
2. I was still unable to escape the need to manipulate the ```$scope``` digest cycle.

Thus, they are weird mutant apps that will probably never make it to Angular 2 since they rely on libraries programmed "in and for Angular" like Angular Material and UI-Bootstrap and are not backward compatible with Angular 1. The fact that [ng-forward is no longer maintained](https://github.com/ngUpgraders/ng-forward/issues/174) was the nail in the coffin. The only hope for the future of these apps is that Angular 2 versions of their current UI frameworks will become mature enough for me to refactor my app with them--starting the cycle of dependency anew.

Ng-metadata more strongly prohibits developers from doing things like manipulating the digest cycle (by simple making it not available). As a framework, it is much more disciplinary since the Typescript requirement makes the addition of third-party libraries a more costly decision. However, ng-metadata added too much overhead for a simple quiz app.

As an aside, ng-metadata so thoroughly imitates Angular 2, I can't see a reason to use it instead of actually making an Angular 2 app.

Angular 1 components are robust enough even without es6 classes, decorators and other sugar. In fact, they solve many of the problems that have plagued the framework by isolating their responsibility to their view and data (e.g., their scope is isolated, they have "well defined" life-cycle hooks so there is no question of whether a controller or directive should handle view logic first, they have a "well defined" api so you aren't trying to piece together what a model looks like from html templates and controller code, etc...) and allowing developers to organize their apps according to a component hierarchy.

## Minification is still a problem
When it came time to deploy, I had all but forgotten this famous gotcha. Do not mangle your variable names when you minify your JavaScript.

## Wrap up

Angular is still a bear. I find its template syntax to be awkward, its directives cumbersome, and I don't like how it imperializes my way of thinking and programming (i.e., I don't like how there is an "angular version" of everything or an "angular way of doing" this or that). However, if I need a project or prototype working by myself in like two days, Angular is still my goto framework.

Besides these and a few other "gotchas" building a quick and dirty Angular 1 app in 2016 is a fast and enjoyable experience. Components are like Angular on easy mode and really reduce the intellectual overhead of using the framework. My main gripe is still modules and dependency injection. Perhaps at one point, in the days of global variables and script tags, Angular's DI was a necessary solution but now it seems cumbersome and arcane. Hopefully, Angular 1 will further simplify.
