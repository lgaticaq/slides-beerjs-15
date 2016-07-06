title: Beerjs #15
author:
  name: Leonardo Gatica
  twitter: lgaticaq
  url: https://about.me/lgatica
  email: lgatica@protonmail.com
output: index.html
theme: juanbrujo/cleaver-beerjs
style: style.css
controls: false

--

# Callback Hell, Async, Promise, Generators y Async/Await

--

## Callback Hell

```javascript
                        const myUglyFunction = cb => {
                          someFunction1((err, data1) => {
                            if (err) return cb(err);
                            someFunction2((err, data2) => {
                              if (err) return cb(err);
                              someFunction3((err, data3) => {
                                if (err) return cb(err);
                                someFunction4((err, data4) => {
                                  if (err) return cb(err);
                                  cb(null, data1 + data2 + data3 + data4);
                                });
                              });
                            });
                          });
                        };
```

--

## Async

```bash
npm i -S async
```

```javascript
import {map, filter, waterfall, parallel, series} from 'async';

map(['file1', 'file2', 'file3'], fs.stat, callback);
filter(['file1', 'file2', 'file3'], fs.exists, callback);
waterfall([
  callback => (null, 'one', 'two'),
  (arg1, arg2, callback) => callback(null, 'three'),
  (arg1, callback) => callback(null, 'done')
], callback);
parallel([function1, function2], callback);
series([function1, function2], callback);
```

--

## Promises (ES6)

```javascript
promise1().then(data1 => promise2(data1))
  .then(data2 => promise3(data2))
  .then(result => console.log(result))
  .catch(err => console.err(err))
```

```javascript
const myPromise = filename => {
  return new Promise((resolve, reject) => {
    fs.stat(filename, (err, result) => {
      if (err) reject(err);
      resolve(result);
    });
  });
};
```

--

## Bluebird

```bash
npm i -S bluebird
```

```javascript
import fs from 'fs';
import bluebird from 'bluebird';

bluebird.promisifyAll(fs);

fs.readFileAsync('file.js', 'utf8').then(...)
```

--

## Generators (ES6)

```javascript

const r = require('rethinkdbdash')();

function *() {
  try {
    yield r.dbCreate('quake').run();
    yield r.db('quake').tableCreate('quakes').run();
    yield r.db('quake').table('quakes')
      .indexCreate('geometry', {geo: true}).run();
    yield r.db('quake').table('quakes')
      .insert(r.http(feedUrl)('features')).run();
  } catch (err) {
    console.error(err);
  }
};
```

--

## async/awit (ES7)

```javascript

async function() {
  try {
    await r.dbCreate('quake').run();
    await r.db('quake').tableCreate('quakes').run();
    await r.db('quake').table('quakes')
      .indexCreate('geometry', {geo: true}).run();
    await r.db('quake').table('quakes')
      .insert(r.http(feedUrl)('features')).run();
  } catch (err) {
    console.error(err);
  }
}
```
