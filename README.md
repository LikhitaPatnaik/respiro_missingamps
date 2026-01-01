# 🫁 Respiro: The Winter Health Shield

> **Missing Amps Winter Classic 2025 Submission**
> *Turning sound waves ("Amps") into actionable health insights.*

<img width="1240" height="914" alt="image" src="https://github.com/user-attachments/assets/9e466a67-ac12-4872-9616-5775fca229f2" />

## 🥶 The Inspiration
Winter 2025 brings beautiful weather, but it also brings the "Winter Smog" and respiratory illnesses. In urban areas (like Visakhapatnam), the Air Quality Index (AQI) often spikes during winter, but people ignore it until they get sick.

We wanted to solve the **"Missing Amps"** challenge by interpreting "Amps" as **Audio Amplitude**. Respiro uses the *amplitude* of your breath to detect health issues that are often invisible (or "missing") to the naked eye.

## 🚀 What it Does
Respiro is a dual-engine health monitor that runs entirely in the browser:

1.  **Hyper-Local Air Analysis:**
    *   It doesn't just guess your city; it uses **GPS** and **OpenStreetMap (Nominatim)** to find your exact suburb (e.g., "Madhurawada, Visakhapatnam").
    *   It pulls real-time **PM2.5 data** via the OpenWeatherMap API.
    *   It translates technical numbers into human-friendly terms (e.g., "Hazy" instead of "Poor") using **CPCB Standards**.

2.  **Bio-Acoustic Lung Monitor:**
    *   Using the native **Web Audio API**, the app listens to your breathing patterns.
    *   It uses a **Spike Detection Algorithm** to differentiate between heavy breathing (slow rise) and coughing (sudden amplitude spike).
    *   It correlates your biological data (Coughing) with environmental data (Smog) to generate a custom health report.

3.  **Atmospheric UI:**
    *   The app interface changes color dynamically based on the air quality (Green for Fresh, Orange for Hazy, Red for Hazardous), giving immediate visual feedback.

## ⚙️ How We Built It
We focused on a lightweight, privacy-first approach. No audio is ever sent to a server; everything is processed locally on the client.

*   **Frontend:** React.js + Vite
*   **Styling:** CSS3 with Glassmorphism & Dynamic Gradients
*   **Sensors:** Navigator Geolocation API + Web Audio API (AnalyserNode)
*   **Data Sources:**
    *   *Pollution:* OpenWeatherMap Air Pollution API
    *   *Reverse Geocoding:* OpenStreetMap (Nominatim)

## 🧠 The "Smart" Audio Logic
We initially tried using heavy AI models (TensorFlow/YAMNet) but found them too slow for a seamless web experience. We switched to a custom **Amplitude Spike Algorithm**:

// Simplified Logic:
const volumeSpike = currentVolume - lastVolume;

// We look for a SUDDEN spike (>20) combined with high volume (>50).
// This filters out wind noise and talking, isolating the "percussive" sound of a cough.
if (currentVolume > 50 && volumeSpike > 20) {
  triggerCoughAlert();
}
