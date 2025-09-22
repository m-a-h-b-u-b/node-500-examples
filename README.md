# Node.js 500+ Examples

A massive collection of **500+ practical Node.js examples**, covering everything from basic concepts and core modules to advanced topics, real-time applications, databases, and practical projects.  
Perfect for learners, teachers, and professionals. Contributions welcome!

**Current Progress:** 103/500 examples completed ✅

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
## 1. Basic Concepts & Core Modules 

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
## 2. Asynchronous Programming 

<details>
<summary>2.1 Basic callback pattern</summary>

```js
const fs = require('fs');

console.log('Reading file...');
fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) return console.error('Error:', err);
  console.log('File content:', data);
});
console.log('This prints first while file is being read.');

```
</details>

<details>
<summary>2.2 Promise-based File Read</summary>

```js
const fs = require('fs').promises;

console.log('Reading file with promises...');
fs.readFile('example.txt', 'utf8')
  .then(data => console.log('Content:', data))
  .catch(err => console.error(err));

```
</details>

<details>
<summary>2.3 Async/Await with Try–Catch</summary>

```js
const fs = require('fs').promises;

async function showFile() {
  try {
    const data = await fs.readFile('example.txt', 'utf8');
    console.log('File data:', data);
  } catch (err) {
    console.error('Read error:', err);
  }
}
showFile();

```
</details>

<details>
<summary>2.4 Parallel Execution with Promise.all</summary>

```js
const fetch = require('node-fetch'); // npm i node-fetch

async function fetchData() {
  const urls = ['https://api.github.com', 'https://jsonplaceholder.typicode.com/todos/1'];
  const results = await Promise.all(urls.map(url => fetch(url).then(r => r.json())));
  console.log('Responses:', results);
}
fetchData();
```
</details>

<details>
<summary>2.5 Event Loop & setImmediate vs setTimeout</summary>

```js
console.log('Start');

setTimeout(() => console.log('Timeout callback'), 0);
setImmediate(() => console.log('Immediate callback'));
process.nextTick(() => console.log('NextTick callback'));

console.log('End');

```
</details>

<details>
<summary>2.6 Convert a callback-based function into a Promise-based one.</summary>

```js
const fs = require('fs');
const util = require('util');
const readFile = util.promisify(fs.readFile);

readFile('example.txt', 'utf8')
  .then(data => console.log('Promisified read:', data))
  .catch(console.error);
```
</details>

<details>
<summary>2.7 Sequential vs. Parallel Async Tasks</summary>

```js
const delay = ms => new Promise(res => setTimeout(res, ms));

async function sequential() {
  console.time('sequential');
  await delay(1000);
  await delay(1000);
  console.timeEnd('sequential');
}

async function parallel() {
  console.time('parallel');
  await Promise.all([delay(1000), delay(1000)]);
  console.timeEnd('parallel');
}

sequential().then(parallel);
```
</details>

<details>
<summary>2.8 Async Iteration with for await...of</summary>

```js
const { Readable } = require('stream');

async function* generate() {
  for (let i = 1; i <= 3; i++) {
    await new Promise(r => setTimeout(r, 500));
    yield i;
  }
}

(async () => {
  for await (const num of generate()) {
    console.log('Number:', num);
  }
})();
```
</details>

<details>
<summary>2.9 Streaming File Read (Backpressure Demo)</summary>

```js
const fs = require('fs');

const stream = fs.createReadStream('bigfile.txt', { encoding: 'utf8' });
stream.on('data', chunk => console.log('Chunk length:', chunk.length));
stream.on('end', () => console.log('Stream finished'));
```
</details>

<details>
<summary>2.10 Using Promise.race</summary>

```js
const slow = new Promise(res => setTimeout(() => res('slow done'), 2000));
const fast = new Promise(res => setTimeout(() => res('fast done'), 500));

Promise.race([slow, fast]).then(result => console.log('Winner:', result));
```
</details>

<details>
<summary>2.11 Worker Threads for CPU-bound Tasks</summary>

```js
// worker.js
const { parentPort } = require('worker_threads');
let sum = 0;
for (let i = 0; i < 1e8; i++) sum += i;
parentPort.postMessage(sum);

// main.js
const { Worker } = require('worker_threads');
new Worker('./worker.js').on('message', msg => console.log('Sum:', msg));

```
</details>

<details>
<summary>2.12 Abortable Fetch with AbortController</summary>

```js
const fetch = require('node-fetch'); // npm i node-fetch
const controller = new AbortController();
const signal = controller.signal;

setTimeout(() => controller.abort(), 1000); // cancel after 1s

fetch('https://httpbin.org/delay/5', { signal })
  .then(res => res.text())
  .then(console.log)
  .catch(err => console.error('Fetch aborted:', err.name));

```
</details>

<details>
<summary>2.13 fDelayed Retry with Async Function</summary>

```js
async function retry(fn, retries = 3, delay = 500) {
  for (let i = 0; i < retries; i++) {
    try {
      return await fn();
    } catch (err) {
      console.log(`Attempt ${i + 1} failed`);
      if (i < retries - 1) await new Promise(r => setTimeout(r, delay));
    }
  }
}

retry(() => Promise.reject('Fail')).catch(err => console.error('All attempts failed:', err));
```
</details>

<details>
<summary>2.14 Async Map with Promise.all</summary>

```js
async function asyncDouble(n) {
  return new Promise(res => setTimeout(() => res(n * 2), 300));
}

async function run() {
  const numbers = [1, 2, 3];
  const doubled = await Promise.all(numbers.map(asyncDouble));
  console.log('Doubled:', doubled);
}

run();
```
</details>

<details>
<summary>2.15 Async Filter Example</summary>

```js
async function isEvenAsync(n) {
  await new Promise(r => setTimeout(r, 100));
  return n % 2 === 0;
}

async function filterAsync(arr, fn) {
  const results = await Promise.all(arr.map(fn));
  return arr.filter((_, i) => results[i]);
}

filterAsync([1,2,3,4,5], isEvenAsync).then(console.log); // [2,4]

```
</details>

<details>
<summary>2.16 Async Reduce Example</summary>

```js
async function sumAsync(arr) {
  let total = 0;
  for (const num of arr) {
    total += await Promise.resolve(num);
  }
  return total;
}

sumAsync([1,2,3,4]).then(console.log); // 10

```
</details>

<details>
<summary>2.17 Timeout Wrapper for Async Functions</summary>

```js
function withTimeout(fn, ms) {
  return Promise.race([
    fn(),
    new Promise((_, rej) => setTimeout(() => rej(new Error('Timeout')), ms))
  ]);
}

withTimeout(() => new Promise(res => setTimeout(() => res('Done'), 2000)), 1000)
  .then(console.log)
  .catch(err => console.error(err.message)); // Timeout

```
</details>

<!-- Add remaining async examples -->

[Return to Table of Contents](#table-of-contents)
---

<a id="3-web-development-with-expressjs"></a>
## 3. Web Development with Express.js 

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
## 4. Databases 

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
## 5. Real-time Applications 

<details>
<summary>5.1 Chat App with Socket.IO</summary>

```js
// Install: npm i express socket.io
const express = require('express');
const http = require('http');
const { Server } = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = new Server(server);

io.on('connection', socket => {
  console.log('User connected');
  socket.on('chat message', msg => io.emit('chat message', msg));
});

server.listen(3000, () => console.log('Chat server on http://localhost:3000'));

```

</details>

<details>
<summary>5.2 Live Stock Prices via WebSockets</summary>

```js
// Install: npm i ws
const WebSocket = require('ws');
const wss = new WebSocket.Server({ port: 8080 });

setInterval(() => {
  const price = (100 + Math.random() * 10).toFixed(2);
  wss.clients.forEach(client => client.send(JSON.stringify({ symbol: 'AAPL', price })));
}, 2000);

console.log('Stock price server running on ws://localhost:8080');

```

</details>

<details>
<summary>5.3 Real-time Notifications with Redis Pub/Sub</summary>

```js
// Install: npm i express socket.io redis
const express = require('express');
const http = require('http');
const { Server } = require('socket.io');
const { createClient } = require('redis');

const app = express();
const server = http.createServer(app);
const io = new Server(server);
const subscriber = createClient();

(async () => {
  await subscriber.connect();
  await subscriber.subscribe('notifications', msg => io.emit('notify', msg));
})();

server.listen(4000, () => console.log('Notifications server running'));

```

</details>


<details>
<summary>5.4 Collaborative Whiteboard with WebSockets</summary>

```js
// Install: npm i express ws
const express = require('express');
const http = require('http');
const WebSocket = require('ws');

const app = express();
const server = http.createServer(app);
const wss = new WebSocket.Server({ server });

wss.on('connection', ws =>
  ws.on('message', data =>
    wss.clients.forEach(client => client.send(data))
  )
);

server.listen(3001, () => console.log('Whiteboard server running'));

```

</details>


<details>
<summary>5.5 Multiplayer Game Server with Socket.IO</summary>

```js
// Install: npm i express socket.io
const express = require('express');
const http = require('http');
const { Server } = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = new Server(server);

let players = {};

io.on('connection', socket => {
  players[socket.id] = { x: 0, y: 0 };
  socket.emit('init', players);

  socket.on('move', data => {
    players[socket.id] = data;
    io.emit('update', players);
  });

  socket.on('disconnect', () => delete players[socket.id]);
});

server.listen(5000, () => console.log('Game server running'));

```

</details>



<details>
<summary>5.6 Multiplayer Game Server with Socket.IO</summary>

```js
// Install: npm i express socket.io
const express = require('express');
const http = require('http');
const { Server } = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = new Server(server);

io.on('connection', socket => {
  socket.on('location', coords => {
    // broadcast updated GPS coordinates to all clients
    io.emit('location-update', coords);
  });
});

server.listen(3002, () => console.log('Location tracking server running'));

```
</details>

<details>
<summary>5.7 Server-Sent Events (SSE) Live Feed</summary>

```js
// No extra package required
const express = require('express');
const app = express();

app.get('/stream', (req, res) => {
  res.writeHead(200, {
    'Content-Type': 'text/event-stream',
    'Cache-Control': 'no-cache',
    'Connection': 'keep-alive'
  });
  setInterval(() => {
    res.write(`data: ${new Date().toISOString()}\n\n`);
  }, 1000);
});

app.listen(3003, () => console.log('SSE server on http://localhost:3003/stream'));

```
</details>

<details>
<summary>5.8 MQTT IoT Sensor Stream</summary>

```js
// Install: npm i mqtt
const mqtt = require('mqtt');
const client = mqtt.connect('mqtt://test.mosquitto.org');

client.on('connect', () => {
  setInterval(() => {
    const temp = (20 + Math.random() * 5).toFixed(1);
    client.publish('sensors/temperature', temp);
  }, 3000);
});

client.on('message', (topic, msg) => console.log(topic, msg.toString()));
client.subscribe('sensors/temperature');

```
</details>

<details>
<summary>5.9 Real-Time Collaboration with Yjs + WebSocket</summary>

```js
// Install: npm i express ws y-websocket
const http = require('http');
const WebSocket = require('ws');
const setupWSConnection = require('y-websocket/bin/utils').setupWSConnection;

const server = http.createServer();
const wss = new WebSocket.Server({ server });

wss.on('connection', (ws, req) => {
  setupWSConnection(ws, req);
});

server.listen(1234, () => console.log('Yjs collaborative editing server running'));

```
</details>

<details>
<summary>5.10 GraphQL Subscriptions (Apollo Server)</summary>

```js
// Install: npm i apollo-server graphql graphql-subscriptions
const { ApolloServer, gql, PubSub } = require('apollo-server');
const pubsub = new PubSub();

const typeDefs = gql`
  type Query { _: Boolean }
  type Subscription { time: String }
`;

const resolvers = {
  Subscription: {
    time: { subscribe: () => setInterval(() => pubsub.publish('TIME', { time: new Date().toISOString() }), 1000) || pubsub.asyncIterator('TIME') }
  }
};

new ApolloServer({ typeDefs, resolvers }).listen(4000, () =>
  console.log('GraphQL subscription server running')
);

```
</details>

<details>
<summary>5.11 Kafka Real-Time Stream Consumer</summary>

```js
// Install: npm i kafkajs
const { Kafka } = require('kafkajs');
const kafka = new Kafka({ brokers: ['localhost:9092'] });
const consumer = kafka.consumer({ groupId: 'realtime-group' });

(async () => {
  await consumer.connect();
  await consumer.subscribe({ topic: 'events' });
  await consumer.run({
    eachMessage: async ({ topic, message }) =>
      console.log(`Received: ${message.value.toString()}`)
  });
})();

```
</details>


[Return to Table of Contents](#table-of-contents)
---

<a id="6-advanced-topics"></a>
## 6. Advanced Topics 

<details>
<summary>6.1 Clustering</summary>

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
<summary>6.2 Child Processes</summary>

```js
// Example: Spawn child process
const { spawn } = require('child_process');
const ls = spawn('ls', ['-lh']);
ls.stdout.on('data', data => console.log(`Output: ${data}`));
```

</details>

<details>
<summary>6.3 Worker Threads - Offload CPU-intensive tasks to a separate thread.</summary>

```js
const { Worker, isMainThread, parentPort } = require('worker_threads');

if (isMainThread) {
  const worker = new Worker(__filename);
  worker.on('message', msg => console.log('From worker:', msg));
} else {
  parentPort.postMessage('Hello from worker thread!');
}
```

</details>

<details>
<summary>6.4 Event Loop Monitoring - Measure performance of code sections in Node.js. </summary>

```js
const { performance, PerformanceObserver } = require('perf_hooks');

const obs = new PerformanceObserver((items) => console.log(items.getEntries()));
obs.observe({ entryTypes: ['measure'] });

performance.mark('A');
// Simulate heavy task
for (let i = 0; i < 1e6; i++) {}
performance.mark('B');
performance.measure('Loop duration', 'A', 'B');
```

</details>

<details>
<summary>Advanced HTTP/2 Server - for improved speed and multiplexing.</summary>

```js
const http2 = require('http2');
const server = http2.createServer((req, res) => {
  res.end('Hello HTTP/2');
});

server.listen(3000, () => console.log('HTTP/2 server running on port 3000'));
```

</details>

<details>
<summary>6.6 Native Addons with N-API - Integrate C/C++ modules for performance-critical operations.</summary>

```js
// Example assumes pre-built native addon: myaddon.node
const addon = require('./build/Release/myaddon.node');
console.log('Result from native addon:', addon.hello());
```

</details>

<details>
<summary>6.7 Dynamic Module Import</summary>

```js
(async () => {
  const { join } = await import('path');
  console.log(join('folder', 'file.txt'));
})();
```

</details>

<details>
<summary>6.8 Buffer Manipulation</summary>

```js
const buf = Buffer.from('Hello Node.js');
console.log(buf.toString());       // Output: Hello Node.js
console.log(buf.toJSON());         // Output: JSON representation

```

</details>

<details>
<summary>6.9 Stream Piping with Backpressure </summary>

```js
const fs = require('fs');
const zlib = require('zlib');

fs.createReadStream('input.txt')
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream('input.txt.gz'));

```

</details>

<details>
<summary>6.10 Advanced Clustering with Sticky Sessions - se sticky sessions to distribute TCP connections across cluster workers.</summary>

```js
const cluster = require('cluster');
const http = require('http');
const net = require('net');

if (cluster.isMaster) {
  const workers = [];
  const numCPUs = require('os').cpus().length;
  for (let i = 0; i < numCPUs; i++) workers.push(cluster.fork());

  const server = net.createServer({ pauseOnConnect: true }, (socket) => {
    const worker = workers[socket.remotePort % numCPUs];
    worker.send('socket', socket);
  });
  server.listen(3000);
} else {
  process.on('message', (msg, socket) => {
    if (msg === 'socket') {
      socket.resume();
      socket.end('Handled by worker ' + process.pid);
    }
  });
}

```

</details>

<details>
<summary>6.11 Process Signals Handling </summary>

```js
process.on('SIGINT', () => {
  console.log('Received SIGINT. Exiting gracefully.');
  process.exit(0);
});

```

</details>

<details>
<summary>6.12 High-Resolution Timers - Benchmark critical sections with millisecond precision. </summary>

```js
const { performance } = require('perf_hooks');
const start = performance.now();
for(let i=0;i<1e6;i++){}
console.log('Loop took:', performance.now() - start, 'ms');

```

</details>

<details>
<summary>6.13 Worker Pool Example </summary>

```js
const { Worker } = require('worker_threads');

function runTask(task) {
  return new Promise((resolve, reject) => {
    const worker = new Worker('./worker.js', { workerData: task });
    worker.on('message', resolve);
    worker.on('error', reject);
  });
}

(async () => {
  const result = await runTask({ number: 42 });
  console.log(result);
})();

```

</details>

<details>
<summary>6.14 Advanced EventEmitter Patterns </summary>

```js
const { EventEmitter } = require('events');

class MyEmitter extends EventEmitter {
  async emitAsync(event, ...args) {
    const listeners = this.listeners(event);
    for(const listener of listeners) await listener(...args);
  }
}

const emitter = new MyEmitter();
emitter.on('data', async msg => console.log('Received:', msg));
emitter.emitAsync('data', 'Hello Advanced');

```

</details>

<details>
<summary>6.15 Async Iterators over Streams </summary>

```js
const fs = require('fs');

(async () => {
  for await (const chunk of fs.createReadStream('file.txt')) {
    console.log(chunk.toString());
  }
})();

```

</details>

<details>
<summary>6.16 HTTP Request Retry with Axios </summary>

```js
const axios = require('axios');

async function fetchWithRetry(url, retries=3) {
  for(let i=0; i<retries; i++){
    try { return await axios.get(url); }
    catch(e){ if(i===retries-1) throw e; }
  }
}

fetchWithRetry('https://api.github.com').then(res => console.log(res.status));

```

</details>

<details>
<summary>6.17 Memory Usage Analysis - Node.js process memory for optimization.</summary>

```js
console.log('Memory Usage:', process.memoryUsage());

```

</details>

<details>
<summary>6.18 Event Loop Delay Monitoring</summary>

```js
const { monitorEventLoopDelay } = require('perf_hooks');
const h = monitorEventLoopDelay();
h.enable();

setTimeout(() => {
  h.disable();
  console.log('Event Loop Delay (ms):', h.mean / 1e6);
}, 1000);

```

</details>

<details>
<summary>6.19 HTTP2 Server for multiplexed connections</summary>

```js
const http2 = require('http2');
const fs = require('fs');

const server = http2.createSecureServer({
  key: fs.readFileSync('key.pem'),
  cert: fs.readFileSync('cert.pem')
});

server.on('stream', (stream) => {
  stream.respond({ ':status': 200 });
  stream.end('Hello HTTP2');
});

server.listen(3000);

```

</details>

<details>
<summary>6.20 Dynamic Module Loading</summary>

```js
(async () => {
  const moduleName = './myModule.js';
  const mod = await import(moduleName);
  mod.run();
})();

```

</details>

<details>
<summary>6.21 Custom Writable Stream</summary>

```js
const { Writable } = require('stream');

const writer = new Writable({
  write(chunk, enc, cb) {
    console.log('Chunk:', chunk.toString());
    cb();
  }
});

process.stdin.pipe(writer);

```

</details>


<details>
<summary>6.22 Custom Readable Stream</summary>

```js
const { Readable } = require('stream');

const readable = new Readable({
  read(size) {
    this.push('Data chunk\n');
    this.push(null);
  }
});

readable.pipe(process.stdout);
```

</details>

<details>
<summary>6.23 Native Addons - Integrate C++ for performance-critical logic</summary>

```js
// Example: simple native addon
// In C++ create addon.cc
// compile with node-gyp and require in JS
const addon = require('./build/Release/addon');
console.log(addon.hello());

```

</details>

<details>
<summary>6.24 Cluster with Round-Robin Load Balancing</summary>

```js
const cluster = require('cluster');
const http = require('http');
if(cluster.isPrimary){
  for(let i=0;i<2;i++) cluster.fork();
} else {
  http.createServer((req,res)=>res.end(`Handled by ${process.pid}`)).listen(3000);
}

```

</details>

<details>
<summary>6.25 Redis Caching Example</summary>

```js
const redis = require('redis');
const client = redis.createClient();
await client.connect();

await client.set('name', 'NodeJS');
const value = await client.get('name');
console.log(value);

```

</details>

<details>
<summary>6.26 Rate Limiting Middleware - Protect APIs from excessive requests.</summary>

```js
const rateLimit = require('express-rate-limit');
const limiter = rateLimit({ windowMs: 60000, max: 10 });
app.use(limiter);

```

</details>

<details>
<summary>6.27 Graceful Shutdown of Servers</summary>

```js
const server = require('http').createServer();
server.listen(3000);
process.on('SIGTERM', () => {
  server.close(() => console.log('Server shut down gracefully'));
});

```

</details>

<details>
<summary>6.28 JWT Token Refresh Example</summary>

```js
const jwt = require('jsonwebtoken');
const refreshToken = jwt.sign({ id:1 }, 'secret', { expiresIn:'7d' });

```

</details>

<details>
<summary>6.29 Cluster with Health Checks</summary>

```js
const cluster = require('cluster');
if(cluster.isPrimary){
  const worker = cluster.fork();
  setInterval(()=>worker.isConnected() && console.log('Worker healthy'), 1000);
}

```

</details>

<details>
<summary>6.30 Dynamic API Mocking</summary>

```js
const express = require('express');
const app = express();
app.get('/api/:resource', (req,res)=>res.json({ resource:req.params.resource }));
app.listen(3000);

```

</details>

<details>
<summary>6.31 Microservice Communication with NATS</summary>

```js
const { connect } = require('nats');
(async () => {
  const nc = await connect({ servers: 'nats://localhost:4222' });
  nc.subscribe('updates', msg => console.log('Received:', msg));
})();

```

</details>

<details>
<summary>6.32 Node.js Performance Hooks</summary>

```js
const { performance, PerformanceObserver } = require('perf_hooks');

const obs = new PerformanceObserver((items) => console.log(items.getEntries()));
obs.observe({ entryTypes: ['measure'] });

performance.mark('start');
for(let i=0;i<1e6;i++){}
performance.mark('end');
performance.measure('loop', 'start', 'end');

```

</details>

[Return to Table of Contents](#table-of-contents)
---

<a id="7-practical-projects--utilities"></a>
## 7. Practical Projects & Utilities 

<details>
<summary>7.1 Image Resizer CLI</summary>

```js
#!/usr/bin/env node
// file: img-resizer.js
const { Command } = require('commander');
const sharp = require('sharp');
const program = new Command();

program
  .requiredOption('-i, --input <file>', 'input image')
  .requiredOption('-o, --output <file>', 'output image')
  .option('-w, --width <n>', 'width', parseInt)
  .option('-h, --height <n>', 'height', parseInt)
  .action(async opts => {
    await sharp(opts.input)
      .resize(opts.width, opts.height)
      .toFile(opts.output);
    console.log(`Saved ${opts.output}`);
  });

program.parse();
// sample run: node img-resizer.js -i photo.jpg -o thumb.jpg -w 300
```

</details>

<details>
<summary>7.2 PDF Merger Utility</summary>

```js
// file: pdf-merge.js
const { PDFDocument } = require('pdf-lib');
const fs = require('fs');

(async () => {
  const files = process.argv.slice(2);
  if (files.length < 2) return console.log('Usage: node pdf-merge.js a.pdf b.pdf ...');
  const merged = await PDFDocument.create();

  for (const f of files) {
    const bytes = await fs.promises.readFile(f);
    const pdf = await PDFDocument.load(bytes);
    const pages = await merged.copyPages(pdf, pdf.getPageIndices());
    pages.forEach(p => merged.addPage(p));
  }

  const out = await merged.save();
  await fs.promises.writeFile('merged.pdf', out);
  console.log('merged.pdf created');
})();
```

</details>

<details>
<summary>7.3 System Info Dashboard (Web)</summary>

```js
// file: sys-dashboard.js
const express = require('express');
const os = require('os');
const app = express();

app.get('/', (req, res) => {
  const data = {
    platform: os.platform(),
    uptime: os.uptime(),
    load: os.loadavg(),
    memory: { free: os.freemem(), total: os.totalmem() }
  };
  res.json(data);
});

app.listen(4000, () => console.log('System info on http://localhost:4000'));
```

</details>


<details>
<summary>7.4 Markdown → HTML Converter</summary>

```js
// file: md2html.js
const fs = require('fs-extra');
const { marked } = require('marked');

(async () => {
  const [,, input, output] = process.argv;
  if (!input || !output) return console.log('Usage: node md2html.js in.md out.html');
  const md = await fs.readFile(input, 'utf8');
  const html = `<!DOCTYPE html><html><body>${marked(md)}</body></html>`;
  await fs.writeFile(output, html);
  console.log(`Converted ${input} → ${output}`);
})();
```

</details>


<details>
<summary>7.5 Simple URL Shortener</summary>

```js
// file: url-shortener.js
const express = require('express');
const { nanoid } = require('nanoid');
const fs = require('fs');
const dbFile = './urls.json';
const app = express();

app.use(express.json());
let db = fs.existsSync(dbFile) ? JSON.parse(fs.readFileSync(dbFile)) : {};

app.post('/new', (req, res) => {
  const { url } = req.body;
  if (!url) return res.status(400).json({error:'url required'});
  const id = nanoid(6);
  db[id] = url;
  fs.writeFileSync(dbFile, JSON.stringify(db));
  res.json({ short: `http://localhost:5000/${id}` });
});

app.get('/:id', (req, res) => {
  const long = db[req.params.id];
  if (!long) return res.status(404).send('Not found');
  res.redirect(long);
});

app.listen(5000, () => console.log('URL shortener on http://localhost:5000'));
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
