# Node.js 500+ Examples

A massive collection of **500+ practical Node.js examples**, covering everything from basic concepts and core modules to advanced topics, real-time applications, databases, and practical projects.  
Perfect for learners, teachers, and professionals. Contributions welcome!

**Current Progress:** 60/500 examples completed ✅

---

## Table of Contents

1. [Basic Concepts & Core Modules](#1-basic-concepts--core-modules)  
2. [Asynchronous Programming](#2-asynchronous-programming)  
3. [Web Development with Express.js](#3-web-development-with-expressjs)  
4. [Databases](#4-databases)  
5. [Real-time Applications](#5-real-time-applications)  
6. [Advanced Topics](#6-advanced-topics)  
7. [Practical Projects & Utilities](#7-practical-projects--utilities)  
8. [Contribution Guide](#8-contribution-guide)  

---

## 1. Basic Concepts & Core Modules (≈50 Examples)

<details>
<summary>Hello World Examples</summary>

```js
// Example 1: Basic HTTP Server
const http = require('http');
const server = http.createServer((req, res) => {
  res.end('Hello World');
});
server.listen(3000, () => console.log('Server running on port 3000'));
```

</details>

<details>
<summary>File System (fs)</summary>

```js
// Example 2: Read file asynchronously
const fs = require('fs');
fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

</details>

<details>
<summary>Path Module</summary>

```js
// Example 3: Join paths
const path = require('path');
const fullPath = path.join(__dirname, 'folder', 'file.txt');
console.log(fullPath);
```

</details>

<!-- Add remaining 47 examples similarly -->


<details>
<summary>OS Module</summary>

```js
// Example 4: System info
const os = require('os');
console.log('CPU architecture:', os.arch());
console.log('Free memory (MB):', os.freemem() / 1024 / 1024);
console.log('Platform:', os.platform());
```
</details>

<details>
<summary>Process Info</summary>

```js
// Example 5: Access process details
console.log('PID:', process.pid);
console.log('Node Version:', process.version);
console.log('Uptime (s):', process.uptime());
```
</details>

<details>
<summary>Environment Variables</summary>

```js
// Example 6: Reading environment variables
process.env.MY_APP_MODE = 'development';
console.log('Mode:', process.env.MY_APP_MODE);
```
</details>

<details>
<summary>Console Utilities</summary>

```js
// Example 7: console methods
console.time('Timer');
console.log('Hello Console!');
console.warn('Warning message');
console.error('Error message');
console.timeEnd('Timer');
```
</details>

<details>
<summary>URL Module</summary>

```js
// Example 8: Parse and format URLs
const { URL } = require('url');
const myURL = new URL('https://example.com/path?name=alice');
console.log(myURL.hostname, myURL.searchParams.get('name'));
```
</details>

<details>
<summary>Events Emitter</summary>

```js
// Example 9: Custom event
const EventEmitter = require('events');
const emitter = new EventEmitter();
emitter.on('greet', name => console.log(`Hello, ${name}`));
emitter.emit('greet', 'Node.js');
```
</details>

<details>
<summary>Timers</summary>

```js
// Example 10: setInterval & clearInterval
let count = 0;
const id = setInterval(() => {
  console.log('Tick', ++count);
  if (count === 5) clearInterval(id);
}, 1000);
```
</details>

<details>
<summary>Crypto Hash</summary>

```js
// Example 11: SHA256 hash
const crypto = require('crypto');
const hash = crypto.createHash('sha256').update('Hello').digest('hex');
console.log(hash);
```
</details>

<details>
<summary>HTTP GET Request (native)</summary>

```js
// Example 12: Simple HTTP client
const https = require('https');
https.get('https://api.github.com', { headers: { 'User-Agent': 'node' } }, res => {
  console.log('Status:', res.statusCode);
});
```
</details>

<details>
<summary>Zlib Compression</summary>

```js
// Example 13: Gzip a file
const fs = require('fs');
const zlib = require('zlib');
fs.createReadStream('input.txt')
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream('input.txt.gz'));
```
</details>

<details>
<summary>Stream Transform</summary>

```js
// Example 14: Uppercase transform stream
const { Transform } = require('stream');
const upper = new Transform({
  transform(chunk, enc, cb) {
    cb(null, chunk.toString().toUpperCase());
  }
});
process.stdin.pipe(upper).pipe(process.stdout);
```
</details>

<details>
<summary>Readline Interface</summary>

```js
// Example 15: Simple CLI prompt
const readline = require('readline').createInterface({
  input: process.stdin,
  output: process.stdout
});
readline.question('Your name? ', name => {
  console.log(`Hello, ${name}!`);
  readline.close();
});
```
</details>

<details>
<summary>Child Process Exec</summary>

```js
// Example 16: Run shell command
const { exec } = require('child_process');
exec('ls -lh', (err, stdout) => {
  if (err) return console.error(err);
  console.log(stdout);
});
```
</details>

<details>
<summary>Cluster Basic</summary>

```js
// Example 17: Fork worker processes
const cluster = require('cluster');
const http = require('http');
const os = require('os');
if (cluster.isPrimary) {
  os.cpus().forEach(() => cluster.fork());
} else {
  http.createServer((_, res) => res.end('Hello from worker')).listen(3000);
}
```
</details>

<details>
<summary>DNS Lookup</summary>

```js
// Example 18: Resolve a domain
const dns = require('dns');
dns.lookup('example.com', (err, address) => {
  if (err) throw err;
  console.log('IP address:', address);
});
```
</details>

[Return to Table of Contents](#table-of-contents)
---

## 2. Asynchronous Programming (≈50 Examples)

<details>
<summary>1. setTimeout Basic</summary>

```js
setTimeout(() => console.log('Hello after 1s'), 1000);
```
</details>

<details>
<summary>2. setInterval Counter</summary>

```js
let i = 0;
const id = setInterval(() => {
  console.log(++i);
  if(i===5) clearInterval(id);
}, 500);
```
</details>

<details>
<summary>3. setImmediate</summary>

```js
setImmediate(() => console.log('Runs after current loop'));
```
</details>

<details>
<summary>4. process.nextTick</summary>

```js
process.nextTick(() => console.log('Next tick callback'));
```
</details>

<details>
<summary>5. Callback Example</summary>

```js
function add(a,b,cb){ cb(a+b); }
add(2,3,res=>console.log(res));
```
</details>

<details>
<summary>6. Callback Error Handling</summary>

```js
function risky(cb){
  try { throw new Error('fail'); }
  catch(e){ cb(e); }
}
risky(err => err && console.error(err.message));
```
</details>

<details>
<summary>7. Promise Basic</summary>

```js
new Promise(res=>res('Done')).then(console.log);
```
</details>

<details>
<summary>8. Promise Chain</summary>

```js
Promise.resolve(2).then(x=>x*3).then(console.log);
```
</details>

<details>
<summary>9. Promise.all</summary>

```js
Promise.all([Promise.resolve(1),Promise.resolve(2)]).then(console.log);
```
</details>

<details>
<summary>10. Promise.race</summary>

```js
Promise.race([
  new Promise(r=>setTimeout(()=>r('fast'),100)),
  new Promise(r=>setTimeout(()=>r('slow'),500))
]).then(console.log);
```
</details>

<details>
<summary>11. Async/Await</summary>

```js
(async () => {
  const v = await Promise.resolve('Awaited');
  console.log(v);
})();
```
</details>

<details>
<summary>12. Async Error Handling</summary>

```js
(async ()=>{
  try{ await Promise.reject('Fail'); }
  catch(e){ console.error(e); }
})();
```
</details>

<details>
<summary>13. fs.promises</summary>

```js
const fs = require('fs').promises;
(async ()=>{
  const txt = await fs.readFile('file.txt','utf8');
  console.log(txt);
})();
```
</details>

<details>
<summary>14. util.promisify</summary>

```js
const {promisify} = require('util');
const readFile = promisify(require('fs').readFile);
readFile('file.txt','utf8').then(console.log);
```
</details>

<details>
<summary>15. Delay Function</summary>

```js
const delay = ms => new Promise(r=>setTimeout(r,ms));
delay(500).then(()=>console.log('Done'));
```
</details>

<details>
<summary>16. Parallel Tasks</summary>

```js
async function run() {
  const [a,b] = await Promise.all([delay(100), delay(200)]);
  console.log('parallel done');
}
run();
```
</details>

<details>
<summary>17. Sequential Tasks</summary>

```js
async function run() {
  await delay(100);
  await delay(200);
  console.log('sequential done');
}
run();
```
</details>

<details>
<summary>18. Async Map</summary>

```js
async function asyncMap(arr, fn){
  return Promise.all(arr.map(fn));
}
asyncMap([1,2], async x=>x*2).then(console.log);
```
</details>

<details>
<summary>19. Retry Logic</summary>

```js
async function retry(fn, n=3){
  for(let i=0;i<n;i++){
    try{return await fn();}
    catch(e){ if(i===n-1) throw e; }
  }
}
```
</details>

<details>
<summary>20. Race with Timeout</summary>

```js
function withTimeout(p, ms){
  const t = new Promise((_,rej)=>setTimeout(()=>rej('Timeout'), ms));
  return Promise.race([p,t]);
}
```
</details>

<details>
<summary>21. EventEmitter Async</summary>

```js
const {EventEmitter} = require('events');
const em = new EventEmitter();
em.on('data', async d => console.log(await Promise.resolve(d)));
em.emit('data','Hello');
```
</details>

<details>
<summary>22. Stream Async Iteration</summary>

```js
const fs = require('fs');
(async ()=>{
  for await(const chunk of fs.createReadStream('file.txt')){
    console.log(chunk.toString());
  }
})();
```
</details>

<details>
<summary>23. Worker Threads</summary>

```js
const { Worker } = require('worker_threads');
new Worker('console.log("worker")',{eval:true});
```
</details>

<details>
<summary>24. Timers Promises</summary>

```js
const { setTimeout } = require('timers/promises');
await setTimeout(500);
console.log('done');
```
</details>

<details>
<summary>25. Async Generator</summary>

```js
async function* gen(){
  yield await Promise.resolve(1);
  yield 2;
}
for await(const x of gen()) console.log(x);
```
</details>

<details>
<summary>26. Pipeline Promises</summary>

```js
const {pipeline} = require('stream/promises');
await pipeline(fs.createReadStream('a.txt'), fs.createWriteStream('b.txt'));
```
</details>

<details>
<summary>27. callbackify</summary>

```js
const {callbackify} = require('util');
const fn = async ()=>'done';
callbackify(fn)((err,res)=>console.log(res));
```
</details>

<details>
<summary>28. AbortController</summary>

```js
const controller = new AbortController();
fetch('https://example.com',{signal:controller.signal});
controller.abort();
```
</details>

<details>
<summary>29. Semaphore</summary>

```js
class Semaphore {
  constructor(n){this.n=n; this.q=[];}
  async acquire(){
    if(this.n>0){this.n--; return;}
    await new Promise(r=>this.q.push(r));
  }
  release(){
    this.n++;
    if(this.q.length) this.q.shift()();
  }
}
```
</details>

<details>
<summary>30. Async Queue with setTimeout</summary>

```js
const tasks=[1,2,3];
function runQueue(){
  if(!tasks.length) return;
  console.log(tasks.shift());
  setTimeout(runQueue,200);
}
runQueue();
```
</details>

<!-- Add remaining async examples -->

[Return to Table of Contents](#table-of-contents)
---

## 3. Web Development with Express.js (≈80 Examples)

<details>
<summary>Simple Express Server</summary>

```js
// Example 1: Basic Express app
const express = require('express');
const app = express();
app.get('/', (req, res) => res.send('Hello Express!'));
app.listen(3000, () => console.log('Server running on port 3000'));
```

</details>

<details>
<summary>Routing</summary>

```js
// Example 2: Dynamic route
app.get('/user/:id', (req, res) => {
  res.send(`User ID: ${req.params.id}`);
});
```

</details>

<!-- Add remaining Express examples -->

[Return to Table of Contents](#table-of-contents)
---

## 4. Databases (≈50 Examples)

<details>
<summary>MongoDB with Mongoose</summary>

```js
// Example 1: Connect to MongoDB
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:27017/mydb');
```

</details>

<details>
<summary>PostgreSQL (pg)</summary>

```js
// Example 2: Simple query
const { Client } = require('pg');
const client = new Client();
await client.connect();
const res = await client.query('SELECT NOW()');
console.log(res.rows[0]);
```

</details>

<!-- Add MySQL and other DB examples -->

[Return to Table of Contents](#table-of-contents)
---

## 5. Real-time Applications (≈40 Examples)

<details>
<summary>WebSocket with Socket.IO</summary>

```js
// Example: Simple chat server
const io = require('socket.io')(3000);
io.on('connection', socket => {
  socket.on('message', msg => io.emit('message', msg));
});
```

</details>

<details>
<summary>Server-Sent Events (SSE)</summary>

```js
// Example: SSE endpoint
app.get('/events', (req, res) => {
  res.setHeader('Content-Type', 'text/event-stream');
  setInterval(() => res.write(`data: ${new Date()}\n\n`), 1000);
});
```

</details>

[Return to Table of Contents](#table-of-contents)
---

## 6. Advanced Topics (≈60 Examples)

<details>
<summary>Clustering</summary>

```js
// Example: Basic cluster setup
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
  for (let i = 0; i < numCPUs; i++) cluster.fork();
} else {
  http.createServer((req, res) => res.end('Hello from worker')).listen(3000);
}
```

</details>

<details>
<summary>Child Processes</summary>

```js
// Example: Spawn child process
const { spawn } = require('child_process');
const ls = spawn('ls', ['-lh']);
ls.stdout.on('data', data => console.log(`Output: ${data}`));
```

</details>

<!-- Add remaining advanced examples -->

[Return to Table of Contents](#table-of-contents)
---

## 7. Practical Projects & Utilities (≈100+ Examples)

<details>
<summary>Command Line Tool</summary>

```js
// Example: Simple CLI
const args = process.argv.slice(2);
console.log(`Hello ${args[0] || 'World'}`);
```

</details>

<details>
<summary>Email Sender</summary>

```js
// Example: Send email with Nodemailer
const nodemailer = require('nodemailer');
const transporter = nodemailer.createTransport({ /* config */ });
transporter.sendMail({ from:'you@domain.com', to:'user@domain.com', subject:'Test', text:'Hello' });
```

</details>

<!-- Add remaining project examples -->

[Return to Table of Contents](#table-of-contents)
---

## 8. Contribution Guide

We welcome contributions! To add new examples:  

1. Fork the repository.  
2. Follow the **example template**:

```markdown
## Example Title

**Category:** <Basic/Async/Web/DB/Real-time/etc.>  
**Description:** <Short description>  

```js
// Your code here
```

**Notes:** <Optional explanation>
```

3. Submit a pull request.  

> **Keep examples small, well-commented, and tested.**

[Return to Table of Contents](#table-of-contents)
---

## 9. Roadmap

- Add advanced DB queries (transactions, joins, indexing)  
- Add caching examples (Redis, memory cache)  
- Add microservice examples and API integrations  
- Add testing patterns and CI/CD workflows  

```}
