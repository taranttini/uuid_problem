-- THIS WORKS FOR ME
```
cd using_uuidv4@6.0.7/ && yarn install && yarn dev && cd ..
```
this uses `uuidv4@6.0.7` + `uuid@7.0.3`

and `uuid@7.0.3` files use module.exports

-- THIS DONT WORK FOR ME
```
cd using_uuidv4@6.0.8/ && yarn install && yarn dev && cd ..
```
this uses `uuidv4@6.0.8` + `uuid@8.0.0`

and `uuid@8.0.0` files don't use module.exports

But the error is created because ts-node-dev maybe depends module.exports

RESULT
```
Tarantini Pereira@WIN10 MSYS /d/sample (master)
$ cd uuidv4@6.0.7/ && yarn install && yarn dev && cd ..
yarn install v1.21.1
[1/4] Resolving packages...
[2/4] Fetching packages...
[3/4] Linking dependencies...
[4/4] Building fresh packages...

success Saved lockfile.
Done in 3.10s.
yarn run v1.21.1
$ ts-node-dev sample.ts
Using ts-node version 8.10.1, typescript version 3.8.3
Done in 0.88s.

Tarantini Pereira@WIN10 MSYS /d/sample (master)
$ cd using_uuidv4@6.0.8/ && yarn install && yarn dev && cd ..
yarn install v1.21.1
[1/4] Resolving packages...
success Already up-to-date.
Done in 0.27s.
yarn run v1.21.1
$ ts-node-dev sample.ts
Using ts-node version 8.10.1, typescript version 3.8.3
Error: No valid exports main found for 'D:\sample\using_uuidv4@6.0.8\node_modules\uuid'
    at resolveExportsTarget (internal/modules/cjs/loader.js:622:9)
    at applyExports (internal/modules/cjs/loader.js:499:14)
    at resolveExports (internal/modules/cjs/loader.js:548:12)
    at Function.Module._findPath (internal/modules/cjs/loader.js:654:22)
    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:953:27)
    at Function.Module._load (internal/modules/cjs/loader.js:859:27)
    at Module.require (internal/modules/cjs/loader.js:1028:19)
    at require (internal/modules/cjs/helpers.js:72:18)
    at Object.<anonymous> (D:\sample\using_uuidv4@6.0.8\node_modules\uuidv4\build\lib\uuidv4.js:3:16)
    at Module._compile (internal/modules/cjs/loader.js:1139:30)
[ERROR] 04:17:07 Error: No valid exports main found for 'D:\sample\using_uuidv4@6.0.8\node_modules\uuid'
```

```
cat using_uuidv4\@6.0.7/node_modules/uuid/dist/v4.js

ENDs

var _default = v4;
exports.default = _default;
module.exports = exports.default;
```

```
cat using_uuidv4\@6.0.8/node_modules/uuid/dist/v4.js

ENDs

var _default = v4;
exports.default = _default;
```