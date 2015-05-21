'use strict';

var fs = require('graceful-fs');
var path = require('path');
var Parser = require('./stream');

var defaultRecords = ['GUID', 'Slug', 'ModTime', 'Sequence'];

/**
 * A convience wrapper around the streaming parser to allow for a simplier
 * interface
 * @param  {string} fn filename
 * @param  {string[]} records what records you're interested in from the main file
 * @param  {string[]} rundownRecords if you've got a rundown, these keys will come back
 * @param  {Function} cb calls back with err, record
 * @return {stream} returns a stream
 */
function enps(fn, records, rundownRecords, cb) {
  if (typeof rundownRecords === 'function') {
    cb = rundownRecords;
    rundownRecords = undefined;
  }

  if (typeof records === 'function') {
    cb = records;
    records = [];
  }

  records = defaultRecords.concat(records);

  var collector = {};
  var enpsParser = new Parser();

  enpsParser.on('record', function(key, val) {
    if (records.indexOf(key) > -1) {
      collector[key] = val;
    }
  });

  return fs.createReadStream(fn)
    .on('error', function(err) {
      cb(err);
    })
    .on('close', function(){
      var count = 0;
      if (Array.isArray(rundownRecords) && collector.Sequence) {
        collector.Sequence.forEach(function(seq) {
          var rowFn = path.join(path.dirname(fn), ['R', collector.GUID].join('_'));
          collector.rows = {};
          rundownRecords = defaultRecords.concat(rundownRecords);
          enps(rowFn, rundownRecords, function(err, sequenceData) {
            ++count;
            collector.rows[seq] = sequenceData;
            if (count === collector.Sequence.length) {
              cb(null, collector);
            }
          });
        });
      } else {
        cb(null, collector);
      }
    })
    .pipe(enpsParser)
    .resume();
}

module.exports = enps;
exports.Parser = Parser;
