# Python-Based C2 Server

## Overview

This project is a Python-based Command and Control (C2) server designed to route traffic between an attacker and a victim via an intermediate beacon, which helps anonymize the attacker's IP. By utilizing a dummy server for communication, the victim never directly interacts with the attacker's system, ensuring greater operational security.

## Key Features

- **Anonymized Traffic Routing**: All traffic between the attacker and victim is routed through a dummy server using a beacon. This design prevents the victim from discovering the attacker’s real IP address.
- **Flexible Deployment**: The server and beacon can be deployed independently, allowing the attacker to maintain control over victims through any publicly accessible server acting as the beacon.
- **Customizable Payload**: Generate custom payloads that include the IP of the dummy server where the beacon is hosted. These payloads can be distributed to victims to establish communication with the beacon and, subsequently, the C2 server.

## Project Structure

- **`main-server.py`**: The core C2 server script, responsible for managing communication between the attacker and the beacon.
- **`beacon.py`**: A Python script that runs on a dummy server, acting as the relay between the attacker and the victim. It forwards the attacker's commands and transmits responses from the victim.
- **`virus.py`**: A sample payload designed to be executed on the victim's machine. This payload establishes a connection with the beacon, using the IP address of the dummy server.

## Setup and Usage

### 1. Setting Up the C2 Server
- Clone this repository onto the attacker’s machine.
- Run `main-server.py` on your local system (attacker's machine) to start the C2 server.

```bash
python3 main-server.py

### 2. Deploying the Beacon on the Dummy Server

- **Setup the Dummy Server**: Choose a server that is publicly accessible to act as the relay (beacon). This server will route traffic between the victim and the C2 server, keeping your identity hidden.
- **Upload the Beacon**: Transfer the `beacon.py` file to your dummy server.
- **Run the Beacon**: Once transferred, run the beacon on the dummy server:

  ```bash
  python3 beacon.py
