This respository demonstrates an issue where the package-lock.json will change depending on whether you are using npm 10 or 11. 

This repo contains a single dependency

```
  "dependencies": {
    "@vue/apollo-composable": "^4.2.2"
  }
```

That package contains

`"@apollo/client"` as both a peer and a dev dependency. 

## Instructions 

Check the repo out. 

`npm -v`

If you are on `npm 10.x.x` already, do nothing. 

If you are on other versions of npm, switch to version 10.  

```
npm i -g npm@10
```  

Or how ever else you like to do it. 


```
npm i
git status
```

Observe no changes. 

Switch to npm 11 and repeat

```
npm i -g npm@11
npm i
git status
```

`git diff` shows

```diff
       "resolved": "https://registry.npmjs.org/@graphql-typed-document-node/core/-/core-3.2.0.tgz",
       "integrity": "sha512-mB9oAsNCm9aM3/SOv4YtBMqZbYj10R7dkq8byBqxGY/ncFwhf2oQzMV+LCRlWoDSEBJ3COiR1yeDvMtsoOsuFQ==",
       "license": "MIT",
-      "peer": true,
       "peerDependencies": {
         "graphql": "^0.8.0 || ^0.9.0 || ^0.10.0 || ^0.11.0 || ^0.12.0 || ^0.13.0 || ^14.0.0 || ^15.0.0 || ^16.0.0 || ^17.0.0"
       }
@@ -92,7 +91,6 @@
```

If you now switch back to npm 10, and re run `npm i` the change will be reversed. 

This suggests that it is not a 'rolling forward' kind of change. If you have some developers on 10 and some on 11, they will be constantly changing their package-lock files. 
