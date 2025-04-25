# 📂 Distributed File System (DFS)

A distributed file system implementation with specialized servers for different file types, providing seamless file storage, retrieval, and management across multiple server nodes.

## System Architecture 🏗️

The system consists of five main components:

- **Main Server (S1)** 🌟: Acts as the gateway and handles .c files directly
- **PDF Server (S2)** 📄: Specializes in PDF file operations (port 8081)
- **Text Server (S3)** 📝: Manages text files (port 8082)
- **ZIP Server (S4)** 🗜️: Handles ZIP archives (port 8083)
- **Client Application** 💻: Provides a user interface for all file operations

## Features ✨

- **Transparent file routing** 🔄: Files are automatically routed to appropriate servers based on file extension
- **Comprehensive file operations**:
  - Upload files to any server 📤
  - Download files from any server 📥
  - Remove files from any server 🗑️
  - List files across all servers 📋
  - Create and download tarballs of specific file types 📦
- **Intelligent path resolution** 🔍: Handles various path formats (~/S1/, ~S1/, etc.)
- **Multi-client support** 👥: Uses forking to handle multiple simultaneous clients
- **Robust error handling** ⚠️: Comprehensive checking and reporting of all operations
- **Transparent cross-server operations** 🔄: File operations work seamlessly across servers

## Getting Started 🚀

### Prerequisites

- C compiler (gcc recommended)
- Linux/Unix environment
- Network connectivity between server machines (or localhost for testing)

### Compilation

```bash
# Compile the main server (S1)
gcc -o s1_server s1_server.c

# Compile the PDF server (S2)
gcc -o s2_server s2_server.c

# Compile the text server (S3)
gcc -o s3_server s3_server.c

# Compile the ZIP server (S4)
gcc -o s4_server s4_server.c

# Compile the client
gcc -o dfs_client dfs_client.c
```

### Running the System

1. Start all server components:

```bash
# Start main server (S1)
./s1_server &

# Start PDF server (S2)
./s2_server &

# Start text server (S3)
./s3_server &

# Start ZIP server (S4)
./s4_server &
```

2. Run the client application:

```bash
./dfs_client
```

## Client Usage Guide 📚

The client provides a menu-driven interface with the following options:

1. **Upload a file to server** 📤
   - Provide local file path and destination server directory
   - Files are automatically routed to the appropriate server based on extension

2. **Download a file from server** 📥
   - Specify the server file path and local destination
   - The system locates and retrieves the file regardless of which server stores it

3. **Remove a file from server** 🗑️
   - Specify the server file path to delete
   - The system routes the delete request to the appropriate server

4. **Download tar file by type (.c, .txt, .pdf)** 📦
   - Create and download an archive containing all files of a specific type
   - Specify the file type and local path to save the tar file

5. **List files in directory** 📋
   - View all files in a specified server directory
   - Shows files from all servers in a consolidated view

0. **Exit** 🚪
   - Terminate the client application

## Path Formats 🔍

The system supports several path formats:
- `~/S1/path/to/file` - Main server path with home directory expansion
- `~S1/path/to/file` - Alternative main server path format
- Similar formats for S2, S3, and S4 respectively

## Implementation Details 🔧

- **Socket Programming**: Uses TCP sockets for reliable communication
- **Protocol Messages**: Well-defined messages for coordination (READY, SIZE_ACK, SUCCESS, etc.)
- **Error Handling**: Comprehensive error checking and reporting
- **Process Management**: Uses fork() to handle multiple client connections
- **Directory Management**: Automatically creates necessary directories as needed

## Limitations and Considerations ⚠️

- Server components must be running on the expected ports
- ZIP file archiving is not supported (but listing and regular operations work)
- All servers should have access to the user's home directory
- Maximum file size is limited to 100MB
- Path length is limited to 1024 characters
