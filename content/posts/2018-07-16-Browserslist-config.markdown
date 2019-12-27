---
layout: post
title:  "Browserslist config"
date:   2018-07-16
categories: ['web development']
tags: ['tool']
---

### Queries

Add `browserslist` key in `package.json`

```
{
  "browserslist": [
    "last 1 version",
    "> 1%",
    "maintained node versions",
    "not dead"
  ]
}
```

### Query Composition

| Query combiner type | Illustration | Example |
| ------------------- | :----------: | ------- |
|`or`/`,` combiner <br> (union) | ![Union of queries](https://raw.githubusercontent.com/browserslist/browserslist/master/img/union.svg?sanitize=true)  | `> .5% or last 2 versions` <br> `> .5%, last 2 versions` |
| `and` combiner <br> (intersection) | ![intersection of queries](https://raw.githubusercontent.com/browserslist/browserslist/master/img/intersection.svg?sanitize=true) | `> .5% and last 2 versions` |
| `not` combiner <br> (relative complement) | ![Relative complement of queries](https://raw.githubusercontent.com/browserslist/browserslist/master/img/complement.svg?sanitize=true) | `> .5% and not last 2 versions` <br> `> .5% or not last 2 versions` <br> `> .5%, not last 2 versions` |

> A quick way to test your query is to do `npx browserslist '> 0.5%, not IE 11'`
in your terminal.

### Full List

* `defaults`: Browserslist’s default browsers
  (`> 0.5%, last 2 versions, Firefox ESR, not dead`).
* `> 5%`: browsers versions selected by global usage statistics.
  `>=`, `<` and `<=` work too.
* `> 5% in US`: uses USA usage statistics. It accepts [two-letter country code].
* `> 5% in alt-AS`: uses Asia region usage statistics. List of all region codes
  can be found at [`caniuse-lite/data/regions`].
* `> 5% in my stats`: uses [custom usage data].
* `> 5% in browserslist-config-mycompany stats`: uses [custom usage data]
  from `browserslist-config-mycompany/browserslist-stats.json`.
* `cover 99.5%`: most popular browsers that provide coverage.
* `cover 99.5% in US`: same as above, with [two-letter country code].
* `cover 99.5% in my stats`: uses [custom usage data].
* `maintained node versions`: all Node.js versions, which are [still maintained]
  by Node.js Foundation.
* `node 10` and `node 10.4`: selects latest Node.js `10.x.x`
  or `10.4.x` release.
* `current node`: Node.js version used by Browserslist right now.
* `extends browserslist-config-mycompany`: take queries from
  `browserslist-config-mycompany` npm package.
* `ie 6-8`: selects an inclusive range of versions.
* `Firefox > 20`: versions of Firefox newer than 20.
  `>=`, `<` and `<=` work too. It also works with Node.js.
* `iOS 7`: the iOS browser version 7 directly.
* `Firefox ESR`: the latest [Firefox ESR] version.
* `PhantomJS 2.1` and `PhantomJS 1.9`: selects Safari versions similar
  to PhantomJS runtime.
* `unreleased versions` or `unreleased Chrome versions`:
  alpha and beta versions.
* `last 2 major versions` or `last 2 iOS major versions`:
  all minor/patch releases of last 2 major versions.
* `since 2015` or `last 2 years`: all versions released since year 2015
  (also `since 2015-03` and `since 2015-03-10`).
* `dead`: browsers without official support or updates for 24 months.
  Right now it is `IE 10`, `IE_Mob 10`, `BlackBerry 10`, `BlackBerry 7`,
  `Samsung 4` and `OperaMobile 12.1`.
* `last 2 versions`: the last 2 versions for *each* browser.
* `last 2 Chrome versions`: the last 2 versions of Chrome browser.
* `not ie <= 8`: exclude browsers selected by previous queries.

[`caniuse-lite/data/regions`]: https://github.com/ben-eb/caniuse-lite/tree/master/data/regions
[two-letter country code]:     https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements
[custom usage data]:           https://github.com/browserslist/browserslist#custom-usage-data
[still maintained]:            https://github.com/nodejs/Release

see more: [browserslist](https://github.com/browserslist/browserslist)
