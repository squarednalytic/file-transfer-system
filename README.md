# File Transfer System

A system that allows a cloud server to download files from on-premise clients behind NAT.

## Architecture

- **Server**: Cloud-hosted service that manages client registrations and initiates file downloads
- **Client**: On-premise service that registers with server and provides files for download
- **Communication**: HTTP-based with client-initiated connections to overcome NAT limitations

## How it Works

1. Clients register with the server and maintain heartbeat
2. Server stores client information but cannot directly connect to clients
3. When server wants to download a file, it notifies the client through an existing connection
4. Client initiates file upload to server using the reverse connection

## Setup

### Prerequisites

- Node.js 14+ 
- npm or yarn

### Installation

1. Clone or download the project files
2. Install server dependencies:
   ```bash
   cd server
   npm install


3. Install client dependencies:
cd client
npm install

Running the System

    1. Start the server:
cd server
npm start

Server will run on http://localhost:3000

2. Start a client (in separate terminal):

cd client
npm start

Client will generate a 100MB file and register with the server.

3. Start additional clients (optional):

cd client
CLIENT_PORT=8081 CLIENT_ID=client-2 npm start

API Usage
Check registered clients:

curl http://localhost:3000/clients

Download file from specific client:

curl -X POST http://localhost:3000/download/client-1

Check client status:

curl http://localhost:8080/status

Environment Variables

Server:

    • PORT - Server port (default: 3000)

Client:

    • CLIENT_PORT - Client port (default: 8080)

   •  CLIENT_ID - Unique client identifier

    • 6SERVER_URL - Server URL (default: http://localhost:3000)

File Generation

The client automatically generates a 100MB file at $HOME/file_to_download.txt. You can manually generate the file:

cd client
npm run generate-file

Scaling

    • For production, use proper database instead of in-memory storage

    • Add authentication and encryption

    • Use message queue for better reliability

    • Implement proper logging and monitoring


## Cara Menjalankan:

1. **Server**:
   ```bash
   cd server
   npm install
   npm start

2. Client:

cd client  
npm install
npm start

3. Test Download: : 
curl -X POST http://localhost:3000/download/client-1
