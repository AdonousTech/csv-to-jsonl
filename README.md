# csv-to-jsonl
small csv to json-lines parser with no dependencies

### Run as a shell script
install globally:
```
npm install -g csv-2-jsonl
```
run script with input file and optional output file path:
```
csv2jsonl path/to/csv [output/filepath]
```

### Use in your Node application
install locally:
```
npm install -s csv-2-jsonl
```
require into your Node file:
```javascript
const csvToJsonl = require('csv-2-jsonl');
const { createReadStream, createWriteStream } = require('fs');

const readable = createReadStream('/Users/gabriel/macondo_residents.csv');
const writable = createWriteStream('/Users/gabriel/macondo_residents.jsonl');
csvToJsonl({ inputStream: readable, outputStream: writable });
```
The exported function also returns a readable stream, so you do not need to supply your own output stream and can instead pipe directly from the returned value:
```javascript
const readable = createReadStream('/Users/toni/macon_dead_holdings.csv');
csvToJsonl({ inputStream: readable })
  .pipe(someOtherTransformStream)
  .pipe(someOtherWritableStream);
```
Alternatively, the exported function can return a promise if the `returnPromise` flag is enabled. Note that this flag has no effect if no `outputStream` argument is supplied.
```javascript
csvToJsonl({
  inputStream: readable,
  outputStream: writable,
  returnPromise: true,
})
  .then(() => console.log('done converting!'));
```