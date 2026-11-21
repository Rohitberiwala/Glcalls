# Security Policy

## Supported Versions

GLCalls actively maintains security updates and patches for the following versions:

| Version | Supported | Status |
| :--- | :---: | :--- |
| `v1.0.x-beta` | :white_check_mark: | Active Beta |
| `< 1.0.0` | :x: | Deprecated |

---

## Architectural Security Commitments

### 1. Ephemeral Voice Processing (Zero Retention)
* **Zero Audio Persistence:** Real-time telephony audio captured over Twilio Media Streams (G.711 μ-law, 8000Hz mono) is processed purely in volatile memory buffers. Audio data is never written to persistent disk storage, temporary files, or secondary databases.
* **Immediate Deletion:** Audio chunks and intermediate speech-to-text / text-to-speech payloads are purged immediately after pipeline delivery (<500ms cycle).
* **Zero Call Recording:** In-call voice recording is disabled by default across all infrastructure endpoints.

### 2. Transport & Telephony Encryption
* All client-to-server and server-to-carrier WebSocket connections enforce **TLS 1.3** encryption (`wss://`).
* Standard PSTN ingress/egress utilizes authenticated Twilio voice gateways with cryptographic webhook signature validation (`X-Twilio-Signature`).
* Third-party AI model streaming interfaces (Deepgram Nova-2, Groq Cloud, Cartesia Sonic) communicate exclusively over secure, authenticated TLS tunnels.

---

## Reporting a Vulnerability

We prioritize platform security, caller privacy, and telephony infrastructure integrity. If you discover a vulnerability or security issue:

1. **Do NOT open a public GitHub Issue.**
2. Send an email with vulnerability details, steps to reproduce, and attack surface analysis to:
   - **Security Team:** `contact@theluvent.com`
   - **Founder:** `rohit@theluvent.com`
3. Include:
   - Description of the vulnerability and affected component.
   - Proof-of-concept (PoC) code or exact steps to reproduce.
   - Potential impact of the issue.

### Remediation Timeline
* **Initial Response:** Within 24–48 hours of report receipt.
* **Vulnerability Assessment & Triage:** Within 5 business days.
* **Patch Deployment:** Critical vulnerabilities are addressed within 7 business days.
* **Public Disclosure:** Coordinated disclosure occurs only after an official patch has been released.
