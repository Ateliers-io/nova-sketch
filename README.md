# NovaSketch — Real-Time Collaborative Workspace

NovaSketch is a distributed digital canvas and creative workspace built to facilitate seamless, real-time co-creation between remote users. This repository serves as the **Main Orchestrator**, managing both the frontend and backend architectures as submodules to provide a unified development environment.

## 🏗️ Project Structure

NovaSketch is organized into two primary sub-systems:

* **[Frontend (novasketch-frontend)](https://www.google.com/search?q=ateliers-io/novasketch-frontend/novasketch-frontend-c003cf4cf4feb04b10a6c395ac33746a0ae432f4/package.json)**: A React-based collaborative interface using Konva.js for high-performance canvas rendering.
* **[Backend (novasketch-backend)](https://www.google.com/search?q=ateliers-io/novasketch-backend/novasketch-backend-ff30925c68d3bd5ec08802f589b2ffe08cad8ead/package.json)**: A Node.js environment handling Yjs-based synchronization, WebSocket messaging, and MongoDB persistence.

---

## 🛠️ Backend Architecture & Capabilities

The backend serves as the authoritative synchronization engine for the collaborative workspace.

### **1. Real-Time Synchronization Engine**

* **CRDT-Based Consistency**: Implements **Yjs** to ensure conflict-free data replication across all connected clients.
* **Awareness Protocol**: Manages ephemeral user data, such as live cursor positions and active selection states, through the `y-protocols/awareness` standard.
* **Optimized WebSocket Messaging**: Categorizes communication into specific message types:
* **Type 0 (Sync)**: Synchronizes the document state.
* **Type 1 (Awareness)**: Handles live user presence.
* **Type 2 (Broadcast)**: Optimized for high-frequency updates like object dragging.
* **Type 3 (Property Updates)**: Manages validated transformations like resizing and rotation.



### **2. Data Persistence & Room Management**

* **Dynamic Room Allocation**: Automatically creates or loads rooms based on the URL path, allowing for infinite isolated shared canvases.
* **Binary State Persistence**: Saves the Yjs document state as binary buffers in **MongoDB**.
* **Debounced Auto-Save**: Utilizes a 2000ms debounced save mechanism to ensure data integrity without over-taxing the database during intense creative sessions.

### **3. Security & Validation**

* **Authentication**: Integrated with **Passport.js** and **Google OAuth 2.0** for secure user identity.
* **State Integrity**: Includes server-side property validation to sanitize incoming transformations before they are broadcast to other clients.

---

## ⚙️ Getting Started

### **Prerequisites**

* **Node.js**: Version 20 or higher.
* **pnpm**: Version 10.28.2 or higher.
* **MongoDB**: An active instance for canvas state persistence.

### **Installation**

1. **Clone the Main Repo with Submodules**:
```bash
git clone --recurse-submodules <repository-url>
cd nova-sketch

```


2. **Initialize Submodules (if cloned without recurse)**:
```bash
git submodule update --init --recursive

```


3. **Setup Backend**:
```bash
cd novasketch-backend
pnpm install
# Configure your .env (see Backend .env.example)
pnpm dev

```


4. **Setup Frontend**:
```bash
cd ../novasketch-frontend
pnpm install
# Configure your .env (see Frontend .env.example)
pnpm dev

```



---

## 🛡️ License

This project is licensed under the **ISC License**.
