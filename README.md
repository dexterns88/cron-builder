# cron-builder
A simple JavaScript module for building cron expressions.

### Install
cron-builder is available on npm and bower:
```
npm install cron-builder --save
```
or
```
bower install cron-builder --save
```

After installing, just require the package as you normally would:
```
var cb = require('/path/to/cron-builder.js');
```



### API
To instantiate the cron builder:

```JavaScript
// (default expression is set to "* * * * * *")
var cronExp = new cb();

// optionally, pass in a cron expression to override the default:
var myCronExp = new cb('5 12 * * 1-5 *')
```

To return the cron expression at any given time:
```JavaScript
cronExp.build();
// '* * * * * *'
```

API includes basic getters and setters:
```JavaScript
cronExp.get('minute');
// '*'
cronExp.set('5,35', 'minute');
// '5,35'
cronExp.get('minute');
// '5,35'
cronExp.build();
// '5,35 * * * * *'
```

Add or remove values one at a time:
```JavaScript
cronExp.addValue('2', 'hour');
cronExp.addValue('4', 'monthOfTheYear');
cronExp.addValue('10', 'monthOfTheYear');
cronExp.build();
// '5,35 2 * 4,10 * *'

cronExp.removeValue('5', 'minute');
cronExp.build();
// '35 2 * 4,10 * *'
```

If you prefer to work with the expression object directly, use `getAll` and `setAll`:
```JavaScript
var exp = cronExp.getAll();
// {minute: ['35'], hour: ['2'], dayOfTheMonth: ['*'], monthOfTheYear: ['4','10'], ...}
exp.dayOfTheMonth = ['7','14','21','28'];
cronExp.setAll(exp);
cronExp.build();
// '35 2 7,14,21,28 4,10 * *'
```

##### Notes:
- cron-builder does not currently support using `/` syntax to indicate values that are repeated. Instead of using `*/15`, use the verbose form `0,15,30,45`.
- cron-builder requires using numeric representations of days of the week and months of the year. So instead of using `Feb,Mar,Apr` just use `2,3,4`.

##### License

The MIT License (MIT)

Copyright (c) 2015 Tyler Waneka

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.