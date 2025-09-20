# Node.js 500+ Examples

A massive collection of **500+ practical Node.js examples**, covering everything from basic concepts and core modules to advanced topics, real-time applications, databases, and practical projects.  
Perfect for learners, teachers, and professionals. Contributions welcome!

**Current Progress:** 15/500 examples completed ✅

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

---

## 2. Asynchronous Programming (≈50 Examples)

<details>
<summary>Callbacks</summary>

```js
// Example 1: Simple callback
function greet(name, callback) {
  callback(`Hello, ${name}`);
}
greet('Alice', console.log);
```

</details>

<details>
<summary>Promises</summary>

```js
// Example 2: Promise chaining
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve('Done!'), 1000);
});
promise.then(console.log).catch(console.error);
```

</details>

<!-- Add remaining async examples -->

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

---

## 9. Roadmap

- Add advanced DB queries (transactions, joins, indexing)  
- Add caching examples (Redis, memory cache)  
- Add microservice examples and API integrations  
- Add testing patterns and CI/CD workflows  

```}
