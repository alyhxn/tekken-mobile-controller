## Tekken 3 - WebRTC Mobile Controller

A lightweight, browser-based multiplayer setup for Tekken 3. This project turns your desktop browser into an arcade machine using EmulatorJS, while instantly transforming your mobile devices into wireless gamepads via WebRTC. All of this is achieved without a backend server, using PeerJS for peer-to-peer communication.

![Tekken 3 Gameplay and Mobile Controller](/demo.png)

![Tekken 3 Mobile Controller](/controller.png)

### Live Demo
**Play here:** [https://alyhxn.github.io/tekken-mobile-controller/](https://alyhxn.github.io/tekken-mobile-controller/)

---

### Key Features
* **Zero-Install Controller:** Scan a QR code with your phone to instantly join the game. No app downloads required.
* **Low Latency Input:** Uses WebRTC data channels for real-time, peer-to-peer button inputs.
* **Smart UI Routing:** A single HTML file serves both the Host (Emulator) and the Client (Mobile Gamepad) dynamically based on URL parameters.
* **Haptic Feedback:** Mobile controllers vibrate on connection to confirm pairing.
* **Responsive Gamepad:** Built with pointer events to support multi-touch and prevent sticky buttons.
* **Auto-Mapped Controls:** Automatically maps Player 1 and Player 2 virtual inputs to the corresponding EmulatorJS keyboard controls.

---

### How It Works

This project handles two distinct environments within a single codebase:

**1. The Host (Laptop/Desktop)**
When the page is loaded without any URL parameters, it acts as the Host. It initializes a PeerJS connection, fetches a unique ID, and generates two QR codes (for Player 1 and Player 2). It also loads EmulatorJS and the Tekken 3 ROM. The Host continuously listens for incoming WebRTC data and translates mobile button presses into virtual `KeyboardEvent` triggers that EmulatorJS understands.

**2. The Client (Mobile Device)**
When a user scans a QR code, they are directed to the same URL but with a `?join=` parameter containing the Host's PeerJS ID. The code detects this parameter, hides the emulator interface, and renders a touch-friendly gamepad. It establishes a WebRTC connection to the Host and sends button state data (`keydown` / `keyup`) as JSON objects.

---

### Tech Stack
* **HTML/CSS/JS:** Core frontend technologies.
* **PeerJS:** Wrapper for WebRTC to handle peer-to-peer data connections.
* **QRCode.js:** Renders the dynamic QR codes for easy mobile pairing.
* **EmulatorJS:** The browser-based emulation engine running the PlayStation core (`psx`).

---

### Local Development / Setup

To run this project locally, you will need a local web server (due to CORS and WebRTC requirements) and the actual game ROM/BIOS.

1. Clone the repository.
2. Place your `tekken3.chd` (game ROM) and `scph5501.bin` (BIOS) in the root directory alongside the HTML file.
3. Serve the directory using a local web server. 
    * *Example using Python: `python -m http.server 8000`*
    * *Example using Node.js: `npx serve`*
4. Open your local IP address in your desktop browser.
5. Scan the generated QR codes with your mobile device on the same network.
