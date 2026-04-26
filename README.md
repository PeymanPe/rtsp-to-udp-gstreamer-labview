# RTSP to UDP Streaming for LabVIEW using GStreamer

This project demonstrates how to convert an RTSP video stream into a UDP MJPEG stream using GStreamer and access it from LabVIEW.

---

## 📌 Overview

The pipeline takes an RTSP (H.264) stream (e.g., from an IP camera), decodes it, converts it into JPEG frames, and sends it over UDP. LabVIEW can then receive and process the stream.

---

## 🎥 GStreamer Pipeline

```bash
gst-launch-1.0 -v \
rtspsrc location="<network stream URL>" latency=100 drop-on-latency=false \
! rtph264depay \
! h264parse \
! avdec_h264 \
! videoconvert \
! jpegenc \
! multipartmux boundary=frame \
! udpsink host=127.0.0.1 port=5000 buffer-size=65536
```

---

## ⚙️ Installation (GStreamer on Windows)

### 1. Download GStreamer

Download the latest **MSVC 64-bit installers** from the official site:
https://gstreamer.freedesktop.org/download/

Install both:

* Runtime installer (`gstreamer-1.0-msvc-x86_64-xxx.msi`)
* Development installer (`gstreamer-1.0-devel-msvc-x86_64-xxx.msi`)

---

### 2. Install

* Run the **Runtime installer first**, then the **Development installer**
* Use the default installation path:

```
C:\gstreamer\1.0\msvc_x86_64\
```

---

### 3. Add to PATH

Add the following directory to your system environment variables:

```
C:\gstreamer\1.0\msvc_x86_64\bin
```

Restart your terminal after updating PATH.

---

### 4. Verify Installation

```bash
gst-launch-1.0 --version
```

---

### 5. Test GStreamer

```bash
gst-launch-1.0 videotestsrc ! autovideosink
```

If a video window appears, GStreamer is installed correctly.

---

## 🚀 Usage

1. Ensure your RTSP stream is accessible:

   ```
   <network stream URL>
   ```

2. Run the GStreamer pipeline

3. Open the LabVIEW VI:
   **`mjpegReader (UDP)V3`**

4. Configure LabVIEW to receive UDP data:

   * **IP:** 127.0.0.1
   * **Port:** 5000

5. Run the VI to view the MJPEG stream

---

## ✨ Features

* RTSP (H.264) input support
* Real-time decoding and conversion
* MJPEG encoding for easy parsing
* UDP streaming compatible with LabVIEW
* Configurable latency
