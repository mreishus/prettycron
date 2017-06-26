# prettyCron [![Build Status](https://travis-ci.org/azza-bazoo/prettycron.svg?branch=master)](https://travis-ci.org/azza-bazoo/prettycron)

prettyCron is a simple JavaScript deuglifier for cron schedules: it prints out a human-readable interpretation of when the schedule will run.

## Notes about this fork

I wanted to use this library in my project using webpack 3 and react, however I couldn't.   After installing prettycron from npm, the project refused to build.

Prettycron uses `later`, a package that has been abandonded and has a problem preventing it from compiling in webpack 2 or 3.   Here is the issue link: https://github.com/bunkat/later/issues/155 .  Some people have contributed workarounds in that thread, but I wasn't able to get them to work.  I suspect it's because in my project I was not using later directly, rather it was a dependency of a dependency.

One person created a forked version of later which fixes the webpack problem.   So, I forked prettyCron and changed its dependency to point at the forked version of later.

Now I'm easily able to use prettyCron.  My package.json file has
```
    "prettycron": "mreishus/prettycron",
```

And using
```
import prettyCron from 'prettycron';
```

"just works".

A better long-term solution might be to fork both `later` and `prettyCron`, fix the problems, and then publish them under npm with different names.

BTW, the npm version of prettyCron is also not the latest version.  So you'll fix two issues with one stone by using this fork. :)

Note that this fork was created on 6/26/17.  I don't plan to update it unless I have an immediate need to.

## For examples...

... [check out the project home page](http://azza-bazoo.github.io/prettycron/).


## Installation - browser

Include prettycron.js after adding [moment.js](http://momentjs.com/) and [later.js](https://github.com/bunkat/later).

```html
<script src="moment.min.js" type="text/javascript"></script>
<script src="later.min.js" type="text/javascript"></script>
<script src="prettycron.js" type="text/javascript"></script>
```


## Installation - Node

Simply use `npm` and `require`:

```
$ npm install prettycron
```

```js
var prettyCron = require('prettycron');
```


## Usage

prettyCron exposes two methods, both of which take a cron specification as the only argument.

### prettyCron.toString(cron)

Returns a human-readable sentence describing all the times this cron will run.

```js
prettyCron.toString("37 10 * * * *");
// returns "10:37 every day"
```

### prettyCron.getNext(cron)

Returns a string representing the next time this cron will run, formatted with moment's [calendar()](http://momentjs.com/docs/#/displaying/calendar-time/) method.

```js
prettyCron.getNext("0 * * * *");
// if current time is 4:45pm, then returns "Today at 5:00 PM"
```

### prettyCron.getNextDates(cron, numDates)

Returns an array of strings representing the next (numDates) amount of times this cron will run, formatted with moment's [calendar()](http://momentjs.com/docs/#/displaying/calendar-time/) method.

```js
prettyCron.getNextDates("0 * * * *", 4);
// If current time is 3.45 PM, then returns [ 'Today at 4:00 PM', 'Today at 5:00 PM', 'Today at 6:00 PM', 'Today at 7:00 PM' ]
```

## Credits

prettyCron was [originally written](http://dsysadm.blogspot.com.au/2012/09/human-readable-cron-expressions-using.html) by [dunse](https://github.com/dunse) and posted to [gist](https://gist.github.com/dunse/3714957). This version is by [Hourann Bosci](http://hourann.com/) with contributions from [Johan Andersson](https://github.com/anderssonjohan), [Phil Jepsen](https://github.com/wired8), [Andre Buchanan](https://github.com/andrebuchanan), and [Anton Petrov](https://github.com/itsmepetrov).

It's licensed under [LGPLv3](http://www.gnu.org/copyleft/lesser.html).
