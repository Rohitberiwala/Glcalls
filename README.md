# GLCalls (Global Live Calls)

<p align="center">
  <strong>Universal Bidirectional Real-Time AI Voice Translation Over Real Phone Networks (PSTN)</strong>
</p>

<p align="center">
  <a href="https://github.com/Rohitberiwala/Glcalls/releases/latest"><img src="https://img.shields.io/badge/Download_APK-v1.0.0--beta-success?style=for-the-badge&logo=android" alt="Download APK"></a>
  <a href="https://github.com/Rohitberiwala/Glcalls/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="License: MIT"></a>
  <img src="https://img.shields.io/badge/Latency-%3C500ms_Glass--to--Glass-brightgreen?style=for-the-badge" alt="Latency">
  <img src="https://img.shields.io/badge/Telephony-PSTN_%7C_G.711_μ--law-orange?style=for-the-badge" alt="Telephony">
  <img src="https://img.shields.io/badge/Callee_Requirement-0_Apps_%7C_0_Internet-red?style=for-the-badge" alt="Callee Requirement">
</p>

---

## Overview

**GLCalls** (*Global Live Calls / Global Calls Translate*, developed by [Luvent Technologies](https://voxsync.theluvent.com)) is an enterprise-grade AI telephony translation platform. 

It enables an Android caller to dial **any standard cellular phone or landline anywhere in the world** and speak in their native language (e.g., Punjabi, Hindi, Spanish, French). The person on the other end hears natural speech translated into their language in **under 500ms**.

### The Breakthrough: Zero-App Callee Experience
Unlike WhatsApp, Zoom, Google Meet, or Microsoft Teams:
* **The person receiving your call needs NO smartphone, NO application, and NO internet connection.**
* They answer a standard cellular or landline phone call over regular PSTN carrier networks.
* Translation operates bidirectionally in full duplex with acoustic hangover isolation.

---

## Download Android Client (Live Beta)

The Android Client is currently in open beta. Direct binary installation is available via GitHub Releases:

### [Download GLCalls APK v1.0.0-beta](https://github.com/Rohitberiwala/Glcalls/releases/latest)

> **Package Details:**
> * **File:** `Glcalls.apk` (~61 MB)
> * **Architecture:** Universal ARM64-v8a / armeabi-v7a
> * **Minimum Android OS:** Android 8.0 (API level 26) or higher
> * **Permissions Required:** Microphone (audio streaming), Internet (carrier signaling)

#### How to Install:
1. Download `Glcalls.apk` onto your Android device from the link above.
2. Tap the downloaded APK in your Downloads manager.
3. If prompted by Android, tap **Settings** and allow **"Install unknown apps"** for your browser or file manager.
4. Tap **Install** and open the application.
5. Grant Microphone access to initiate live translation calls.

---

## Technical Architecture & Pipeline

```text
[ Android App Caller ]
        │  (Linear PCM 16kHz via WebSocket)
        ▼
[ Node.js Telephony Orchestrator ] ◄───► [ Twilio PSTN Gateway ] ◄───► [ Callee Regular Phone ]
        │                                 (G.711 μ-law 8kHz)             (Landline / Mobile)
        ├──► Deepgram Nova-2 STT (150ms endpointing)
        │         │
        │         ▼ (Streamed Text Tokens)
        ├──► Groq LLaMA-3.3 70B / Qwen 2.5 (Sub-200ms Neural Translation)
        │         │
        │         ▼ (Translated Tokens)
        ├──► Cartesia Sonic TTS (<150ms Neural Voice Synthesis)
        │         │
        └─────────┴──► Outbound G.711 Audio Stream (Injected into Twilio Leg)
```

| Pipeline Stage | Technology | Specification / Latency |
| :--- | :--- | :--- |
| **Telephony Ingress** | Twilio Media Streams | G.711 μ-law (PCMU), 8000 Hz mono, 20ms audio frames |
| **Speech-to-Text (STT)** | Deepgram Nova-2 | Streaming WebSocket, 150ms endpointing, automated punctuation |
| **Neural Translation** | Groq Cloud LPU | LLaMA-3.3-70B / Qwen-2.5-72B streaming inference (<200ms) |
| **Voice Synthesis (TTS)** | Cartesia Sonic-3.5 | Telephony-native PCM/μ-law streaming (<150ms first audio byte) |
| **Echo Suppression** | Custom Acoustic Hangover Guard | 1200ms bidirectional isolation window to prevent audio bleed |
| **End-to-End Latency** | Full Streaming Pipeline | **350ms – 550ms glass-to-glass average** |

---

## Supported Languages (50+ Bidirectional Pairs)

GLCalls supports direct neural corridors and high-speed English-pivot routing across all major global language families:

* **South Asian / Indic:** Punjabi (ਪੰਜਾਬੀ), Hindi (हिन्दी), Bengali (বাংলা), Tamil (தமிழ்), Telugu (తెలుగు), Marathi (मराठी), Gujarati (ગુજરાતી), Urdu (اردو), Kannada (ಕನ್ನಡ), Malayalam (മലയാളം).
* **European:** English, Spanish, French, German, Italian, Portuguese, Dutch, Polish, Russian, Swedish, Danish, Ukrainian, Greek, Romanian.
* **East & Southeast Asian:** Mandarin Chinese, Cantonese, Japanese, Korean, Vietnamese, Tagalog/Filipino, Indonesian, Thai.
* **Middle Eastern & African:** Arabic (Gulf, Levantine, Egyptian, Maghrebi), Turkish, Persian/Farsi, Hebrew, Swahili.

---

## Privacy & Zero-Retention Security

GLCalls is engineered with privacy as a foundational constraint:
* **Ephemeral In-Memory Buffers:** Audio frames are processed entirely in transient RAM buffers and are discarded immediately after translation.
* **No Audio Storage:** Audio data is **never** written to persistent disk, databases, or cloud buckets.
* **Zero Call Recording:** In-call voice recording is disabled by default.
* **Security Policy:** Read our full [SECURITY.md](SECURITY.md) for vulnerability disclosure standards.

---

## Leadership & Operational Transparency

* **Founder & Lead AI Systems Architect:** Rohit Sharma (Rohit Beriwala)
* **LinkedIn:** [linkedin.com/in/rohit-beriwala](https://www.linkedin.com/in/rohit-beriwala/)
* **GitHub:** [github.com/Rohitberiwala](https://github.com/Rohitberiwala)
* **Corporate Website:** [voxsync.theluvent.com](https://voxsync.theluvent.com)
* **Contact:** `contact@theluvent.com`

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
