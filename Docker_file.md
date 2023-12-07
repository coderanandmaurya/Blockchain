Certainly! To create a simple Node.js backend application that prints "Hello, World!" and then deploy it using Docker, follow the steps below:

### 1. Create a Node.js Backend File

Create a file named `app.js` with the following content:

```javascript
// app.js
const http = require('http');

const hostname = '0.0.0.0';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello, World!\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

### 2. Create a `package.json` File

Create a `package.json` file with the following content:

```json
// package.json
{
  "name": "docker-node-hello-world",
  "version": "1.0.0",
  "description": "A simple Node.js app for Docker",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

### 3. Create a Dockerfile

Create a `Dockerfile` with the following content:

```Dockerfile
# Dockerfile
FROM node:14

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD [ "npm", "start" ]
```

### 4. Build and Run Docker Container

Now, you can build and run the Docker container:

```bash
# Build the Docker image
docker build -t node-hello-world .

# Run the Docker container
docker run -p 3000:3000 -d node-hello-world
```

This assumes that you have Docker installed on your machine.

Now, your Node.js application should be running in a Docker container, and you can access it by visiting `http://localhost:3000` in your web browser. You should see "Hello, World!" printed on the page.

Remember to replace any version numbers or additional configurations based on your specific needs.
