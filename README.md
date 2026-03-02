
# Smart Greenhouse IoT Platform

This repository presents a Smart Greenhouse IoT Platform that combines Internet of Things technologies, AI-powered analysis, and live data visualization to efficiently regulate greenhouse environments. The system continuously tracks environmental parameters, performs automated control actions, and delivers intelligent plant care recommendations through an integrated AI assistant.

---

## Project Description

The Smart Greenhouse solution is built to:

* Track environmental conditions such as temperature, air humidity, soil moisture, and light levels using various sensors.
* Automatically operate devices including water pumps, ventilation fans, lighting systems, and humidifiers to maintain ideal growing conditions.
* Offer a real-time monitoring and control interface through a Node-RED dashboard.
* Answer user inquiries and provide plant care guidance using an AI assistant connected to the Google Gemini API.

---

## Repository Structure

### 1. Node-RED Flow Files

* **weather_dashboard_flow.json** – Handles external weather data integration, visualization, and environmental tracking.
* **greenhouse_automation_flow.json** – Controls greenhouse equipment automatically based on sensor readings and user-defined configurations.

### 2. Python Backend

* **smart_planter_server.py** – Flask-based server responsible for processing user questions, generating AI responses, and managing sensor-related data.

### 3. ESP32 Firmware

* **smart_greenhouse_esp32.ino** – Firmware for the ESP32 microcontroller that collects sensor data and controls actuators, communicating through an MQTT broker.

### 4. Data Storage Files

* **temp.csv, hum.csv, shum.csv, lum.csv** – CSV files used to log temperature, air humidity, soil moisture, and light intensity readings.
* **plant.txt** – Specifies the plant species currently being monitored.
* **conversation_history.json** – Stores previous interactions between the user and the AI assistant.

---

## Setup Instructions

### Requirements

* Python 3.7 or newer
* Node-RED
* MQTT broker (for example, Mosquitto)
* OpenWeatherMap API key

---

## Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/anthonynguyenchau/Greenhouse-ESP32)https://github.com/anthonynguyenchau/Greenhouse-ESP32
```

### 2. Install Python Packages

```bash
pip install -r requirements.txt
```

### 3. Configure Environment Variables

Create a `.env` file in the main directory and add your Google Gemini API key:

```
API_KEY=your_google_gemini_api_key
```

### 4. Define the Plant Type

Create or edit `plant.txt` and specify the plant name (for example: `Tomato`).

### 5. Launch the Flask Server

```bash
python smart_planter_server.py
```

### 6. Upload Firmware to ESP32

Flash the `smart_greenhouse_esp32.ino` file to your ESP32 board. Ensure Wi-Fi credentials and MQTT broker details are correctly configured before uploading.

### 7. Import Node-RED Flows

Open Node-RED and import both:

* `weather_dashboard_flow.json`
* `greenhouse_automation_flow.json`

---

## Node-RED Configuration

### HTTP Node Configuration

* Install the HTTP nodes via **Manage Palette > Install** if they are not already available.
* Add an HTTP input node with the `POST` method.
* Configure an endpoint (e.g., `/api/data`) and connect it to the appropriate processing nodes.

### OpenWeatherMap Integration

* Create an account on OpenWeatherMap and obtain an API key.
* Enter your API key and location details into the OpenWeatherMap node in Node-RED.
* Connect it to dashboard components to display real-time weather information.

---

## How to Use

* **Access the Dashboard:** Open the Node-RED user interface to monitor environmental data and manually control devices.
* **Use the AI Assistant:** Send a POST request to the `/ask` endpoint of the Flask server to receive plant care suggestions or greenhouse status updates.

### Sample API Request

```
POST /ask
{
  "question": "How is my plant doing?"
}
```

---

## Security Considerations

* **Protect API Keys:** Store sensitive credentials in environment variables and exclude them from version control using `.gitignore`.
* **Manage Log Files Carefully:** Keep files such as `conversation_history.json` private or properly secured before sharing the repository.


