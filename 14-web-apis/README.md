# Web API

## 1. **Geolocation API**

- **Purpose**: Provides the user's geographic location.
- **Key Methods**:
  - `navigator.geolocation.getCurrentPosition(success, error?)`: Fetches current location.
  - `navigator.geolocation.watchPosition(success, error?)`: Tracks location changes.
  - `navigator.geolocation.clearWatch(id)`: Stops tracking.
- **Example**:
  ```javascript
  navigator.geolocation.getCurrentPosition((position) => {
    console.log(position.coords.latitude, position.coords.longitude);
  });
  ```

---

## 2. **Fetch API**

- **Purpose**: Enables making HTTP requests (GET, POST, etc.).
- **Key Features**: Promises-based; simpler than `XMLHttpRequest`.
- **Example**:
  ```javascript
  fetch("https://api.example.com/data")
    .then((response) => response.json())
    .then((data) => console.log(data))
    .catch((error) => console.error(error));
  ```

---

## 3. **Canvas API**

- **Purpose**: Enables drawing graphics and animations on a web page.
- **Key Methods**:
  - `getContext('2d')` for 2D drawing.
  - `fillRect(x, y, width, height)` to draw rectangles.
- **Example**:
  ```javascript
  const canvas = document.getElementById("myCanvas");
  const ctx = canvas.getContext("2d");
  ctx.fillStyle = "blue";
  ctx.fillRect(10, 10, 100, 100);
  ```

---

## 4. **Web Storage API**

- **Purpose**: Provides mechanisms to store data locally.
- **Key Types**:
  - `localStorage`: Persistent storage.
  - `sessionStorage`: Temporary storage (cleared when the tab closes).
- **Example**:
  ```javascript
  localStorage.setItem("key", "value");
  console.log(localStorage.getItem("key"));
  localStorage.removeItem("key");
  ```

---

## 5. **WebSocket API**

- **Purpose**: Establishes a persistent, bidirectional connection with a server.
- **Key Methods**:
  - `WebSocket.send(data)`: Sends data to the server.
  - Event listeners: `onopen`, `onmessage`, `onclose`.
- **Example**:
  ```javascript
  const ws = new WebSocket("wss://example.com/socket");
  ws.onmessage = (event) => console.log(event.data);
  ws.send("Hello Server");
  ```

---

## 6. **File API**

- **Purpose**: Allows reading file data from user input.
- **Key Interfaces**:
  - `File`: Represents individual files.
  - `FileReader`: Reads files.
- **Example**:
  ```javascript
  const input = document.querySelector('input[type="file"]');
  input.addEventListener("change", (event) => {
    const file = event.target.files[0];
    const reader = new FileReader();
    reader.onload = (e) => console.log(e.target.result);
    reader.readAsText(file);
  });
  ```

---

## 7. **Notification API**

- **Purpose**: Displays notifications to the user.
- **Permissions**: Requires user consent.
- **Example**:
  ```javascript
  if (Notification.permission === "granted") {
    new Notification("Hello, User!");
  } else {
    Notification.requestPermission();
  }
  ```

---

## 8. **DeviceOrientation API**

- **Purpose**: Provides information about device motion and orientation.
- **Key Events**:
  - `deviceorientation`: Detects orientation changes.
  - `devicemotion`: Detects motion changes.
- **Example**:
  ```javascript
  window.addEventListener("deviceorientation", (event) => {
    console.log(event.alpha, event.beta, event.gamma);
  });
  ```

---

## 9. **Web Audio API**

- **Purpose**: Provides advanced audio processing and playback features.
- **Key Interfaces**:
  - `AudioContext`: Core interface.
  - `gainNode`: Adjusts volume.
- **Example**:
  ```javascript
  const audioContext = new AudioContext();
  const oscillator = audioContext.createOscillator();
  oscillator.connect(audioContext.destination);
  oscillator.start();
  ```

---

## 10. **Clipboard API**

- **Purpose**: Allows reading from and writing to the clipboard.
- **Key Methods**:
  - `navigator.clipboard.writeText()`
  - `navigator.clipboard.readText()`
- **Example**:
  ```javascript
  navigator.clipboard.writeText("Copied text!");
  navigator.clipboard.readText().then((text) => console.log(text));
  ```

---

## 11. **Intersection Observer API**

- **Purpose**: Detects when elements intersect with a viewport or parent element.
- **Key Methods**:
  - `IntersectionObserver(callback, options)`.
  - `observe()` and `unobserve()`.
- **Example**:
  ```javascript
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) console.log("Visible:", entry.target);
    });
  });
  observer.observe(document.querySelector(".target"));
  ```

---

## 12. **WebRTC API**

- **Purpose**: Enables real-time peer-to-peer communication (video, audio, data).
- **Key Interfaces**:
  - `RTCPeerConnection`.
  - `getUserMedia()`.
- **Example**:
  ```javascript
  navigator.mediaDevices
    .getUserMedia({ video: true })
    .then((stream) => (videoElement.srcObject = stream))
    .catch((error) => console.error(error));
  ```

# Web Worker

## 🧠 1. What Are Web Workers?

> Web Workers let you run **JavaScript in the background**, on a **separate thread** from the main UI thread.

✅ Prevents blocking the main thread during:

- Heavy computations (e.g., image processing, sorting)
- Data parsing (e.g., large JSON, CSV)
- Repetitive loops
- WebSocket/REST polling

---

## 🧵 2. Why Use Web Workers?

| Reason                | Benefit                                 |
| --------------------- | --------------------------------------- |
| Non-blocking UI       | Keeps the interface responsive          |
| Background processing | Offload CPU-heavy work from main thread |
| Better performance    | Avoids "Page Unresponsive" errors       |
| Parallelism           | Utilizes multi-core CPUs                |

---

## 🛠️ 3. Types of Workers

| Type               | Description                                 |
| ------------------ | ------------------------------------------- |
| **Dedicated**      | One page ↔ one worker                       |
| **Shared**         | Multiple scripts/tabs share the same worker |
| **Service Worker** | Acts as a proxy (offline caching, push)     |

For UI tasks, we mostly use **Dedicated Web Workers**.

---

## 📦 4. Web Worker Architecture (Flow)

```txt
Main Thread
   |
   | postMessage()
   ↓
[ Worker.js ]
   ↑
   | postMessage()
   |
Main Thread (onmessage)
```

---

## 📄 5. Web Worker File (`worker.js`)

```js
// worker.js
self.onmessage = function (e) {
  const result = heavyCalculation(e.data);
  self.postMessage(result);
};

function heavyCalculation(data) {
  // simulate CPU work
  return data * 2;
}
```

---

## 📥 6. Main Thread Script

```js
const worker = new Worker("worker.js");

worker.postMessage(5); // send data to worker

worker.onmessage = function (e) {
  console.log("Received from worker:", e.data);
};

worker.onerror = function (e) {
  console.error("Worker error:", e.message);
};
```

---

## 🧪 7. Real-World Use Cases

| Use Case                 | Description                      |
| ------------------------ | -------------------------------- |
| Image/Video processing   | Filters, resizing, compression   |
| Data parsing             | CSV/JSON parsing, log analysis   |
| Math-heavy operations    | Physics simulations, games       |
| Background fetch/polling | Avoid blocking fetch retry loops |
| Real-time calculations   | Large dataset computations       |

---

## 🧩 8. Transferring Data Efficiently

Large data = slow `postMessage`.

Use **Transferable Objects** (no copy, just transfer memory reference):

```js
const buffer = new ArrayBuffer(1024);
worker.postMessage(buffer, [buffer]); // faster!
```

---

## 🧱 9. Limitations of Web Workers

| Limitation                | Detail                             |
| ------------------------- | ---------------------------------- |
| No DOM access             | Cannot access `document`, `window` |
| No alert, confirm, prompt | Only standard JS + fetch APIs      |
| File must be same-origin  | Unless CORS headers allow it       |
| Slight overhead to spawn  | Don’t use for trivial tasks        |

---

## ⚙️ 10. Terminating a Worker

```js
worker.terminate(); // stops the worker
```

Also, inside the worker you can do:

```js
self.close(); // worker self-destructs
```

---

## 🧰 11. Inline Worker via Blob (no separate file)

```js
const blob = new Blob(
  [
    `
  onmessage = e => postMessage(e.data * 10);
`,
  ],
  { type: "application/javascript" }
);

const worker = new Worker(URL.createObjectURL(blob));
worker.postMessage(7);
worker.onmessage = (e) => console.log(e.data); // 70
```

✅ Useful for dynamic workers in single-page apps.

---

## 📦 12. Using Web Workers in Modern Frameworks

| Framework       | Integration                                                |
| --------------- | ---------------------------------------------------------- |
| **React**       | Use via Webpack loader, Vite plugin, or `workerize-loader` |
| **Vue/Angular** | Similar via plugins or file separation                     |
| **Next.js**     | Requires custom Webpack config for worker file export      |

Example:

```ts
// worker.js
export default function () {
  self.onmessage = (e) => self.postMessage(e.data * 3);
}
```

---

## 🚀 13. Debugging Web Workers

- Use **Chrome DevTools → Sources → Workers**
- You can:

  - Inspect scripts
  - Add breakpoints
  - Log messages using `console.log()` inside worker

---

## 🧠 14. Best Practices

✅ Name your worker threads descriptively
✅ Always check browser support (`window.Worker`)
✅ Use `Transferable` for large data
✅ Cleanup unused workers with `terminate()`
✅ Keep worker logic focused and decoupled

---

## 🔍 15. Browser Support

| Browser    | Support            |
| ---------- | ------------------ |
| Chrome     | ✅ Full            |
| Firefox    | ✅ Full            |
| Safari     | ✅ Full            |
| Edge/Opera | ✅ Full            |
| IE         | ⚠️ Partial / buggy |

---

## 🧪 Summary Cheatsheet

| Concept         | Syntax / Example                   |
| --------------- | ---------------------------------- |
| Create Worker   | `new Worker('worker.js')`          |
| Send Data       | `worker.postMessage(data)`         |
| Receive Data    | `worker.onmessage = (e) => {}`     |
| Inside Worker   | `self.onmessage = (e) => {}`       |
| Terminate       | `worker.terminate()`               |
| Transfer Buffer | `postMessage(buffer, [buffer])`    |
| No DOM Access   | Use fetch, math, memory, etc. only |
