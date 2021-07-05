---
layout: post
title: Ionic Angular and Webstorm - Picking the right import
--- 
Generally the autoimport feature of WebStorm is excellent. That makes the fow occasions where it really falls short even harder to spot. In the context of Ionic Angular this often happens with:

1. Native Plugins: In Ionic 4+ all native plugins have to be imported from `native-plugin/ngx`. Without the  `/ngx` part the code will fail to run
2. Plugins/Libs like `@ionic/storage`, the Storage will be imported from the place per default, this is also true for the file plugin, where the import is just `file`

These errors are often really hart to find, especially for beginners, due to one gets so used to Webstorm automatically picking the right import for you. Most often the time the imports are folded also and not a place where one searches for errors first.

Hope that helps someone!