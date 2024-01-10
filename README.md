# Renton Technical College CSI-244
<br />    

<div align="center">  
    <img src="logo.jpg" alt="Logo">
    <h3 align="center">Guided Activity 2</h3>
</div>

This repository is a part of CSI-244 at Renton Technical College.

## Guided Activity Part 3 Bootstrap and Formdata
1. Clone this repository to your machine.
2. Open the repository in Visual Studio code and follow the instructions below.

Thank you for clarifying. Let's create step-by-step instructions tailored to your specific project files, including the use of `res.sendFile` for serving your HTML pages, as seen in your `server.js`. I'll follow the structure and specifics of the files from your zip file.

### Step-by-Step Instructions for Your ExpressJS Project

#### Step 1: Project Setup

##### Creating Your Project
- **Action:** Start a new Node.js project and install Express.
  - Open your terminal or command prompt.
  - Run the following command to initialize your project:
    ```powershell
    npm init
    ```
  - Follow the prompts to create your project, setting `server.js` as the entry point.

##### Installing Express
- **Action:** Install Express.
  - In the terminal, run:
    ```powershell
    npm install express
    ```

##### Creating the Server File
- **Action:** Create the main server file.
  - In your project directory, create a file named `server.js`.

#### Step 2: Setting Up the Express Server

##### Writing the Server Code
- **Setting Up Express:**
  - Open `server.js` in a text editor.
  - Write the following code to import necessary modules and set up the Express app:
    ```javascript
    const express = require("express");
    const path = require("path");
    const fs = require("fs");
    const app = express();
    ```

- **Serving HTML Pages:**
  - Define routes to serve your `index.html` and `support.html` pages using `res.sendFile`. For example:
    ```javascript
    // Serve index.html on the root path
    app.get("/", (req, res) => {
      res.sendFile(path.join(__dirname, "public", "index.html"));
    });

    // Serve support.html on the '/support' path
    app.get("/support", (req, res) => {
      res.sendFile(path.join(__dirname, "public", "support.html"));
    });
    ```

- **Starting the Server:**
  - Make the server listen on a port (e.g., 3000) for incoming connections:
    ```javascript
    const PORT = process.env.PORT || 3000;
    app.listen(PORT, () => {
      console.log(`Server running on port ${PORT}`);
    });
    ```

#### Step 3: Creating HTML Pages

##### Creating `index.html`
- **Action:** Create the main page of your website.
  - Inside a directory named `public`, create a file named `index.html`.
  - Add your HTML content, including Bootstrap if used.

##### Creating `support.html`
- **Action:** Create a support page with a form.
  - Still in the `public` directory, create a file named `support.html`.
  - Design your form and include necessary HTML elements.

#### Step 4: Handling Form Submissions

##### Setting Up Route for Form Submission
- **Action:** Create a route to process form submissions.
  - In `server.js`, add a route for form submission. For example:
    ```javascript
    app.post("/submitform", (req, res) => {
      // Code to process form data
    });
    ```
  - Include necessary middleware to parse form data.

#### Step 5: Testing the Application

1. **Run Your Server:**
   - Use the command `node server.js` to start your server.

2. **Test the Pages and Form:**
   - Visit `http://localhost:3000` in a browser to view the `index.html` page.
   - Go to `http://localhost:3000/support` to access the support form.
   - Test submitting the form and ensure the server processes it as expected.

3. **Debugging:**
   - Troubleshoot any issues by checking the server console and ensuring all routes are correctly set up.


Create a new commit with the message Guided Activity 2 Complete and push the changes to GitHub


If you have any questions about this assignment please reach out to myself or our TA for this course.
