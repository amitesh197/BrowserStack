# BrowserStack

# File Watcher Service

## Overview
This project implements a real-time log-watching service that monitors a log file on a server and streams updates to a web-based client. The client displays new log entries as they are written to the file, without requiring a page refresh. The solution is implemented using Spring Boot and WebSockets to achieve real-time communication between the server and the client.

## Features
- **Real-Time Updates:** The server monitors a log file (`log.txt`) and sends updates to the client whenever new lines are added to the file.
- **WebSocket Communication:** WebSockets are used to push log updates to the client, ensuring that the client receives new data as soon as it becomes available.
- **Simple and Efficient:** The server only transmits new log entries to the client, making the solution efficient in terms of network usage and performance.

## Project Structure

### Backend
- **`DemoApplication.java`:** The main entry point for the Spring Boot application. It enables scheduling for periodic tasks.
- **`FileWatcherService.java`:** This service monitors the log file and sends updates to the client using WebSockets. It checks the file for changes every 100 milliseconds and sends new log entries to the WebSocket destination `/topic/log`.
- **`FileWatcherController.java`:** This controller handles incoming WebSocket messages and relays them to the clients.
- **`WebSocketConfig.java`:** Configures the WebSocket message broker and registers the WebSocket endpoint (`/logs`).

### Frontend
- **`index.html`:** The web client that connects to the WebSocket endpoint and displays real-time log updates. The client subscribes to the `/topic/log` WebSocket destination and dynamically updates the displayed log content.

### Model
- **`Message.java`:** A simple model class used to represent log messages being transmitted between the server and the client.

## How It Works

1. **File Monitoring:** 
   - `FileWatcherService.java` uses a `RandomAccessFile` to read the log file and track its last read position. It periodically checks for new entries and sends any updates to the client via WebSockets.

2. **Real-Time Data Transmission:**
   - The server sends updates to a WebSocket destination (`/topic/log`) which the client subscribes to. As new log entries are detected, they are immediately sent to all connected clients.

3. **Client-Side Rendering:**
   - The `index.html` file includes JavaScript that establishes a WebSocket connection to the server. Once connected, the client listens for messages on the `/topic/log` destination and updates the DOM to display new log entries in real-time.

## Tech Stack
- **Backend:** Java, Spring Boot, WebSockets
- **Frontend:** HTML, JavaScript, SockJS, STOMP.js
- **Build Tool:** Maven (for managing dependencies and building the project)

## Future Scope
- **Initial Load:** The current implementation focuses on real-time updates and but we can implement to display the last 10 lines of the log file when the client first loads the page.

## Instructions for using:

### Open in IntelliJ 

### Go to DemoApplication.java file

### Click on Run button 

### Open localhost:8080 

### Go to terminal Git Bash and enter:
for i in range {1..1000}; do date >> log.txt; sleep 1; done; 

### Refresh the localhost page

### Check inspect -> console ("Connected!!" and Subscribed and then message content appears every second)

### Check inspect -> Network -> websocket file -> check files
