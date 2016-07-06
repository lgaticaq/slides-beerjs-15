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

# Solucionar el Callback Hell y de pasadita mejorar el performance

--

## Callback Hell

```javascript
                        const list = (req, res, next) => {
                          Ticket.findAllManual((err, manual) => {
                            if (err) return next(err);
                            Ticket.findAllPaymentsWebpay((err, webpay) => {
                              if (err) return next(err);
                              Ticket.findAllPaymentsTransfer((err, transfer) => {
                                if (err) return next(err);
                                res.render('ticket/all', {
                                  manual: manual,
                                  webpay: webpay,
                                  transfer: transfer
                                });
                              });
                            });
                          });
                        }
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
geocoder.geocode(address).then(results => {
  const coords = `${results[0].latitude},${results[0].longitude}`;
  return w3w.reverse({coords: coords, lang: LANG});
})
  .then(response => res.send(response))
  .catch(err => res.reply('an error occurred')

const promises = [promise1(), promise2(), promise3()];
Promise.all(promises).then(results => console.log(results[0]));
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
const login = function *() {
  try {
    const account = yield db.Account.find({
      email: req.body.email,
      password: req.body.password
    });
    account.statistics = yield account.getAccountStatistics(account);
    yield account.incrementAccountLoginCount(account);
    this.body = account;
  } catch (err) {
    return res.status(500).send(err);
  }
};
```

--

## async/awit (ES7)

```javascript
const login = async function() {
  try {
    const account = await db.Account.find({
      email: req.body.email,
      password: req.body.password
    });
    account.statistics = await account.getAccountStatistics(account);
    await account.incrementAccountLoginCount(account);
    this.body = account;
  } catch (err) {
    return res.status(500).send(err);
  }
};
```
