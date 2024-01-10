# Renton Technical College CSI-244
<br />    

<div align="center">  
    <img src="logo.jpg" alt="Logo">
    <h3 align="center">Guided Activity 2</h3>
</div>

This repository is a part of CSI-244 at Renton Technical College.

## Guided Activity Part 2 Intro To Node.js
1. Clone this repository to your machine.
2. Open the repository in Visual Studio code and follow the instructions below.

### Node.js Server with System Info, Logging, and Student Information

#### Objective
Create a Node.js server that:
1. Provides system information.
2. Logs visitor details.
3. Displays the log.
4. Shows a static HTML page with your personal details.

---

### Step 1: Project Setup

#### Creating Your Project Folder
- **Action:** Make a new folder for your project.
  - In your terminal or command prompt, run:
    ```bash
    mkdir my_node_server
    ```
  - This creates a directory named `my_node_server`.

- **Navigate to Your Project Folder:**
  - Change into your new directory:
    ```powershell
    cd my_node_server
    ```

#### Creating the Server File
- **Create a File Named `server.js`:**
  - This file will be the entry point for your Node.js server.
  - You can create it using a text editor or via the terminal:
    ```powershell
    new-item server.js
    ```
---
Create a new commit with the message Step 1 Complete and push the changes to GitHub

### Step 2: Create Separate Modules for Each Functionality

#### System Info Module (`systemInfo.js`)
- **Purpose:** To fetch and return the system's memory and CPU information.
- **Creating the File:**
  - In your project folder, create a new file named `systemInfo.js`.
- **Adding Code:**
  - Edit `systemInfo.js` to have the following content:
    ```javascript
    const os = require('os');

    function getSystemInfo() {
      return {
        totalMemory: os.totalmem(),
        freeMemory: os.freemem(),
        cpuCount: os.cpus().length
      };
    }

    module.exports = getSystemInfo;
    ```
  - Here, `os` is a built-in Node.js module for operating system-related utility methods.

#### Log Visitor Module (`logVisitor.js`)
- **Purpose:** To log each visitor's details to a file.
- **Creating the File:**
  - Create a file named `logVisitor.js`.
- **Adding Code:**
  - Add this to `logVisitor.js`:
    ```javascript
    const fs = require('fs');
    const path = require('path');

    function logVisitor(visitorData) {
      const logFilePath = path.join(__dirname, 'visitors.log');
      fs.appendFileSync(logFilePath, visitorData + '\n');
    }

    module.exports = logVisitor;
    ```
  - `fs` is used for file system operations, and `path` helps with file paths.

#### Read Log File Module (`readLogFile.js`)
- **Purpose:** To read and return the contents of the log file.
- **Creating the File:**
  - Create a file named `readLogFile.js`.
- **Adding Code:**
  - Write the following in `readLogFile.js`:
    ```javascript
    const fs = require('fs');
    const path = require('path');

    function getLogFile() {
      const logFilePath = path.join(__dirname, 'visitors.log');
      return fs.readFileSync(logFilePath, 'utf8');
    }

    module.exports = getLogFile;
    ```

---
Create a new commit with the message Step 2 Complete and push the changes to GitHub
### Step 3: Implementing the Server (`server.js`)

#### Setting Up the Server
- **Code Explanation:**
  - Import the necessary modules and your custom modules at the top of `server.js`.
  - Create an HTTP server using the `http` module.
  - Define the logic for each endpoint.

- **Implementing the Server:**
  - Edit `server.js` to include:
    ```javascript
    const http = require('http');
    const getSystemInfo = require('./systemInfo');
    const logVisitor = require('./logVisitor');
    const getLogFile = require('./readLogFile');
    const fs = require('fs');
    const path = require('path');

    const server = http.createServer((req, res) => {
      if (req.url === '/system-info') {
        // ... (System Info logic)
      } else if (req.url === '/log-visit') {
        // ... (Log Visit logic)
      } else if (req.url === '/show-log') {
        // ... (Show Log logic)
      } else if (req.url === '/') {
        // ... (Student Information logic)
      } else {
        res.writeHead(404);
        res.end('Not Found');
      }
    });

    const port = 3000;
    server.listen(port, () => {
      console.log(`Server running on port ${port}`);
    });
    ```

#### Adding Logic for Each Endpoint
- **System Info Endpoint:**
  ```javascript
  if (req.url === '/system-info') {
    res.writeHead(200, {'Content-Type': 'application/json'});
    res.end(JSON.stringify(getSystemInfo()));
  }
  ```
  - This returns the system's memory

 and CPU information in JSON format.

- **Log Visit Endpoint:**
  ```javascript
  else if (req.url === '/log-visit') {
    const visitorData = `Visitor at ${new Date().toISOString()}`;
    logVisitor(visitorData);
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Visit logged');
  }
  ```
  - Logs the visitor's timestamp to a file.

- **Show Log Endpoint:**
  ```javascript
  else if (req.url === '/show-log') {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end(getLogFile());
  }
  ```
  - Displays the contents of the log file.

- **Student Information Endpoint:**
  - Create a static HTML file named `studentInfo.html` in your project folder with your details.
  - Add the following logic:
    ```javascript
    else if (req.url === '/') {
      const studentInfoPath = path.join(__dirname, 'studentInfo.html');
      fs.readFile(studentInfoPath, (err, data) => {
        if (err) {
          res.writeHead(500);
          res.end('Error loading student information');
        } else {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end(data);
        }
      });
    }
    ```

---
Create a new commit with the message Step 3 Complete and push the changes to GitHub
### Step 4: Testing Your Server

1. **Run Your Server:**
   - In the terminal, start your server:
     ```bash
     node server.js
     ```
   - Your server is now live on `http://localhost:3000`.

2. **Test Each Endpoint:**
   - Visit `http://localhost:3000/` in a web browser for your student details.
   - Go to `http://localhost:3000/system-info` for system info.
   - Navigate to `http://localhost:3000/log-visit` to log your visit.
   - Check `http://localhost:3000/show-log` to view the log.

Create a new commit with the message Guided Activity 2 Complete and push the changes to GitHub


If you have any questions about this assignment please reach out to myself or our TA for this course.
