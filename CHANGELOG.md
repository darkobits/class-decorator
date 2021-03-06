# Change Log

All notable changes to this project will be documented in this file. See [standard-version](https://github.com/conventional-changelog/standard-version) for commit guidelines.

<a name="4.1.11"></a>
## [4.1.11](https://github.com/darkobits/class-decorator/compare/v4.1.10...v4.1.11) (2019-01-29)


### Bug Fixes

* Instance delegates to parent of orphaned instance. ([db6c682](https://github.com/darkobits/class-decorator/commit/db6c682))



<a name="4.1.10"></a>
## [4.1.10](https://github.com/darkobits/class-decorator/compare/v4.1.9...v4.1.10) (2019-01-29)


### Bug Fixes

* Correct prototype of orphaned objects. ([c2c72eb](https://github.com/darkobits/class-decorator/commit/c2c72eb))



<a name="4.1.9"></a>
## [4.1.9](https://github.com/darkobits/class-decorator/compare/v4.1.8...v4.1.9) (2019-01-29)


### Bug Fixes

* Ensure proper cloning of getters/setters. ([43915eb](https://github.com/darkobits/class-decorator/commit/43915eb))



<a name="4.1.8"></a>
## [4.1.8](https://github.com/darkobits/class-decorator/compare/v4.1.7...v4.1.8) (2019-01-29)


### Bug Fixes

* Append to beginning of prototype chains. ([93d4a82](https://github.com/darkobits/class-decorator/commit/93d4a82))



<a name="4.1.7"></a>
## [4.1.7](https://github.com/darkobits/class-decorator/compare/v4.1.6...v4.1.7) (2019-01-28)


### Bug Fixes

* Recurse in findLastPrototypeBefore. ([4b81361](https://github.com/darkobits/class-decorator/commit/4b81361))



<a name="4.1.6"></a>
## [4.1.6](https://github.com/darkobits/class-decorator/compare/v4.1.5...v4.1.6) (2019-01-28)


### Bug Fixes

* Ensure prototypes of undecorated subclasses are visible to decorated constructors. ([a9f8cb7](https://github.com/darkobits/class-decorator/commit/a9f8cb7))



<a name="4.1.5"></a>
## [4.1.5](https://github.com/darkobits/class-decorators/compare/v4.1.4...v4.1.5) (2019-01-28)


### Bug Fixes

* Relocate all non-production code to own folder. ([9cf9f6d](https://github.com/darkobits/class-decorators/commit/9cf9f6d))



<a name="4.1.4"></a>
## [4.1.4](https://github.com/darkobits/class-decorators/compare/v4.1.3...v4.1.4) (2019-01-27)



<a name="4.1.3"></a>
## [4.1.3](https://github.com/darkobits/class-decorators/compare/v4.1.2...v4.1.3) (2019-01-27)


### Bug Fixes

* Ensure parent constructors receive correct prototype values set by child constructors. ([a0f2848](https://github.com/darkobits/class-decorators/commit/a0f2848))



<a name="4.1.2"></a>
## [4.1.2](https://github.com/darkobits/class-decorator/compare/v4.1.1...v4.1.2) (2019-01-22)



<a name="4.1.1"></a>
## [4.1.1](https://github.com/darkobits/class-decorator/compare/v4.1.0...v4.1.1) (2018-10-23)



<a name="4.1.0"></a>
# [4.1.0](https://github.com/darkobits/class-decorator/compare/v4.0.5...v4.1.0) (2018-08-17)


### Features

* Pass instance reference to method proxy. ([26314f3](https://github.com/darkobits/class-decorator/commit/26314f3))



<a name="4.0.5"></a>
## [4.0.5](https://github.com/darkobits/class-decorator/compare/v4.0.4...v4.0.5) (2018-08-17)



<a name="4.0.4"></a>
## [4.0.4](https://github.com/darkobits/class-decorator/compare/v4.0.3...v4.0.4) (2018-06-21)



<a name="4.0.3"></a>
## [4.0.3](https://github.com/darkobits/class-decorator/compare/v4.0.2...v4.0.3) (2018-06-13)



<a name="4.0.2"></a>
## [4.0.2](https://github.com/darkobits/class-decorator/compare/v4.0.1...v4.0.2) (2018-06-05)


### Bug Fixes

* Add fallback method to invoke canonical constructor. ([a180202](https://github.com/darkobits/class-decorator/commit/a180202))



<a name="4.0.1"></a>
## [4.0.1](https://github.com/darkobits/class-decorator/compare/v4.0.0...v4.0.1) (2018-06-05)



<a name="4.0.0"></a>
# [4.0.0](https://github.com/darkobits/class-decorator/compare/v3.1.0...v4.0.0) (2018-06-05)


### Code Refactoring

* Update implementation. ([04d0b99](https://github.com/darkobits/class-decorator/commit/04d0b99))


### Features

* **MethodDecorator:** Pass prototype to method decorators. ([02fb91f](https://github.com/darkobits/class-decorator/commit/02fb91f))


### BREAKING CHANGES

* This refactor introduces a new API and will require consumers to update code that uses this package.



<a name="3.1.0"></a>
# [3.1.0](https://github.com/darkobits/class-decorator/compare/v3.0.1...v3.1.0) (2017-10-02)


### Features

* Allow decorator descriptor object to be passed directly to classDecorator. ([468ce60](https://github.com/darkobits/class-decorator/commit/468ce60))



<a name="3.0.1"></a>
## [3.0.1](https://github.com/darkobits/class-decorator/compare/v3.0.0...v3.0.1) (2017-09-28)



<a name="3.0.0"></a>
# [3.0.0](https://github.com/darkobits/class-decorator/compare/v2.0.0...v3.0.0) (2017-09-26)


### Code Refactoring

* Use objects instead of classes to describe decorators. ([a881e10](https://github.com/darkobits/class-decorator/commit/a881e10))


### BREAKING CHANGES

* Consumers should now return an object rather than a class to describe decorator functionality.



<a name="2.0.0"></a>
# [2.0.0](https://github.com/darkobits/class-decorator/compare/v1.0.1...v2.0.0) (2017-09-21)


### Code Refactoring

* Refactor class-decorator. ([d5b6359](https://github.com/darkobits/class-decorator/commit/d5b6359))


### BREAKING CHANGES

* API not backwards-compatible.



<a name="1.0.1"></a>
## [1.0.1](https://github.com/darkobits/class-decorator/compare/v1.0.0...v1.0.1) (2017-09-19)


### Bug Fixes

* Add "files" to package.json. ([4ef6332](https://github.com/darkobits/class-decorator/commit/4ef6332))



<a name="1.0.0"></a>
# 1.0.0 (2017-09-19)


### Features

* Add `createClassDecorator`. 744d0a0
