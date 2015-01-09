# chronic 

*adjective*: from Greek *khronikos* ‘of time,’ from *khronos* ‘time.’

[![NPM](https://nodei.co/npm/chronic.png)](https://nodei.co/npm/chronic/)

[![Build Status](https://img.shields.io/travis/codingalchemy/chronic.svg?style=flat-square)](https://travis-ci.org/codingalchemy/chronic)
[![Dependency Status](https://img.shields.io/david/codingalchemy/chronic.svg?style=flat-square)](https://david-dm.org/codingalchemy/chronic)
[![Stability Status](https://img.shields.io/badge/stability-unstable-orange.svg?style=flat-square)](https://github.com/dominictarr/stability#experimental)

```bash
npm install chronic --save-dev
```

## Background

This library is built on top of azer's [bud](https://github.com/azer/bud) and gulp's [vinyl-fs](https://github.com/wearefractal/vinyl-fs). Rationale for this project can be found [here](https://github.com/codingalchemy/chronic/blob/master/RATIONALE.md).
*The API internals of this libary are very much in flux and subject to change*


## Usage

``` js
var chron = require('chronic');

chron('first task', chron.src('./one/**').dest('./two'), chron.build)

chron('another task', chron.once('first task'). function(t) {
  t.build(t.src('./two/**'), t.dest('./three'));
});

chron('default', chron.once('another task'), function(t) {
  t.done();
});


```

## API

### chronic(task, opts, [func])

- `task` a string, works similarly to `gulp.task('task', function(..))`. Used to name tasks. 
- `opts` a chainable series chronic methods. 
- `func` a function that contains the paramater `t`

#### opts:

- `chronic.once` a comma separated list of strings (tasks). 
  - a list of tasks which should be *run and completed* prior to this task starting
- `chronic.path` a glob of string(s), either in an array or commma separated. 
  - Passed down to `t.src('path')` and `t.files`
- `chronic.watch` a glob of string(s), either in an array or commma separated. 
  - Passed down to `t.watching` and `t.files`
- `chronic.transform` a comma separated list of functions that are stream transforms. 
  - this should only be used with both `chronic.path` and `chronic.dest`
  - these functions are piped inbetween path and dest using [pump](https://github.com/mafintosh/pump).
  - only gulp-plugins can safely be used at the moment 
- `chronic.dest` a string which is passed down to `t.dest('path')`.

#### t:



## License

MIT