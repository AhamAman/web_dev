# 🚀 Node.js Mastery Roadmap

## Phase 14: Monitoring with PM2 – Process Management & Production Reliability

---

# 🎯 Mission of This Phase

Building a Node.js application is easy.

Keeping it alive 24/7 is hard.

Production systems face:

* Crashes
* Memory leaks
* Unexpected errors
* Server restarts
* High traffic spikes

PM2 exists to ensure your application continues running even when problems occur.

---

# 🧠 First Principles Understanding

## Why PM2 Exists

Running Node.js directly:

```bash
node app.js
```

Problem:

```text
Application Crashes
        ↓
Server Stops
        ↓
Users Cannot Access Service
```

---

## Solution

PM2 acts as a supervisor.

```text
PM2
 ↓
Node.js App
```

If the app crashes:

```text
PM2 Detects Failure
         ↓
Automatically Restarts App
```

---

## First Principle

PM2 is not a web server.

PM2 is a:

```text
Process Manager
```

Its job:

```text
Start
Monitor
Restart
Manage
```

Node.js processes.

---

# 🏗 Understanding Process Management

## What is a Process?

When Node.js runs:

```bash
node app.js
```

The operating system creates:

```text
Process
```

---

## Process Lifecycle

```text
Start
 ↓
Running
 ↓
Crash / Exit
 ↓
Stopped
```

---

## Without PM2

```text
Crash
 ↓
Application Offline
```

---

## With PM2

```text
Crash
 ↓
PM2 Detects Failure
 ↓
Restart
 ↓
Application Online
```

---

## Checklist

* [ ] Explain processes.
* [ ] Explain process lifecycle.
* [ ] Explain why process managers exist.

---

## Veteran Insight

Production systems assume failures will happen.

PM2 automates recovery.

---

# 1️⃣ Introduction to PM2

## What is PM2?

PM2 stands for:

```text
Process Manager 2
```

---

## Features

* Process Management
* Auto Restart
* Monitoring
* Logging
* Clustering
* Startup Scripts

---

## Installation

```bash
npm install -g pm2
```

---

## Verify Installation

```bash
pm2 --version
```

---

## Checklist

* [ ] Install PM2.
* [ ] Verify installation.
* [ ] Understand PM2 role.

---

## Veteran Understanding

PM2 is one of the most common Node.js production tools.

---

# 2️⃣ Running Applications with PM2

## Start Application

```bash
pm2 start app.js
```

---

## Result

```text
PM2
 ↓
Manages Process
 ↓
Tracks Health
```

---

## Naming Processes

```bash
pm2 start app.js --name api-server
```

---

## Benefits

* Easier management
* Easier monitoring
* Easier deployments

---

## Checklist

* [ ] Start applications.
* [ ] Assign names.
* [ ] Verify processes.

---

## Veteran Insight

Always name production processes.

---

# 3️⃣ Viewing Running Processes

## List Processes

```bash
pm2 list
```

---

## Example Output

```text
Name        Status
--------------------
api-server  online
worker      online
```

---

## Important Information

PM2 displays:

* Name
* Status
* CPU
* Memory
* Uptime

---

## Checklist

* [ ] View process list.
* [ ] Understand process status.

---

## Veteran Understanding

Monitoring begins with visibility.

---

# 4️⃣ Auto-Restarting Applications

## Problem

Application crashes:

```js
throw new Error("Crash");
```

---

## Without PM2

```text
Application Stops
```

---

## With PM2

```text
Crash
 ↓
Restart
 ↓
Service Restored
```

---

## Restart Policy

PM2 automatically:

```text
Detect
 ↓
Restart
```

failed processes.

---

## Checklist

* [ ] Trigger test crashes.
* [ ] Observe restart behavior.

---

## Veteran Insight

Automatic recovery dramatically improves uptime.

---

# 5️⃣ Managing Applications

## Stop

```bash
pm2 stop api-server
```

---

## Restart

```bash
pm2 restart api-server
```

---

## Reload

```bash
pm2 reload api-server
```

---

## Delete

```bash
pm2 delete api-server
```

---

## Lifecycle Flow

```text
Start
 ↓
Restart
 ↓
Reload
 ↓
Stop
 ↓
Delete
```

---

## Checklist

* [ ] Stop processes.
* [ ] Restart processes.
* [ ] Reload applications.

---

## Veteran Understanding

Reloading can minimize downtime during deployments.

---

# 6️⃣ Monitoring Applications

## Why Monitoring Matters

You need answers to:

```text
Is App Healthy?
Is Memory Growing?
Is CPU High?
```

---

## PM2 Monitor Dashboard

```bash
pm2 monit
```

---

## Displays

* CPU Usage
* Memory Usage
* Event Loop Delay
* Restart Count

---

## Monitoring Flow

```text
Application
      ↓
PM2 Metrics
      ↓
Dashboard
```

---

## Checklist

* [ ] Use pm2 monit.
* [ ] Track resource usage.
* [ ] Identify anomalies.

---

## Veteran Insight

Most production incidents reveal themselves through metrics first.

---

# 7️⃣ Understanding PM2 Logs

## Why Logs Matter

Applications leave evidence.

---

## View Logs

```bash
pm2 logs
```

---

## View Specific Process Logs

```bash
pm2 logs api-server
```

---

## Types of Logs

### Output Logs

```text
console.log()
```

---

### Error Logs

```text
console.error()
```

---

## Checklist

* [ ] View logs.
* [ ] Read errors.
* [ ] Analyze failures.

---

## Veteran Understanding

Logs explain what happened after monitoring reveals a problem.

---

# 8️⃣ PM2 Log Files

## Location

PM2 stores logs automatically.

Example:

```text
~/.pm2/logs
```

---

## Files

```text
api-server-out.log
api-server-error.log
```

---

## Benefits

* Historical records
* Debugging
* Auditing

---

## Checklist

* [ ] Locate logs.
* [ ] Analyze historical data.

---

## Veteran Insight

Logs are often more valuable than stack traces.

---

# 9️⃣ Log Rotation

## Problem

Logs grow forever.

---

## Example

```text
1 MB
 ↓
100 MB
 ↓
1 GB
 ↓
50 GB
```

Disk fills up.

---

## Solution

Log Rotation.

---

## PM2 Module

Install:

```bash
pm2 install pm2-logrotate
```

---

## Function

```text
Large Log
      ↓
Archive
      ↓
New Log
```

---

## Benefits

* Saves disk space
* Improves performance
* Easier management

---

## Checklist

* [ ] Install log rotation.
* [ ] Configure limits.

---

## Veteran Understanding

Ignoring log rotation eventually causes outages.

---

# 🔟 Configuring Log Rotation

## View Settings

```bash
pm2 conf
```

---

## Example Configuration

```bash
pm2 set pm2-logrotate:max_size 10M
```

---

## Retention Example

```bash
pm2 set pm2-logrotate:retain 30
```

---

## Meaning

```text
Keep 30 Archived Logs
```

---

## Checklist

* [ ] Set max log size.
* [ ] Set retention policy.

---

## Veteran Insight

Retention policies balance storage and debugging needs.

---

# 1️⃣1️⃣ Startup Scripts

## Problem

Server Reboots.

PM2 stops.

---

## Solution

Generate startup script.

---

## Command

```bash
pm2 startup
```

---

## Save Current Processes

```bash
pm2 save
```

---

## Flow

```text
Server Reboot
      ↓
PM2 Starts
      ↓
Applications Restore
```

---

## Checklist

* [ ] Configure startup scripts.
* [ ] Save process list.

---

## Veteran Understanding

Production applications should survive reboots automatically.

---

# 1️⃣2️⃣ PM2 Cluster Mode

## Problem

One CPU Core.

```text
Node.js
 ↓
Single Core
```

---

## Solution

Cluster Mode.

---

## Example

```bash
pm2 start app.js -i max
```

---

## Meaning

```text
Use All CPU Cores
```

---

## Architecture

```text
PM2
 ↓
Worker 1
Worker 2
Worker 3
Worker 4
```

---

## Benefits

* Better performance
* Higher throughput
* Improved reliability

---

## Checklist

* [ ] Enable clustering.
* [ ] Understand multi-core execution.

---

## Veteran Insight

Cluster mode is one of the easiest performance wins in Node.js.

---

# 1️⃣3️⃣ Ecosystem Configuration File

## Why Use Ecosystem Files?

Avoid long commands.

---

## Example

```js
module.exports = {
  apps: [
    {
      name: "api",
      script: "./app.js"
    }
  ]
};
```

---

## Start

```bash
pm2 start ecosystem.config.js
```

---

## Benefits

* Repeatable deployments
* Version-controlled configuration

---

## Checklist

* [ ] Create ecosystem file.
* [ ] Manage multiple apps.

---

## Veteran Understanding

Infrastructure should be reproducible.

---

# 🔥 PM2 Production Architecture

```text
Internet
    ↓
Nginx
    ↓
PM2
    ↓
Node.js Application
    ↓
Database
```

---

# 🔥 PM2 Monitoring Pipeline

```text
Application
      ↓
PM2
      ↓
Metrics
      ↓
Logs
      ↓
Dashboard
```

---

# 🔥 PM2 Command Cheat Sheet

## Start

```bash
pm2 start app.js
```

---

## List

```bash
pm2 list
```

---

## Monitor

```bash
pm2 monit
```

---

## Logs

```bash
pm2 logs
```

---

## Restart

```bash
pm2 restart app
```

---

## Stop

```bash
pm2 stop app
```

---

## Delete

```bash
pm2 delete app
```

---

## Startup

```bash
pm2 startup
pm2 save
```

---

# 🔥 Core Concepts Master Checklist

## PM2 Fundamentals

* [ ] Explain PM2.
* [ ] Explain process management.
* [ ] Explain auto-restarts.

---

## Application Management

* [ ] Start apps.
* [ ] Stop apps.
* [ ] Restart apps.

---

## Monitoring

* [ ] Use pm2 monit.
* [ ] Track CPU usage.
* [ ] Track memory usage.

---

## Logging

* [ ] View logs.
* [ ] Analyze errors.
* [ ] Configure storage.

---

## Log Rotation

* [ ] Install pm2-logrotate.
* [ ] Configure retention.

---

## Production Setup

* [ ] Configure startup scripts.
* [ ] Enable cluster mode.
* [ ] Create ecosystem files.

---

# 🧪 Veteran-Level Exercises

## Beginner

* [ ] Run Express app using PM2.
* [ ] Monitor memory usage.
* [ ] Analyze logs.

---

## Intermediate

* [ ] Configure log rotation.
* [ ] Configure startup scripts.
* [ ] Deploy clustered application.

---

## Advanced

* [ ] Multi-service PM2 ecosystem.
* [ ] Blue-green deployment setup.
* [ ] High-availability Node.js infrastructure.

---

# ⚠️ Common Beginner Mistakes

* [ ] Running production apps with node instead of PM2.
* [ ] Ignoring memory usage.
* [ ] Not enabling startup scripts.
* [ ] No log rotation.
* [ ] Not using named processes.
* [ ] Forgetting pm2 save.

---

# 🏆 Veteran Thinking Questions

* [ ] Why is automatic restart essential in production?
* [ ] What problems does cluster mode solve?
* [ ] Why do logs require rotation?
* [ ] How does PM2 improve application availability?
* [ ] What happens when a server reboots unexpectedly?

---

# 📚 Learning Sequence

```text
Process Fundamentals
         ↓
PM2 Installation
         ↓
Running Applications
         ↓
Auto Restarts
         ↓
Process Management
         ↓
Monitoring
         ↓
Logs
         ↓
Log Rotation
         ↓
Startup Scripts
         ↓
Cluster Mode
         ↓
Ecosystem Files
         ↓
Production Operations
```

---

# ✅ Phase Completion Criteria

You have mastered this phase when you can:

* [ ] Explain process management.
* [ ] Run applications with PM2.
* [ ] Configure automatic restarts.
* [ ] Monitor CPU and memory usage.
* [ ] Analyze logs.
* [ ] Configure log rotation.
* [ ] Deploy clustered Node.js applications.

---

# 🚀 Next Phase

```text
Redis
  ↓
Caching
  ↓
Message Queues
  ↓
Background Jobs
  ↓
BullMQ
  ↓
Performance Engineering
  ↓
Scalable Backend Systems
```
