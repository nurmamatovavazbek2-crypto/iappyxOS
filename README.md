package com.milliysertifikat.ustoz;

import android.app.*;
import android.os.*;
import android.graphics.Color;
import android.content.*;
import android.view.*;
import android.widget.*;
import java.util.*;

public class MainActivity extends Activity {

    LinearLayout main;
    TextView title;

    String[] subjects = {
        "📚 Tarix",
        "➗ Matematika",
        "🇬🇧 Ingliz tili",
        "📖 Ona tili va adabiyot",
        "⚗️ Kimyo",
        "🧬 Biologiya",
        "⚡ Fizika",
        "🇷🇺 Rus tili",
        "🇰🇷 Koreys tili",
        "🇹🇷 Turk tili"
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        showHome();
    }

    void showHome() {
        main = new LinearLayout(this);
        main.setOrientation(LinearLayout.VERTICAL);
        main.setPadding(30,30,30,30);
        main.setBackgroundColor(Color.WHITE);

        title = new TextView(this);
        title.setText("🎓 MILLIY SERTIFIKAT USTOZ");
        title.setTextSize(25);
        title.setTextColor(Color.BLACK);
        title.setGravity(Gravity.CENTER);
        title.setPadding(10,20,10,30);

        main.addView(title);

        TextView subtitle = new TextView(this);
        subtitle.setText(
            "Milliy sertifikat imtihoniga tayyorgarlik platformasi"
        );
        subtitle.setTextSize(17);
        subtitle.setGravity(Gravity.CENTER);
        subtitle.setPadding(10,0,10,30);

        main.addView(subtitle);

        Button diagnostic = new Button(this);
        diagnostic.setText("📝 Diagnostik test");
        main.addView(diagnostic);

        Button ai = new Button(this);
        ai.setText("🤖 AI Ustoz");
        main.addView(ai);

        TextView fanTitle = new TextView(this);
        fanTitle.setText("Fanlardan birini tanlang:");
        fanTitle.setTextSize(20);
        fanTitle.setTextColor(Color.BLACK);
        fanTitle.setPadding(0,30,0,15);

        main.addView(fanTitle);

        for(String subject : subjects) {
            Button b = new Button(this);
            b.setText(subject);
            b.setTextSize(17);

            b.setOnClickListener(v -> showSubject(subject));

            main.addView(b);
        }

        diagnostic.setOnClickListener(v -> startTest("📋 Diagnostik test"));

        ai.setOnClickListener(v -> showAI());

        setContentView(main);
    }

    void showSubject(String subject) {

        main.removeAllViews();

        TextView t = new TextView(this);
        t.setText(subject);
        t.setTextSize(26);
        t.setTextColor(Color.BLACK);
        t.setGravity(Gravity.CENTER);
        t.setPadding(10,30,10,30);

        main.addView(t);

        String[] topics = {
            "📌 1-mavzu",
            "📌 2-mavzu",
            "📌 3-mavzu",
            "📝 Test ishlash",
            "🎯 Imtihon rejimi"
        };

        for(String topic : topics) {

            Button b = new Button(this);
            b.setText(topic);
            b.setTextSize(17);

            b.setOnClickListener(v -> {

                if(topic.contains("Test"))
                    startTest(subject);

                else if(topic.contains("Imtihon"))
                    startTest("🎯 " + subject + " imtihon");

                else
                    lesson(subject, topic);
            });

            main.addView(b);
        }

        Button back = new Button(this);
        back.setText("⬅️ Bosh sahifa");
        back.setOnClickListener(v -> showHome());

        main.addView(back);
    }

    void lesson(String subject, String topic) {

        main.removeAllViews();

        TextView t = new TextView(this);
        t.setText(
            subject + "\n\n" +
            topic + "\n\n" +
            "Bu bo‘limda mavzu bo‘yicha dars materiallari " +
            "va tushuntirishlar joylashtiriladi."
        );

        t.setTextSize(20);
        t.setTextColor(Color.BLACK);
        t.setPadding(20,30,20,30);

        main.addView(t);

        Button test = new Button(this);
        test.setText("📝 Shu mavzudan test");
        test.setOnClickListener(v -> startTest(subject));

        main.addView(test);

        Button back = new Button(this);
        back.setText("⬅️ Orqaga");
        back.setOnClickListener(v -> showSubject(subject));

        main.addView(back);
    }

    void startTest(String subject) {

        main.removeAllViews();

        TextView t = new TextView(this);
        t.setText(
            subject + "\n\n" +
            "1-savol\n\n" +
            "Quyidagi variantlardan to‘g‘ri javobni tanlang:"
        );

        t.setTextSize(20);
        t.setTextColor(Color.BLACK);
        t.setPadding(20,30,20,30);

        main.addView(t);

        String[] answers = {
            "A) 1-variant",
            "B) 2-variant",
            "C) 3-variant",
            "D) 4-variant"
        };

        for(String answer : answers) {

            Button b = new Button(this);
            b.setText(answer);

            b.setOnClickListener(v -> {
                result();
            });

            main.addView(b);
        }
    }

    void result() {

        main.removeAllViews();

        TextView result = new TextView(this);

        result.setText(
            "🎉 TEST YAKUNLANDI!\n\n" +
            "Natija: 1 / 1\n\n" +
            "📊 To‘g‘ri javoblar: 1\n" +
            "❌ Xatolar: 0\n\n" +
            "Davom eting! Har kuni ozgina bo‘lsa ham " +
            "o‘qish katta natija beradi."
        );

        result.setTextSize(21);
        result.setTextColor(Color.BLACK);
        result.setPadding(20,50,20,30);

        main.addView(result);

        Button home = new Button(this);
        home.setText("🏠 Bosh sahifa");

        home.setOnClickListener(v -> showHome());

        main.addView(home);
    }

    void showAI() {

        main.removeAllViews();

        TextView title = new TextView(this);
        title.setText("🤖 AI USTOZ");
        title.setTextSize(27);
        title.setGravity(Gravity.CENTER);
        title.setTextColor(Color.BLACK);
        title.setPadding(10,30,10,30);

        main.addView(title);

        TextView info = new TextView(this);
        info.setText(
            "Savolingizni yozing. AI Ustoz sizga " +
            "mavzuni sodda qilib tushuntirishga yordam beradi."
        );

        info.setTextSize(18);
        info.setTextColor(Color.BLACK);

        main.addView(info);

        EditText question = new EditText(this);
        question.setHint("Savolingizni yozing...");
        question.setMinLines(4);

        main.addView(question);

        Button send = new Button(this);
        send.setText("📨 Yuborish");

        main.addView(send);

        TextView answer = new TextView(this);
        answer.setTextSize(18);
        answer.setTextColor(Color.BLACK);
        answer.setPadding(10,30,10,30);

        main.addView(answer);

        send.setOnClickListener(v -> {

            String q = question.getText().toString();

            if(q.trim().isEmpty()) {
                answer.setText("Iltimos, savolingizni yozing.");
            } else {
                answer.setText(
                    "🤖 AI Ustoz:\n\n" +
                    "Savolingiz qabul qilindi:\n\"" +
                    q + "\"\n\n" +
                    "Bu demo versiya. Keyingi bosqichda " +
                    "haqiqiy AI xizmatini ulashimiz mumkin."
                );
            }
        });

        Button back = new Button(this);
        back.setText("⬅️ Bosh sahifa");

        back.setOnClickListener(v -> showHome());

        main.addView(back);
    }
}

**Generate real Android apps on your device — no server, no app store, no code.**

Describe what you want to your favorite AI, and iappyxOS turns it into a real installed APK with its own launcher icon. Building, signing, and installing all happen on-device. No cloud. No subscription. No coding required.

Sibling project to [iappyxOS Launcher](https://github.com/iappyx/iappyxOS-Launcher) (a programmable Android home screen) — both are standalone, and the same widget HTML runs in either one.

## Demo

[![Watch the demo](https://img.youtube.com/vi/VWvjfr7BCnY/maxresdefault.jpg)](https://youtu.be/VWvjfr7BCnY)

## Screenshots

<p align="center">
  <img src="docs/screenshot_1_myapps.png" width="24%" />
  <img src="docs/screenshot_2_create.png" width="24%" />
  <img src="docs/screenshot_3_demos.png" width="24%" />
  <img src="docs/screenshot_4_app.png" width="24%" />
</p>
<p align="center">
  <img src="docs/screenshot_5_icon.png" width="24%" />
  <img src="docs/screenshot_6_preview.png" width="24%" />
</p>

*My Apps • Create • 57 Demos • Generated Radio App • Icon Editor • Preview with Console*

## What it does

- **AI-generated App** — describe your app in plain language, let an AI generate the code, preview it, and build
- **Website as App** — turn any website into a lightweight standalone app (1MB, no bridges, sandboxed)
- **Demo Apps** — 57 pre-built apps to test native bridges (camera, GPS, NFC, BLE, SSH, network shares, and more)

Every generated app is a real signed APK that appears in your Android launcher. You can share it, uninstall it, or update it — just like any app. Generated apps pass Google Play Protect scanning.

## How it works

```
┌─────────────────────────────────────┐
│         STANDARD LAUNCHER           │
│   App 1 🎯   App 2 📍   App 3 📷   │
└──────────────┬──────────────────────┘
               │ real installed APKs
┌──────────────▼──────────────────────┐
│         GENERATED APP SHELL         │
│  WebView + native bridge layer      │
│  HTML/JS injected as assets         │
└──────────────┬──────────────────────┘
               │ created and signed by
┌──────────────▼──────────────────────┐
│       CONTAINER APP (iappyxOS)      │
│  AI prompt → HTML → APK injection   │
│  → manifest patching → v2 signing   │
│  → PackageInstaller                 │
└─────────────────────────────────────┘
```

1. User describes an app (or picks a template, or enters a URL)
2. HTML/JS is injected into a pre-built WebView shell APK
3. The Android manifest is binary-patched with a unique package name
4. The APK is signed on-device using the Android Keystore (hardware-backed)
5. The system installer dialog appears — the app shows up in the launcher

## Features

- **AI generation** — automatic via API (Anthropic, OpenRouter) or manual copy-paste to any AI
- **37 native bridge classes (140+ methods)** — camera, location, sensors, audio, notifications, push notifications (FCM), NFC, Bluetooth LE, Bluetooth Classic (serial), SSH/SFTP, SMB network shares, HTTP server/client, TCP/UDP sockets, WiFi Direct, mDNS, biometric, SQLite, contacts, SMS, calendar, clipboard, TTS, screen, vibration, alarms, media gallery, download manager, home screen widgets, scheduled background tasks, event triggers (charger / headphones / Bluetooth / WiFi / Android Auto), app-launch intents, and more
- **Bundled app files** — attach databases, JSON, images, or any data file to your app at build time. Accessible at runtime via `readAsset()` / `extractAsset()` — no download needed
- **Icon editor** — emoji, text, images, custom colors, gradients, shadows, filters, rotation, multiple layers
- **App management** — launch, rebuild, edit, share (APK, HTML, QR code, WiFi Direct), uninstall
- **QR code transfer** — share apps between devices via animated QR codes (no internet needed)
- **P2P sharing** — share built apps directly between devices via WiFi Direct
- **CSS style presets** — Material, Glassmorphic, Minimal, Dynamic (Material You colors) — applied globally
- **Preview** — test your app in a WebView with live JS console and simulated bridges before building
- **Offline-first** — everything except AI generation works in airplane mode
- **Configurable** — custom system prompt, app ID prefix, multiple AI providers, CSS styles
- **[Showcase](https://github.com/iappyx/iappyxOS-showcase)** — browse and build community apps directly in the app, or submit your own via PR
- **Home screen widgets** — generated apps can create configurable widgets with grids, clocks, timers, toggles
- **Background tasks** — scheduled JS execution even when the app is closed, auto-updates widgets
- **Version history** — automatic snapshots on rebuild, restore previous versions
- **Onboarding** — guided first-launch experience

## Quick start

1. [Download the latest Beta](https://github.com/iappyx/iappyxOS/raw/main/bin/iappyxOS.apk)
2. Sideload on Android 10+ (enable "Install unknown apps" for your browser)
3. Open iappyxOS → Create → pick a mode → build

**AI generation (two options):**
- **Manual (recommended)** — copy the generated prompt, paste it into any AI chat (Claude, ChatGPT, Gemini, etc.), paste the HTML back, preview, build. The Manual flow offers two prompt variants:
  - **Full (~45 KB)** — works with any AI, no internet needed on the AI's side.
  - **Linked (~600 chars)** — tiny prompt that points the AI at [`SPEC.md`](SPEC.md) via its canonical raw URL. Works with AIs that can fetch URLs (Claude.ai, ChatGPT with browsing, Gemini). Useful when your AI's paste limit rejects the full prompt.
- **Automatic** — add your API key in Settings (Anthropic or OpenRouter), then tap "Generate" in the Create flow

### Using the spec from any AI tool
`SPEC.md` at the repo root is the canonical iappyxOS bridge reference, always fetchable at:
```
https://raw.githubusercontent.com/iappyx/iappyxOS/main/SPEC.md
```
If you're chatting with Claude.ai or ChatGPT directly (outside the container), include that URL in your prompt and the AI will fetch it. When you get the HTML back, import it via Create → paste HTML.

## Sharing apps

Share your generated apps with others — multiple ways, no account needed:

- **Share APK** — send the compiled app file via any app (WhatsApp, email, Drive, Bluetooth)
- **Share Nearby** — transfer directly to another device via WiFi Direct, no internet required
- **Share via QR** — beam your app to another device using animated QR codes — no WiFi, no Bluetooth, just two screens
- **Share HTML** — export the source code so others can preview, modify, and rebuild it in their own iappyxOS

Recipients with iappyxOS installed can rebuild shared apps with their own icon and name.

## Native bridges

Generated apps access device hardware through a JavaScript bridge (`window.iappyx`):

| Bridge | What it does |
|--------|-------------|
| Storage | Key-value, file storage, pick files, save to Downloads, share files, move/copy with content URI support |
| Camera | Photo, video, QR/barcode scan, OCR, ML image classification, background removal, EXIF metadata, real-time frame scanning |
| Location | GPS single shot, continuous tracking, foreground service, geofencing |
| Sensors | Accelerometer, gyroscope, magnetometer, compass heading, proximity, light, pressure, step counter |
| Audio | Play/pause/seek/loop, record, speech-to-text, media session (lock screen controls), sound effects, audio focus, audio visualizer (waveform + FFT) |
| Notifications | Send with actions, schedule, repeating, badge count, cancel |
| NFC | Read tags, write NDEF text/URI |
| Bluetooth LE | Scan, connect, read/write characteristics, subscribe to notifications |
| SQLite | Full SQL database with transactions |
| Biometric | Fingerprint/face authentication |
| TTS | Text-to-speech with language, pitch, rate, completion callback |
| Contacts | Read device contacts (name, phone, email) |
| SMS | Send SMS messages |
| Calendar | Read/add calendar events |
| Clipboard | Read/write, monitor changes |
| Screen | Keep on, brightness, wake lock |
| Vibration | Patterns, haptic feedback (click, tick, heavy) |
| Alarms | Exact and repeating alarms (fire even when app is closed) |
| Share | Photos, text, files via share sheet; receive shared content from other apps |
| Device | Info, connectivity, torch, print, wallpaper, DND, shortcuts, dark mode, Material You theme colors |
| Media | Browse gallery (photos/videos/music), pick images, save to gallery, get metadata |
| Download | Queue file downloads with progress, survives app close |
| HTTP Server | Local HTTP/HTTPS server with TLS, CORS, file streaming |
| HTTP Client | Native requests with self-signed cert support, multipart upload, cookies (OkHttp) |
| SSH / SFTP | Remote terminal, command execution, file transfer, port forwarding (JSch) |
| SMB | Browse Windows/NAS network shares, upload, download, copy, rename, delete (jcifs-ng) |
| TCP Socket | Persistent bidirectional connections with TLS support |
| UDP | Datagram send/receive, unicast and multicast |
| NSD (mDNS) | Service registration, discovery, and resolve |
| WiFi Direct | P2P peer discovery, connection, group management |
| Push Notifications | FCM push notifications (requires Firebase setup in Advanced Settings) |
| Bluetooth Classic | Serial communication (SPP) for Arduino, ESP32, OBD-II car diagnostics, HC-05/HC-06 |
| Widget | Home screen widgets with configurable grid layouts, clocks, timers, checkboxes, toggles |
| Tasks | Scheduled background JS execution — fetch APIs, update widgets, send notifications while app is closed |
| Triggers | Fire a JS callback when charger / headphones / Bluetooth / WiFi / Android Auto connects or disconnects. Optional persistent mode survives app swipe-away and reboot. |
| Intent | Launch other installed apps (by package) or deep-link URIs. Enumerate installe
