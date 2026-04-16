# VGT CHRONOS BETA 1.0 

[![License](https://img.shields.io/badge/License-AGPLv3-green?style=for-the-badge)](LICENSE)
[![Version](https://img.shields.io/badge/Version-1.1_BETA-brightgreen?style=for-the-badge)](#)
[![Target](https://img.shields.io/badge/Target-Wordpress-FCC624?style=for-the-badge&logo=Wordpress)](#)
[![Language](https://img.shields.io/badge/Language-PHP-00ADD8?style=for-the-badge&logo=php)](#)
[![VGT](https://img.shields.io/badge/VGT-VisionGaiaTechnology-red?style=for-the-badge)](https://visiongaiatechnology.de)

# ⚠️ EXPERIMENTAL R&D PROJECT

This project is a **Proof of Concept (PoC)** and part of ongoing research and development at
VisionGaia Technology. It is **not** a certified or production-ready product.

**Use at your own risk.** The software may contain security vulnerabilities, bugs, or
unexpected behavior. It may break your environment if misconfigured or used improperly.

**Do not deploy in critical production environments** unless you have thoroughly audited
the code and understand the implications. For enterprise-grade, verified protection,
we recommend established and officially certified solutions.

Found a vulnerability or have an improvement? **Open an issue or contact us.**

## 🔍 What is VGT Chronos?

The VGT Chronos Engine is an uncompromising countdown system for WordPress, engineered for extreme performance and security. Moving away from the overhead of traditional page-builder modules, Chronos is based on a native Vanilla-JS physics engine (60FPS Render Loop) and isolated backend instances.


<img width="1724" height="878" alt="{185DC291-D873-4469-8745-801682F2DDA0}" src="https://github.com/user-attachments/assets/13645832-db1f-4d51-a690-14ac80141706" />





| Specification | Parameter |
| --- | --- |
| Minimum PHP Version | 8.1 (Enforces strict_types=1) |
| Dependencies (Backend) | WordPress Core Functions |
| Dependencies (Frontend) | Zero-Dependency (No jQuery, No React/Vue) |
| Architectural Pattern | Singleton Bootstrapper, Namespaced Isolation (VGT\Chronos) |
| Database Engine | Custom Table via dbDelta (wp_vgt_countdowns) |

## ⚡2. CORE ARCHITECTURE & PERFORMANCE

2.1 Rendering & Physics Engine

60FPS Render Loop: Client-side animations exclusively utilize requestAnimationFrame for hardware acceleration. Complete avoidance of I/O-blocking setInterval routines for the tick cycle.

Absolute Time Synchronization: Elimination of JavaScript date-parsing errors. Target time is pre-calculated on the PHP server in absolute Unix epoch milliseconds, eliminating cross-timezone desynchronization.

Zero-Runtime Overhead: Styles are processed as dynamic inline CSS via wp_add_inline_style. No blocking network requests for external stylesheets in the frontend.

Evergreen Persistence: Local state persistence for persistent evergreen timers via localStorage (vgt_chronos_{id}_start).

2.2 Security KERNEL (Defense-in-Depth)

Strict Whitelisting: All UI parameters (Themes, Actions, Types) are validated server-side against constant arrays (in_array(..., ..., true)).

Input Sanitization: Absolute data cleaning prior to DB insertion (sanitize_text_field, absint, sanitize_hex_color, esc_url_raw).

Query Hardening: Uncompromising use of Prepared Statements ($wpdb->prepare and formatting arrays %s, %d).

Mutation Protection: Every write/delete operation is secured via current_user_can('manage_options') and cryptographic nonces (wp_verify_nonce).

## 🗄️ 3. DATABASE SCHEMA

Prefix-dynamic table: {prefix}vgt_countdowns

| Column | Type | Attributes | Function |
| --- | --- | --- | --- |
| id | bigint(20) unsigned | NOT NULL, AUTO_INCREMENT, PK | Unique System Identifier |
| title | varchar(255) | NOT NULL | Internal System Designation |
| type | varchar(50) | DEFAULT 'fixed' | Logic: fixed or evergreen |
| end_datetime | varchar(50) | NULL | ISO 8601 Termination Timestamp |
| duration_seconds | int(11) unsigned | NULL | Runtime in seconds for Evergreen |
| action_on_expire | varchar(50) | DEFAULT 'hide' | Post-Expiration Action (hide, redirect) |
| redirect_url | varchar(2048) | NULL | Target URL for Redirect Action |
| design_settings | json | NOT NULL | Scalable storage for UI payload |
| created_at | datetime | DEFAULT CURRENT_TIMESTAMP | Creation Timestamp |

## 🎨 4. UI/UX CONFIGURATION MATRIX

#### 4.1 Visual Engines (Themes)

```bash
→ blocks:       Solid Blocks (Default)
→ cyber:        Cyber Neon
→ minimal:      Minimal Line
→ matrix:       Digital Matrix
→ glass:        Glassmorphism
→ neon-pulse:   Neon Pulse
```

#### 4.2 Tick Animations (GPU-Accelerated)

| Animation | Effect |
| --- | --- |
| none | Zero Motion (Static) |
| pulse | Cyber Pulse (Scaling + Glow) |
| flip | 3D Mechanical Flip (Split-Flap System) |
| slide | Digital Slide (Vertical Translation) |
| glitch | System Glitch (RGB-Split Translation) |

#### 4.3 Post-Expiration Protocol

hide (Purge): Injects .vgt-timer-hidden (Enforces CSS display: none !important).

redirect (Force): Executes window.location.replace() to overwrite the browser history stack, preventing users from "glitching back" into the expired state.

#### 4.4 Dashboard Engine

Live Preview Canvas: Reactive Vanilla JS DOM-binding synchronizes inputs (colors, animations, languages) instantly in real-time. No page reloads.

Tick Simulation: An isolated tick interval in the admin area visualizes animations with perfect asynchrony, independent of real time.

## 💰 Support the Project

[![Paypal](https://img.shields.io/badge/Paypal-Donate_Via_Paypal-blue?style=for-the-badge&logo=Paypal)](https://www.paypal.com/paypalme/dergoldenelotus)

| Methode | Address |
| --- | --- |
| Bitcoin | bc1q3ue5gq822tddmkdrek79adlkm36fatat3lz0dm |
| ETH | 0xD37DEfb09e07bD775EaaE9ccDaFE3a5b2348Fe85 |
| USDT (ERC-20) | 0xD37DEfb09e07bD775EaaE9ccDaFE3a5b2348Fe85 |



## 🔗 VGT Ecosystem

| Tool | Type | Purpose |
|---|---|---|
| ⚔️ **[VGT Sentinel](https://github.com/visiongaiatechnology/sentinelcom)** | **WAF / IDS Framework** | Zero-Trust WordPress security suite  |
| 🛡️ **[VGT Myrmidon](https://github.com/visiongaiatechnology/vgtmyrmidon)** | **ZTNA** | Zero Trust device registry and cryptographic integrity verification |
| ⚡ **[VGT Auto-Punisher](https://github.com/visiongaiatechnology/vgt-auto-punisher)** | **IDS** | L4+L7 Hybrid IDS — attackers terminated before they even knock |
| 📊 **[VGT Dattrack](https://github.com/visiongaiatechnology/dattrack)** | **Analytics** | Sovereign analytics engine — your data, your server, no third parties |
| 🌐 **[VGT Global Threat Sync](https://github.com/visiongaiatechnology/vgt-global-threat-sync)** | **Preventive** | Daily threat feed — block known attackers before they arrive |
| 🔥 **[VGT Windows Firewall Burner](https://github.com/visiongaiatechnology/vgt-windows-burner)** | **Windows** | 280,000+ APT IPs in native Windows Firewall |

## 🤝 Contributing

Pull requests are welcome. For major changes, open an issue first.

Licensed under **AGPLv3** — *"For Humans, not for SaaS Corporations."*

---

## 🏢 Built by VisionGaia Technology

[![VGT](https://img.shields.io/badge/VGT-VisionGaia_Technology-red?style=for-the-badge)](https://visiongaiatechnology.de)

VisionGaia Technology builds enterprise-grade security infrastructure — engineered to the DIAMANT VGT SUPREME standard.
