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
```
### 2. Deploying the Beacon on the Dummy Server

- **Setup the Dummy Server**: Choose a server that is publicly accessible to act as the relay (beacon). This server will route traffic between the victim and the C2 server, keeping your identity hidden.
- **Upload the Beacon**: Transfer the `beacon.py` file to your dummy server.
- **Run the Beacon**: Once transferred, run the beacon on the dummy server:

  ```bash
  python3 beacon.py
  ```
### 3. Creating the Payload

    Edit virus.py to include the IP address of the dummy server (where the beacon is running).

```python

BEACON_IP = "YOUR_DUMMY_SERVER_IP"
```
    Distribute virus.py to the target victim. Once executed on the victim's machine, it will establish communication with the beacon, routing traffic through the dummy server to the attacker's C2 server.

### 4. Running the Attack

    Once the victim runs the payload, it connects to the beacon, which routes the communication to the C2 server.
    Use the C2 server (main-server.py) to issue commands to the victim via the beacon. All responses are routed back through the beacon to the C2 server, hiding the attacker's IP.

Example Workflow

    Start the C2 server on the attacker's machine:

   ``` bash

python3 main-server.py
  ```
Start the beacon on a dummy server:

```bash

    python3 beacon.py
```
    Edit virus.py to use the beacon's IP, then distribute it to the victim.

    Once the victim executes virus.py, the C2 server can now control the victim's machine, issuing commands and receiving responses via the beacon.

Security Notes

    Ensure that the beacon is hosted on a dummy server that cannot be easily traced back to the attacker.
    Use encrypted channels where possible to prevent detection.
    Regularly rotate IPs of dummy servers to further minimize exposure.

Future Enhancements

    Implement encryption between the C2 server, beacon, and victim for added security.
    Add more customizable payload options to support different types of attack vectors.
    Introduce authentication mechanisms to restrict access to the C2 server.
