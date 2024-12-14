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
