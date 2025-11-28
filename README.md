# P5 Archive Search

A native macOS application for browsing and searching Archiware P5 Archive Index inventory.

![macOS](https://img.shields.io/badge/macOS-14.0+-blue) ![Swift](https://img.shields.io/badge/Swift-5.9-orange) ![License](https://img.shields.io/badge/License-MIT-green)
<img width="1121" height="852" alt="p5archivesearch-setup" src="https://github.com/user-attachments/assets/f136cbb8-f1f9-4aa1-adf0-6eb19f7d3510" />

## Overview

P5 Archive Search provides a modern SwiftUI interface for exploring the contents of Archiware P5 Archive indexes. Browse through archived directories, recursively analyze entire folder structures, and maintain a local SQLite database of indexed items for fast offline searching.

## Features

### Browse Archive Indexes
Navigate through P5 archive index inventory with a familiar file browser interface. Double-click folders to drill down, use breadcrumb navigation to jump back, and view detailed information about each item including archive status, media labels, and modification dates.

### Recursive Analysis
The **Analyze** feature recursively scans all subdirectories from a starting path, automatically indexing every file and folder to the local database. This allows you to build a complete searchable inventory of your archive without manually browsing each folder.

- Start from any path and scan all subdirectories automatically
- Real-time progress showing current folder, folders scanned, and items indexed
- Stop anytime with the Stop button
- Continues scanning even if individual folders encounter errors
- Rate-limited requests to avoid overwhelming the server

### Fast Offline Search
Search your indexed items instantly without making API calls. Filter by:
- File or folder name
- Path
- Server
- Archive index
- Item type (files only, directories only)

### Multiple Server Support
Configure connections to multiple P5 servers, each with their own archive index. Switch between servers easily from the sidebar.

### Export Options
- **JSON** - Raw API responses saved automatically with each query
- **CSV** - Export search results or browse results to CSV format
- **SQLite Database** - All indexed items stored locally for fast access

### Secure Credentials
Server passwords are stored securely in the macOS Keychain, never in plain text.

## Requirements

- macOS 14.6 (Sonoma) or later
- Archiware P5 server with REST API enabled
- Network access to the P5 server
- Optional: `jq` installed for automatic CSV generation (`brew install jq`)
- Note: jq is included by default in macOS 15 (Sequoia) and later

## Quick Start

1. **Add a Server** - Click the `+` button in the sidebar
2. **Enter Connection Details**:
   - Alias: A friendly name for the server
   - IP Address: The P5 server IP or hostname
   - Port: Usually `8000`
   - Archive Index: The index to query (e.g., `Default-Archive`)
   - Username/Password: Your P5 credentials
3. **Enter a Starting Path** - Type a path like `Volumes/YourVolume`
4. **Browse or Analyze**:
   - Click **Browse** to view the contents of that path
   - Click **Analyze** to recursively scan all subdirectories
5. **Search** - Switch to "Search DB" tab to find indexed items

## User Interface

### Browse Tab

The Browse tab provides an interactive file browser for the P5 archive index.

**Navigation Bar**
- **Back button (←)** - Return to previous location
- **Up button (↑)** - Go to parent directory
- **Path field** - Enter or edit the current path
- **Browse button** - Query the current path
- **Analyze button** - Recursively scan all subdirectories

**Breadcrumb Trail**
Click any path component to jump directly to that location. Click "Root" to return to the top level.

**Results Table**
Displays items at the current path with columns for:
- Name (with folder/file icon)
- Type (Directory/File)
- Size
- Volume/Media label
- Archived status and date
- Modification date
- Navigation path

Double-click any folder to navigate into it.

### Analyze Mode

When you click Analyze, the app recursively scans all subdirectories:

1. A progress bar appears showing:
   - Current folder being scanned
   - Total folders processed
   - Total items indexed
2. The log panel shows real-time progress for each folder
3. Click **Stop** to halt the analysis at any time
4. When complete, a summary shows total folders and items indexed

**Tips for Analyzing:**
- Start with a specific subfolder rather than the root for faster results
- The analysis can be stopped and resumed later (already-indexed items won't be duplicated)
- Check the log panel if folders are being skipped due to errors

### Search DB Tab

Search through all indexed items in the local database.

**Search Controls**
- **Search field** - Enter keywords to search names and paths
- **Server filter** - Limit results to a specific server
- **Index filter** - Limit results to a specific archive index
- **Type filter** - Show only files or only directories

**Results Table**
Shows matching items with details including which server and archive index they came from.

**Export**
Click the export button to save search results to CSV.

### Log Panel

The log panel at the bottom shows:
- API query progress and status
- Analysis progress during recursive scans
- Error messages and warnings
- Summary statistics

## Data Storage

### SQLite Database
Location: `~/Library/Application Support/P5ArchiveSearch/P5InventorySearch.sqlite`

Stores all indexed items with the following information:
- Name and path
- Item type (file/directory)
- Size
- Archive status and date
- Media/volume label
- Server and archive index
- Query date

### Output Files
Location: `~/Documents/P5ArchiveSearch/`

Each browse query saves:
- `inventory_{timestamp}.json` - Raw JSON response
- `inventory_{server}_{timestamp}.csv` - Formatted CSV (requires jq)

### Server Configurations
- Server settings stored in UserDefaults
- Passwords stored securely in macOS Keychain


<img width="1010" height="269" alt="p5archivesearch-setup2" src="https://github.com/user-attachments/assets/9740bf01-71ab-4d3e-a842-a82526b7147a" />


## API Endpoint

The app queries the P5 Archive Index Inventory REST API:

```
GET http://{server}:{port}/rest/v1/archive/indexes/{archive-index}/inventory/{path}
```

Example:
```
http://192.168.1.100:8000/rest/v1/archive/indexes/Default-Archive/inventory/Volumes/JellyfishSMB
```

## Troubleshooting

### Connection Failed
- Verify the P5 server is running and accessible
- Check the IP address, port, and credentials
- Ensure the P5 REST API is enabled on the server
- Try accessing the API URL directly in a browser

### No Items Displayed
- Verify the archive index name is correct
- Check if the path exists in the archive (paths are case-sensitive)
- Review the log panel for error messages
- Try a higher-level path (e.g., just "Volumes")

### Analyze Stops or Skips Folders
- Check the log panel for error messages
- Some folders may have permission issues or be inaccessible
- The analysis continues even when individual folders fail
- Error count is shown in the final summary

### Paths with Spaces
The app automatically URL-encodes spaces and special characters. The log panel shows both original and encoded paths when they differ.

### CSV Not Generated
- Install jq: `brew install jq`
- JSON files are still saved even without jq

## Keyboard Shortcuts

| Action | Shortcut |
|--------|----------|
| Browse/Search | Return |
| Cancel | Escape |

## Version History

### 1.3.0

Sort by sorting fixed

### 1.2.0
- Added recursive Analyze feature for automatic subdirectory scanning
- Real-time progress tracking during analysis
- Stoppable analysis with summary statistics
- Improved error handling for failed folders


### 1.1
Adjusted minimum macOS to 14.6 Sonoma

### 1.0.0
- Initial release
- Browse and search P5 Archive Index inventory
- SQLite database for offline searching
- CSV and JSON export
- Multi-server support with secure credential storage

## License

MIT License

## Acknowledgments

- Built for use with [Archiware P5](https://www.archiware.com/)


