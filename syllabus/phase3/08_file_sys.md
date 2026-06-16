# 🚀 Node.js Mastery Roadmap

## Phase 8: Working with File Systems – Reading and Writing Files

---

# 🎯 Mission of This Phase

Most backend applications interact with files.

Examples:

* Uploading profile pictures
* Reading configuration files
* Processing CSV data
* Generating reports
* Storing logs
* Managing documents
* Handling media uploads

This phase teaches how Node.js interacts with the operating system's file system.

---

# 🧠 First Principles Understanding

## What is a File System?

A file system is how an operating system organizes and stores data.

Example:

```text
Computer
   ↓
Disk
   ↓
Folders
   ↓
Files
```

Everything eventually becomes:

```text
Bytes Stored On Disk
```

---

## First Principle

Node.js applications do not directly access storage devices.

Instead:

```text
Application
     ↓
fs Module
     ↓
Operating System
     ↓
Disk Storage
```

The `fs` module acts as a bridge.

---

# 📂 Why File Systems Matter

Without databases:

```text
Data → Lost After Restart
```

Without file systems:

```text
Documents
Images
Videos
Logs
Configurations
```

Cannot be stored permanently.

---

## Real-World Examples

### User Uploads

```text
avatar.jpg
```

---

### Logs

```text
server.log
```

---

### Reports

```text
sales-report.pdf
```

---

### Configurations

```text
config.json
```

---

# 1️⃣ Introduction to the fs Module

## What is fs?

Node.js provides a built-in module:

```js
const fs = require("fs");
```

No installation required.

---

## Responsibilities

The fs module can:

* Create files
* Read files
* Write files
* Update files
* Delete files
* Create directories
* Read directories

---

## Checklist

* [ ] Import fs module.
* [ ] Understand file operations.
* [ ] Understand directory operations.

---

## Veteran Insight

Most backend systems use the file system more than developers realize.

---

# 2️⃣ Understanding File Operations

## Common Operations

```text
Create
Read
Update
Delete
```

File systems also follow CRUD.

---

## File Lifecycle

```text
Create File
      ↓
Read File
      ↓
Modify File
      ↓
Delete File
```

---

## Checklist

* [ ] Understand CRUD for files.
* [ ] Understand file paths.
* [ ] Understand permissions.

---

# 3️⃣ Understanding File Paths

## Absolute Path

Full location.

Example:

```text
C:/Users/John/file.txt
```

---

## Relative Path

Relative to current location.

Example:

```text
./file.txt
```

---

## Useful Globals

### Current Directory

```js
__dirname
```

---

### Current File

```js
__filename
```

---

## Path Construction

Use:

```js
const path = require("path");
```

---

Example:

```js
path.join(
    __dirname,
    "files",
    "notes.txt"
);
```

---

## Checklist

* [ ] Understand paths.
* [ ] Use path.join().
* [ ] Avoid hardcoded paths.

---

## Veteran Understanding

Hardcoded paths break portability.

Always use path utilities.

---

# 4️⃣ Reading Files

## Synchronous Reading

```js
const data =
fs.readFileSync(
    "file.txt",
    "utf8"
);
```

---

## Execution Flow

```text
Read File
    ↓
Wait
    ↓
Continue
```

---

## Characteristics

* Blocking
* Simpler
* Slower for servers

---

## Checklist

* [ ] Read files synchronously.
* [ ] Understand blocking behavior.

---

# 5️⃣ Asynchronous File Reading

## Example

```js
fs.readFile(
    "file.txt",
    "utf8",
    (err, data) => {
        console.log(data);
    }
);
```

---

## Flow

```text
Start Reading
      ↓
Continue Program
      ↓
File Completes
      ↓
Callback Executes
```

---

## Characteristics

* Non-blocking
* Scalable
* Preferred in production

---

## Checklist

* [ ] Read files asynchronously.
* [ ] Handle errors.
* [ ] Compare performance.

---

## Veteran Insight

Server applications should almost always prefer asynchronous operations.

---

# 6️⃣ Reading Files with Promises

## Modern Approach

```js
const fs =
require("fs/promises");
```

---

## Example

```js
const data =
await fs.readFile(
    "file.txt",
    "utf8"
);
```

---

## Benefits

* Cleaner syntax
* Easier error handling
* Better scalability

---

## Checklist

* [ ] Use fs/promises.
* [ ] Use async/await.
* [ ] Handle exceptions.

---

## Veteran Understanding

Modern Node.js applications primarily use promise-based APIs.

---

# 7️⃣ Writing Files

## Creating a File

```js
fs.writeFile(
    "notes.txt",
    "Hello World",
    callback
);
```

---

## Synchronous Version

```js
fs.writeFileSync(
    "notes.txt",
    "Hello World"
);
```

---

## Overwrite Behavior

```text
Existing File
      ↓
New Content Replaces Old Content
```

---

## Checklist

* [ ] Create files.
* [ ] Write content.
* [ ] Understand overwrite behavior.

---

# 8️⃣ Appending Files

## Why Append?

Avoid replacing existing content.

---

## Example

```js
fs.appendFile(
    "log.txt",
    "New Entry\n",
    callback
);
```

---

## Common Use Cases

* Logs
* Reports
* Audit Trails

---

## Checklist

* [ ] Append data.
* [ ] Build log files.

---

## Veteran Insight

Production applications frequently append logs rather than rewrite files.

---

# 9️⃣ Deleting Files

## Example

```js
fs.unlink(
    "file.txt",
    callback
);
```

---

## Promise Version

```js
await fs.unlink(
    "file.txt"
);
```

---

## Checklist

* [ ] Delete files.
* [ ] Handle missing files.
* [ ] Handle permissions errors.

---

## Veteran Understanding

Deletion operations should often include safety checks.

---

# 🔟 Working with Directories

## Create Folder

```js
fs.mkdir(
    "uploads",
    callback
);
```

---

## Read Folder

```js
fs.readdir(
    "./uploads",
    callback
);
```

---

## Remove Folder

```js
fs.rmdir(
    "./uploads",
    callback
);
```

---

## Checklist

* [ ] Create directories.
* [ ] Read directories.
* [ ] Remove directories.

---

## Veteran Insight

Many upload systems dynamically create folders.

---

# 1️⃣1️⃣ File Metadata

## What is Metadata?

Information about files.

---

## Example

```js
fs.stat(
    "file.txt",
    callback
);
```

---

## Useful Information

```text
Size
Creation Date
Modified Date
Permissions
```

---

## Checklist

* [ ] Read metadata.
* [ ] Check file size.
* [ ] Check timestamps.

---

## Veteran Understanding

Metadata validation improves upload security.

---

# 1️⃣2️⃣ File Uploads

## Why File Uploads Matter

Applications frequently receive:

* Images
* Videos
* PDFs
* Documents

---

## Upload Flow

```text
Browser
    ↓
Multipart Form
    ↓
Express Server
    ↓
Multer Middleware
    ↓
File Storage
```

---

# 1️⃣3️⃣ Understanding Multipart Forms

## Why JSON Doesn't Work

JSON handles:

```text
Text
Numbers
Objects
```

Poor for large files.

---

## Solution

```text
multipart/form-data
```

Designed for file transfer.

---

## Checklist

* [ ] Understand multipart forms.
* [ ] Understand file transfer.

---

# 1️⃣4️⃣ Using Multer

## Installation

```bash
npm install multer
```

---

## Basic Setup

```js
const multer =
require("multer");
```

---

## Storage Configuration

```js
const upload =
multer({
    dest: "uploads/"
});
```

---

## Upload Route

```js
app.post(
    "/upload",
    upload.single("image"),
    handler
);
```

---

## Request Flow

```text
User Uploads File
       ↓
Multer Processes File
       ↓
File Stored
       ↓
Route Executes
```

---

## Checklist

* [ ] Install multer.
* [ ] Configure storage.
* [ ] Upload files.
* [ ] Handle upload errors.

---

## Veteran Insight

File uploads are one of the most attacked backend features.

Always validate uploads.

---

# 1️⃣5️⃣ Upload Security

## Validate File Types

Allowed:

```text
jpg
png
pdf
```

---

## Reject Dangerous Files

```text
.exe
.bat
.sh
```

---

## Validate Size

Example:

```text
Maximum:
5 MB
```

---

## Scan Uploads

Large systems often use:

```text
Virus Scanners
Malware Detection
```

---

## Checklist

* [ ] Validate MIME types.
* [ ] Validate size.
* [ ] Restrict uploads.

---

## Veteran Understanding

Never trust uploaded files.

Treat every upload as potentially malicious.

---

# 🔥 File System Architecture

```text
Application
      ↓
fs Module
      ↓
Operating System
      ↓
Storage Device
```

---

# 🔥 Upload Architecture

```text
Client
   ↓
Multipart Form
   ↓
Express Route
   ↓
Multer
   ↓
Validation
   ↓
Storage
```

---

# 🔥 Core Concepts Master Checklist

## fs Module

* [ ] Import fs.
* [ ] Explain file operations.

---

## Reading Files

* [ ] Read synchronously.
* [ ] Read asynchronously.
* [ ] Use promises.

---

## Writing Files

* [ ] Create files.
* [ ] Update files.
* [ ] Append data.

---

## Directories

* [ ] Create folders.
* [ ] Read folders.
* [ ] Delete folders.

---

## Uploads

* [ ] Configure multer.
* [ ] Upload files.
* [ ] Validate uploads.

---

# 🧪 Veteran-Level Exercises

## Beginner

* [ ] Notes application.
* [ ] Log file generator.
* [ ] Configuration reader.

---

## Intermediate

* [ ] CSV importer.
* [ ] File explorer API.
* [ ] Document manager.

---

## Advanced

* [ ] Cloud storage integration.
* [ ] Image upload service.
* [ ] File processing pipeline.

---

# ⚠️ Common Beginner Mistakes

* [ ] Using synchronous operations in production.
* [ ] Hardcoding paths.
* [ ] Ignoring upload validation.
* [ ] Loading huge files into memory.
* [ ] Not handling errors.
* [ ] Trusting uploaded file names.

---

# 🏆 Veteran Thinking Questions

* [ ] Why are async file operations preferred?
* [ ] When should streams replace file reads?
* [ ] Why are file uploads security risks?
* [ ] How do cloud providers store files efficiently?
* [ ] What happens when a 10GB file is uploaded?

---

# 📚 Learning Sequence

```text
File System Fundamentals
         ↓
Paths
         ↓
Reading Files
         ↓
Writing Files
         ↓
Directories
         ↓
Metadata
         ↓
Multipart Forms
         ↓
Multer
         ↓
Upload Security
         ↓
Production Storage Systems
```

---

# ✅ Phase Completion Criteria

You have mastered this phase when you can:

* [ ] Explain the fs module.
* [ ] Read and write files.
* [ ] Work with directories.
* [ ] Handle file metadata.
* [ ] Build upload endpoints.
* [ ] Configure multer.
* [ ] Secure file upload systems.

---

# 🚀 Next Phase

```text
Streams
    ↓
Buffers
    ↓
Event Emitters
    ↓
Node Internals
    ↓
Performance Optimization
    ↓
Scalable Backend Systems
```
