# Chat_App
# Chat Application

## Overview

This is a basic Python-based chat application that allows users to establish peer-to-peer communication over a network using **UDP sockets**. The application supports sending text messages, heartbeats (to ensure the connection is active), and connection requests.

## Features

- **Peer-to-Peer Messaging**: Exchange text messages directly between two users by specifying IP and port.
- **Heartbeat Mechanism**: Sends a heartbeat signal every 25 seconds to maintain the connection and detect lost peers.
- **Connection Requests**: Users can initiate and accept/decline connection requests.
- **Automatic Disconnection**: After missing 3 consecutive heartbeats, the session is terminated automatically.
- **Threading Support**: Separate threads for listening to messages, sending heartbeats, and handling user input.

## Requirements

- Python 3.x
- Basic understanding of socket programming
- Familiarity with threading in Python

## How It Works

### Message Types

1. **Text Messages** (`MESSAGE_TYPE_TEXT = 1`): Regular chat messages.
2. **Heartbeat Messages** (`MESSAGE_TYPE_HEARTBEAT = 2`): Keep the connection alive.
3. **Connection Requests** (`MESSAGE_TYPE_CONNECT_REQUEST = 3`): Sent to initiate a connection.

### Key Components

- **Heartbeat Mechanism**: Sends heartbeats at regular intervals to ensure the connection stays alive. If 3 heartbeats are missed, the session ends.
- **Multi-threading**:
  - **Listener Thread**: Listens for incoming messages.
  - **Heartbeat Thread**: Sends heartbeats to the connected peer.
  - **Input Thread**: Handles user commands and input.

### User Interaction

- **Initiating a Connection**: Start by providing the target peer's IP address and port. A connection request is sent, and the peer can accept or decline.
- **Sending Messages**: Once connected, users can exchange text messages.
- **Exiting**: Type `exit` to end the session or close the chat if heartbeats are missed.

## Running the Program

### Setup

1. Clone or download the project files to your local machine.
2. Ensure Python 3.x is installed.

### Usage

To run the chat application, use the following command:

```bash
python netchat.py <port>

Where <port> is the port number on which the application will listen for incoming messages.
### Example Flow

1. **User A** starts the application on port `5555`:
   ```bash
   python netchat.py 5555

2. User A will now be waiting for incoming connections.

   User B starts the application on port 6666":
   python netchat.py 6666


3. User A initiates the chat by entering User B's IP address and port:
    Start chat with? (IP Port): 192.168.0.10 6666

4. User B will receive a connection request and can accept or decline:
    Connection request from: 192.168.0.20 5555
[192.168.0.20:5000] Accept connection? (y/n): y

5.  User A and User B can now exchange messages:

    User A:
        [192.168.0.10:6666] Your message: Hello, User B!
    
    USER B:
        [192.168.0.20:5555] Your message: Hi, User A! How are you?

6.  Heartbeat: Both users will send periodic heartbeats to maintain the connection.

    Heartbeat sent to 192.168.0.10:6666
    Heartbeat sent to 192.168.0.20:5555

7.  Disconnection: If a user misses 3 heartbeats, the session will close automatically:

    Missed 3 heartbeats
    Connection lost. Ending session.

8. To manually exit the chat, type exit:

    [192.168.0.10:6666] Your message: exit
    Closing session with peer...


