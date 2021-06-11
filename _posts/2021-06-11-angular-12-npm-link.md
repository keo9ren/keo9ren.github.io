---
layout: post
title: Angular 12 (Ionic included) npm link fix
--- 
Angular 12 switched the default bundler to webpack 5, which treats node_modules as immutable per default.

A negative side effect of this if you `npm link` your library changes in the lib wil not be reflected in the app after recompilation.

You can set the environment variable `NG_BUILD_CACHE=0` to fix this temporarily.
Beware that might slow down your builds.

Windows (Powershell):
```shell
$env:NG_BUILD_CACHE=0
ionic serve
```

A other, hacky, alternative is to switch, `@angular-devkit/build-angular` while developing and switch it back for production builds.

Shell
```shell
npm install -D @angular-devkit/build-angular@0.1102.14
ionic serve
```

```shell
npm install -D @angular-devkit/build-angular@12.0.3
ionic build --prod
```
