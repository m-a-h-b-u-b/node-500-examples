# Node.js 500+ Examples

A massive collection of **500+ practical Node.js examples**, covering everything from basic concepts and core modules to advanced topics, real-time applications, databases, and practical projects.  
Perfect for learners, teachers, and professionals. Contributions welcome!

**Current Progress:** 72/500 examples completed ✅

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

<a id="1-basic-concepts--core-modules"></a>
## 1. Basic Concepts & Core Modules (≈50 Examples)

<details>
<summary>1.1 Hello World Examples</summary>

```js
const http = require('http');
const server = http.createServer((req, res) => {
  res.end('Hello World');
});
server.listen(3000, () => console.log('Server running on port 3000'));
```

</details>

<details>
<summary>1.2 File System (fs)</summary>

```js
const fs = require('fs');
fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

</details>

<details>
<summary>1.3 Path Module</summary>

```js
const path = require('path');
const fullPath = path.join(__dirname, 'folder', 'file.txt');
console.log(fullPath);
```

</details>

<!-- Add remaining 47 examples similarly -->


<details>
<summary>1.4 OS Module</summary>

```js
const os = require('os');
console.log('CPU architecture:', os.arch());
console.log('Free memory (MB):', os.freemem() / 1024 / 1024);
console.log('Platform:', os.platform());
```
</details>

<details>
<summary>1.5 Process Info</summary>

```js
console.log('PID:', process.pid);
console.log('Node Version:', process.version);
console.log('Uptime (s):', process.uptime());
```
</details>

<details>
<summary>1.6 Environment Variables</summary>

```js
process.env.MY_APP_MODE = 'development';
console.log('Mode:', process.env.MY_APP_MODE);
```
</details>

<details>
<summary>1.7 Console Utilities</summary>

```js
console.time('Timer');
console.log('Hello Console!');
console.warn('Warning message');
console.error('Error message');
console.timeEnd('Timer');
```
</details>

<details>
<summary>1.8 URL Module</summary>

```js
// Example 8: Parse and format URLs
const { URL } = require('url');
const myURL = new URL('https://example.com/path?name=alice');
console.log(myURL.hostname, myURL.searchParams.get('name'));
```
</details>

<details>
<summary>1.9 Events Emitter</summary>

```js
const EventEmitter = require('events');
const emitter = new EventEmitter();
emitter.on('greet', name => console.log(`Hello, ${name}`));
emitter.emit('greet', 'Node.js');
```
</details>

<details>
<summary>1.10 Timers</summary>

```js
let count = 0;
const id = setInterval(() => {
  console.log('Tick', ++count);
  if (count === 5) clearInterval(id);
}, 1000);
```
</details>

<details>
<summary>1.11 Crypto Hash</summary>

```js
const crypto = require('crypto');
const hash = crypto.createHash('sha256').update('Hello').digest('hex');
console.log(hash);
```
</details>

<details>
<summary>1.12 HTTP GET Request (native)</summary>

```js
const https = require('https');
https.get('https://api.github.com', { headers: { 'User-Agent': 'node' } }, res => {
  console.log('Status:', res.statusCode);
});
```
</details>

<details>
<summary>1.13 Zlib Compression</summary>

```js
const fs = require('fs');
const zlib = require('zlib');
fs.createReadStream('input.txt')
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream('input.txt.gz'));
```
</details>

<details>
<summary>1.14 Stream Transform</summary>

```js
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
<summary>1.15 Readline Interface</summary>

```js
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
<summary>1.16 Child Process Exec</summary>

```js
const { exec } = require('child_process');
exec('ls -lh', (err, stdout) => {
  if (err) return console.error(err);
  console.log(stdout);
});
```
</details>

<details>
<summary>1.17 Cluster Basic</summary>

```js
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
<summary>1.18 DNS Lookup</summary>

```js
const dns = require('dns');
dns.lookup('example.com', (err, address) => {
  if (err) throw err;
  console.log('IP address:', address);
});
```
</details>

[Return to Table of Contents](#table-of-contents)
---

<a id="2-asynchronous-programming"></a>
## 2. Asynchronous Programming (≈50 Examples)

<details>
<summary>2.1 setTimeout Basic</summary>

```js
setTimeout(() => console.log('Hello after 1s'), 1000);
```
</details>

<details>
<summary>2.2 setInterval Counter</summary>

```js
let i = 0;
const id = setInterval(() => {
  console.log(++i);
  if(i===5) clearInterval(id);
}, 500);
```
</details>

<details>
<summary>2.3 setImmediate</summary>

```js
setImmediate(() => console.log('Runs after current loop'));
```
</details>

<details>
<summary>2.4 process.nextTick</summary>

```js
process.nextTick(() => console.log('Next tick callback'));
```
</details>

<details>
<summary>2.5 Callback Example</summary>

```js
function add(a,b,cb){ cb(a+b); }
add(2,3,res=>console.log(res));
```
</details>

<details>
<summary>2.6 Callback Error Handling</summary>

```js
function risky(cb){
  try { throw new Error('fail'); }
  catch(e){ cb(e); }
}
risky(err => err && console.error(err.message));
```
</details>

<details>
<summary>2.7 Promise Basic</summary>

```js
new Promise(res=>res('Done')).then(console.log);
```
</details>

<details>
<summary>2.8 Promise Chain</summary>

```js
Promise.resolve(2).then(x=>x*3).then(console.log);
```
</details>

<details>
<summary>2.9 Promise.all</summary>

```js
Promise.all([Promise.resolve(1),Promise.resolve(2)]).then(console.log);
```
</details>

<details>
<summary>2.10 Promise.race</summary>

```js
Promise.race([
  new Promise(r=>setTimeout(()=>r('fast'),100)),
  new Promise(r=>setTimeout(()=>r('slow'),500))
]).then(console.log);
```
</details>

<details>
<summary>2.11 Async/Await</summary>

```js
(async () => {
  const v = await Promise.resolve('Awaited');
  console.log(v);
})();
```
</details>

<details>
<summary>2.12 Async Error Handling</summary>

```js
(async ()=>{
  try{ await Promise.reject('Fail'); }
  catch(e){ console.error(e); }
})();
```
</details>

<details>
<summary>2.13 fs.promises</summary>

```js
const fs = require('fs').promises;
(async ()=>{
  const txt = await fs.readFile('file.txt','utf8');
  console.log(txt);
})();
```
</details>

<details>
<summary>2.14 util.promisify</summary>

```js
const {promisify} = require('util');
const readFile = promisify(require('fs').readFile);
readFile('file.txt','utf8').then(console.log);
```
</details>

<details>
<summary>2.15 Delay Function</summary>

```js
const delay = ms => new Promise(r=>setTimeout(r,ms));
delay(500).then(()=>console.log('Done'));
```
</details>

<details>
<summary>2.16 Parallel Tasks</summary>

```js
async function run() {
  const [a,b] = await Promise.all([delay(100), delay(200)]);
  console.log('parallel done');
}
run();
```
</details>

<details>
<summary>2.17 Sequential Tasks</summary>

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
<summary>2.18 Async Map</summary>

```js
async function asyncMap(arr, fn){
  return Promise.all(arr.map(fn));
}
asyncMap([1,2], async x=>x*2).then(console.log);
```
</details>

<details>
<summary>2.19 Retry Logic</summary>

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
<summary>2.20 Race with Timeout</summary>

```js
function withTimeout(p, ms){
  const t = new Promise((_,rej)=>setTimeout(()=>rej('Timeout'), ms));
  return Promise.race([p,t]);
}
```
</details>

<details>
<summary>2.21 EventEmitter Async</summary>

```js
const {EventEmitter} = require('events');
const em = new EventEmitter();
em.on('data', async d => console.log(await Promise.resolve(d)));
em.emit('data','Hello');
```
</details>

<details>
<summary>2.22 Stream Async Iteration</summary>

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
<summary>2.23 Worker Threads</summary>

```js
const { Worker } = require('worker_threads');
new Worker('console.log("worker")',{eval:true});
```
</details>

<details>
<summary>2.24 Timers Promises</summary>

```js
const { setTimeout } = require('timers/promises');
await setTimeout(500);
console.log('done');
```
</details>

<details>
<summary>2.25 Async Generator</summary>

```js
async function* gen(){
  yield await Promise.resolve(1);
  yield 2;
}
for await(const x of gen()) console.log(x);
```
</details>

<details>
<summary>2.26 Pipeline Promises</summary>

```js
const {pipeline} = require('stream/promises');
await pipeline(fs.createReadStream('a.txt'), fs.createWriteStream('b.txt'));
```
</details>

<details>
<summary>2.27 callbackify</summary>

```js
const {callbackify} = require('util');
const fn = async ()=>'done';
callbackify(fn)((err,res)=>console.log(res));
```
</details>

<details>
<summary>2.28 AbortController</summary>

```js
const controller = new AbortController();
fetch('https://example.com',{signal:controller.signal});
controller.abort();
```
</details>

<details>
<summary>2.29 Semaphore</summary>

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
<summary>2.30 Async Queue with setTimeout</summary>

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

<a id="3-web-development-with-expressjs"></a>
## 3. Web Development with Express.js (≈80 Examples)

<details>
<summary>3.1 A simple Express.js server that responds with "Hello World"</summary>

```js
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(PORT, () => console.log(`Server running on http://localhost:${PORT}`));
```

</details>

<details>
<summary>3.2 RESTful API (CRUD for Users)</summary>

```js
const express = require('express');
const app = express();
app.use(express.json());

let users = [{ id: 1, name: 'Alice' }];

app.get('/users', (req, res) => res.json(users));
app.post('/users', (req, res) => {
  const user = { id: Date.now(), name: req.body.name };
  users.push(user);
  res.status(201).json(user);
});
app.put('/users/:id', (req, res) => {
  const user = users.find(u => u.id == req.params.id);
  if (!user) return res.sendStatus(404);
  user.name = req.body.name;
  res.json(user);
});
app.delete('/users/:id', (req, res) => {
  users = users.filter(u => u.id != req.params.id);
  res.sendStatus(204);
});

app.listen(3000, () => console.log('API ready on http://localhost:3000'));
```

</details>


<details>
<summary>3.3 Using custom middleware for request logging</summary>

```js
const express = require('express');
const app = express();

// Custom middleware
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
});

app.get('/', (req, res) => res.send('Middleware in action!'));

app.listen(3000, () => console.log('Server running with middleware'));

```

</details>


<details>
<summary>3.4 Serving Static Files</summary>

```js
const express = require('express');
const path = require('path');
const app = express();

app.use(express.static(path.join(__dirname, 'public')));

app.listen(3000, () => console.log('Static server at http://localhost:3000'));

```

</details>


<details>
<summary>3.5 Handling dynamic URL segments and query parameters.</summary>

```js
const express = require('express');
const app = express();

app.get('/user/:id', (req, res) => {
  const { id } = req.params;
  const { search } = req.query; // e.g. /user/42?search=books
  res.send(`User ID: ${id}, Search: ${search || 'none'}`);
});

app.listen(3000, () => console.log('Listening on http://localhost:3000'));

```

</details>


</details>


<details>

<summary>3.6 Error Handling Middleware</summary>

```js
const express = require('express');
const app = express();

app.get('/fail', (req, res, next) => {
  const err = new Error('Something went wrong!');
  err.status = 500;
  next(err);
});

// Error handler
app.use((err, req, res, next) => {
  res.status(err.status || 500).json({ message: err.message });
});

app.listen(3000, () => console.log('Error handling example running'));

```

</details>

</details>


<details>
<summary>3.7 File Upload with Multer</summary>

```js
const express = require('express');
const multer = require('multer');
const upload = multer({ dest: 'uploads/' });
const app = express();

app.post('/upload', upload.single('file'), (req, res) => {
  res.send(`File uploaded: ${req.file.originalname}`);
});

app.listen(3000, () => console.log('Upload server ready at /upload'));

```

</details>

</details>


<details>
<summary>3.8 JWT Authentication</summary>

```js
const express = require('express');
const jwt = require('jsonwebtoken');
const app = express();
app.use(express.json());

const SECRET = 'mysecret';

// Login to get token
app.post('/login', (req, res) => {
  const user = { id: 1, name: 'Alice' };
  const token = jwt.sign(user, SECRET, { expiresIn: '1h' });
  res.json({ token });
});

// Protected route
app.get('/profile', (req, res) => {
  const authHeader = req.headers['authorization'];
  const token = authHeader && authHeader.split(' ')[1];
  if (!token) return res.sendStatus(401);

  jwt.verify(token, SECRET, (err, user) => {
    if (err) return res.sendStatus(403);
    res.json({ message: 'Welcome!', user });
  });
});

app.listen(3000, () => console.log('JWT example running on /login and /profile'));

```

</details>

</details>

<!-- Add remaining Express examples -->

[Return to Table of Contents](#table-of-contents)
---

<a id="4-databases"></a>
## 4. Databases (≈50 Examples)

<details>
<summary>4.1 MongoDB with Mongoose</summary>

```js
// Install: npm i mongoose
const mongoose = require('mongoose');

mongoose.connect('mongodb://127.0.0.1:27017/mydb');

const User = mongoose.model('User', new mongoose.Schema({ name: String }));

(async () => {
  const user = await User.create({ name: 'Alice' });
  console.log('Saved:', user);
  const all = await User.find();
  console.log('All users:', all);
})();

```

</details>

<details>
<summary>4.2 PostgreSQL with pg</summary>

```js
// Install: npm i pg
const { Client } = require('pg');

const client = new Client({
  connectionString: 'postgresql://postgres:password@localhost:5432/mydb'
});

(async () => {
  await client.connect();
  const res = await client.query('SELECT NOW() AS current_time');
  console.log(res.rows[0]);
  await client.end();
})();

```

</details>

<details>
<summary>4.3 MySQL with mysql2</summary>

```js
// Install: npm i mysql2
const mysql = require('mysql2/promise');

(async () => {
  const conn = await mysql.createConnection({ host: 'localhost', user: 'root', database: 'test' });
  const [rows] = await conn.execute('SELECT 1 + 1 AS result');
  console.log('Query result:', rows[0].result);
  await conn.end();
})();

```

</details>

<details>
<summary>P4.4 SQLite with better-sqlite3</summary>

```js
// Install: npm i better-sqlite3
const Database = require('better-sqlite3');
const db = new Database('example.db');

db.prepare('CREATE TABLE IF NOT EXISTS notes (id INTEGER PRIMARY KEY, text TEXT)').run();
db.prepare('INSERT INTO notes (text) VALUES (?)').run('Hello SQLite');
const rows = db.prepare('SELECT * FROM notes').all();
console.log(rows);

```

</details>

<details>
<summary>4.5 Redis with redis</summary>

```js
// Install: npm i redis
const { createClient } = require('redis');

(async () => {
  const client = createClient();
  await client.connect();

  await client.set('greeting', 'Hello Redis!');
  const val = await client.get('greeting');
  console.log('Stored value:', val);

  await client.quit();
})();

```

</details>


<details>
<summary>4.6 MariaDB with mariadb</summary>

```js
// Install: npm i mariadb
const mariadb = require('mariadb');

(async () => {
  const pool = mariadb.createPool({ host: 'localhost', user: 'root', password: '', database: 'test' });
  const conn = await pool.getConnection();
  const rows = await conn.query('SELECT NOW() AS time');
  console.log('Current time:', rows[0].time);
  conn.release();
  pool.end();
})();

```

</details>

<details>
<summary>4.7 CouchDB with nano</summary>

```js
// Install: npm i nano
const nano = require('nano')('http://admin:password@localhost:5984');

(async () => {
  const db = nano.db.use('mydb');
  await db.insert({ type: 'note', text: 'Hello CouchDB' }, 'note1');
  const doc = await db.get('note1');
  console.log('Fetched doc:', doc);
})();

```

</details>


<details>
<summary>4.8 Cassandra with cassandra-driver</summary>

```js
// Install: npm i cassandra-driver
const cassandra = require('cassandra-driver');

(async () => {
  const client = new cassandra.Client({ contactPoints: ['127.0.0.1'], localDataCenter: 'datacenter1', keyspace: 'test' });
  const result = await client.execute('SELECT release_version FROM system.local');
  console.log('Cassandra version:', result.rows[0].release_version);
  await client.shutdown();
})();

```

</details>


<details>
<summary>4.9 Oracle Database with oracledb</summary>

```js
// Install: npm i oracledb
const oracledb = require('oracledb');

(async () => {
  const conn = await oracledb.getConnection({ user: 'system', password: 'password', connectionString: 'localhost/XE' });
  const result = await conn.execute('SELECT SYSDATE FROM dual');
  console.log('Current date:', result.rows[0][0]);
  await conn.close();
})();

```

</details>


<details>
<summary>4.10 Firebase Realtime Database</summary>

```js
// Install: npm i firebase
import { initializeApp } from 'firebase/app';
import { getDatabase, ref, set, get } from 'firebase/database';

const firebaseConfig = { /* your config */ };
const app = initializeApp(firebaseConfig);
const db = getDatabase(app);

(async () => {
  await set(ref(db, 'messages/msg1'), { text: 'Hello Firebase' });
  const snapshot = await get(ref(db, 'messages/msg1'));
  console.log('Data:', snapshot.val());
})();

```

</details>



[Return to Table of Contents](#table-of-contents)
---

<a id="5-real-time-applications"></a>
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

<a id="6-advanced-topics"></a>
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

<a id="7-practical-projects--utilities"></a>
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

<a id="8-Contribution-guide"></a>
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
