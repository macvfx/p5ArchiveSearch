# P5 Archive Search

A native macOS application for browsing and searching Archiware P5 Archive Index inventory.

![macOS](https://img.shields.io/badge/macOS-14.0+-blue) ![Swift](https://img.shields.io/badge/Swift-5.9-orange) ![License](https://img.shields.io/badge/License-MIT-green)
<img width="1121" height="852" alt="p5archivesearch-setup" src="https://github.com/user-attachments/assets/f136cbb8-f1f9-4aa1-adf0-6eb19f7d3510" />

## Overview

P5 Archive Search provides a modern SwiftUI interface for exploring the contents of Archiware P5 Archive indexes. Browse through archived directories, search for specific files, and maintain a local SQLite database of indexed items for fast offline searching.

## Features

- **Browse Archive Indexes** - Navigate through P5 archive index inventory with a familiar file browser interface
- **Breadcrumb Navigation** - Easy path navigation with clickable breadcrumbs and back/up buttons
- **Multiple Server Support** - Configure and manage connections to multiple P5 servers
- **Custom Archive Indexes** - Specify which archive index to query (defaults to "Default-Archive")
- **SQLite Database** - All discovered items are stored locally for fast searching
- **Search Functionality** - Search indexed items by name, path, type, server, and archive index
- **Export Options** - Export search results to CSV and save raw JSON responses
- **Secure Credentials** - Server passwords stored securely in macOS Keychain
- **Real-time Logging** - Monitor API queries and responses in the built-in log panel

## Requirements

- macOS 14.0 (Sonoma) or later
- Archiware P5 server with REST API enabled
- Network access to P5 server
- Optional: `jq` installed for CSV generation (`brew install jq`)
- **Note:** jq is included by default in macOS 15 (Sequoia) and later

## Quick Start

1. **Add a Server** - Click the `+` button in the sidebar to add a P5 server
2. **Enter Connection Details**:
   - Alias: A friendly name for the server
   - IP Address: The P5 server IP or hostname
   - Port: Usually `8000`
   - Archive Index: The index to query (e.g., `Default-Archive`)
   - Username/Password: Your P5 credentials
3. **Enter a Starting Path** - Type a path like `Volumes/YourVolume` in the path field
4. **Click Browse** - The app will query the P5 server and display the contents
5. **Navigate** - Double-click folders to drill down, use breadcrumbs to navigate back
6. 
<img width="1010" height="269" alt="p5archivesearch-setup2" src="https://github.com/user-attachments/assets/9740bf01-71ab-4d3e-a842-a82526b7147a" />

## API Endpoint

The app queries the P5 Archive Index Inventory REST API:

```
GET http://{server}:{port}/rest/v1/archive/indexes/{archive-index}/inventory/{path}
```

Example:
```
http://192.168.1.100:8000/rest/v1/archive/indexes/Default-Archive/inventory/Volumes/BigStorageSMB
```

## Data Storage

### SQLite Database
- Location: `~/Library/Application Support/P5ArchiveSearch/P5InventorySearch.sqlite`
- Stores all indexed items for offline searching
- Automatically deduplicates entries

### Output Files
- Location: `~/Documents/P5ArchiveSearch/{server}_{timestamp}/`
- Each query saves:
  - `inventory_{timestamp}.json` - Raw JSON response
  - `inventory_{server}_{timestamp}.csv` - Formatted CSV (requires `jq`)

### Server Configurations
- Stored in UserDefaults
- Passwords stored in macOS Keychain

## User Interface

### Browse Tab
- **Path Field** - Enter the starting path for browsing
- **Breadcrumbs** - Click any path component to navigate
- **Results Table** - Shows directory contents with:
  - Name (with folder/file icons)
  - Type (Directory/File)
  - Size
  - Volume/Media label
  - Archived status and date
  - Modification date
  - Navigation path

### Search DB Tab
- **Search Field** - Enter search terms
- **Filters** - Filter by server, archive index, or item type
- **Results Table** - Shows matching items from the local database
- **Export** - Export results to CSV

### Log Panel
- Shows real-time progress and status messages
- Displays API URLs and response information
- Helps troubleshoot connection issues

## Keyboard Shortcuts

| Action | Shortcut |
|--------|----------|
| Browse/Search | Return |
| Cancel | Escape |

## Troubleshooting

### Connection Failed
- Verify the P5 server is running and accessible
- Check the IP address, port, and credentials
- Ensure the P5 REST API is enabled
- Try accessing the API URL directly in a browser

### No Items Displayed
- Verify the archive index name is correct
- Check if the path exists in the archive
- Review the log panel for error messages

### Spaces in Paths
- The app automatically URL-encodes spaces and special characters
- Paths like `Stock Footage` become `Stock%20Footage` in API calls

### CSV Not Generated
- Install `jq`: `brew install jq`
- The app will show a warning in the log if `jq` is not found


Optional external tools:
- `jq` - For CSV generation
- `curl` - For API requests (included with macOS)
- SQLite3

## License

MIT License - See LICENSE file for details.

## Acknowledgments

Built for use with [Archiware P5](https://www.archiware.com/)

## Version History

### 1.0.0
- Initial release
- Browse and search P5 Archive Index inventory
- SQLite database for offline searching
- CSV and JSON export
- Multi-server support with secure credential storage
