# QR Hotel Review System

A mobile-first web app that lets guests write a review once and post it to multiple platforms (Google, TripAdvisor, Booking) via a single QR code scan.

## How It Works

1. **Write:** Guest types a review on their phone.
2. **Select:** Guest chooses a platform (e.g., Google Maps).
3. **Copy & Go:** Clicking the button automatically **copies the text** to the clipboard and opens the review site.
4. **Paste:** Guest pastes and submits.

## Project Structure

```text
.
├── index.html        # Main UI and Configuration
├── script.js         # Clipboard logic & state management
└── images/           # Assets (Backgrounds)

```

## Configuration

Open `index.html` to customize the hotel details:

### 1. Update Review Links

Find the checkboxes in the HTML and replace the `data-url` with your specific hotel links:

```html
<input type="checkbox" data-url="YOUR_GOOGLE_MAPS_LINK_HERE" ... />

```

### 2. Update Branding

* **Logo:** Replace the `<svg>` inside `#hotelLogo` or swap it for an `<img>` tag.
* **Background:** Replace `images/the-riada-hotel.jpg`.

## 🚀 Deployment

* **Static Hosting:** Works on any standard web server (Apache, Nginx, Netlify, Vercel).
* **HTTPS Required:** The site **must** be served over HTTPS. Modern browsers block the `Clipboard API` (Copy function) on insecure HTTP connections.

##  Tech Stack

* **HTML5 / Vanilla JS**
* **Tailwind CSS** (via CDN)

---

> **About This Project** > This system was developed as a lightweight, easily customizable reviewing solution for hotels. It is designed to be a "drop-in" tool that requires zero backend infrastructure, allowing hotel managers to improve their online presence with minimal technical effort.
