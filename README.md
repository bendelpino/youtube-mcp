# YouTube MCP Server

A Model Context Protocol (MCP) server that enables Claude Desktop (and other applications) to interact with YouTube, providing search and transcript functionality.

## Features

- **Search YouTube Videos**: Search for videos with customizable result counts
- **Get Video Transcripts**: Extract transcripts from YouTube videos using URLs or video IDs
- **AI-Ready Integration**: Seamlessly integrates with Claude Desktop for YouTube content analysis

## Tools Available

### 1. `search_youtube_videos`

- **Purpose**: Search YouTube for videos based on a query
- **Parameters**:
  - `search_term` (string): The search query
  - `num_videos` (int): Number of videos to return (default: 5, max: 50)
- **Returns**: List of video information including titles, channels, descriptions, URLs, and metadata

### 2. `get_youtube_transcript`

- **Purpose**: Extract transcript from a YouTube video
- **Parameters**:
  - `video_url_or_title` (string): YouTube video URL or video ID
- **Returns**: Full transcript with timestamps and metadata

### 3. `analyze_youtube_content_prompt`

- **Purpose**: AI prompt template for comprehensive YouTube content analysis
- **Parameters**:
  - `search_term` (string): Topic to analyze
  - `num_videos` (int): Number of videos to analyze

## Setup

### 1. Install Dependencies

```bash
# Create virtual environment
python3 -m venv .venv

# Activate virtual environment
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Get YouTube API Key

1. Go to [Google Cloud Console](https://console.developers.google.com/)
2. Create a new project or select existing one
3. Enable YouTube Data API v3
4. Create credentials (API Key)
5. Copy the API key

### 3. Configure Environment

```bash
# Copy example environment file
cp .env.example .env

# Edit .env and add your YouTube API key
YOUTUBE_API_KEY=your_actual_api_key_here
```

### 4. Test the Server

```bash
# Activate virtual environment
source .venv/bin/activate

# Run the server
python youtube_server.py
```

## Integration with Claude Desktop

Add this configuration to your Claude Desktop MCP settings:

```json
{
  "mcpServers": {
        "youtube": {
            "command": "local/path/to/uv",
            "args": [
                "run",
                "--directory",
                "/Path/to/your/project",
                "youtube_server.py"
            ],
            "env": {
                "YOUTUBE_API_KEY": "your_key_here"
            }
  }
}
```

## Usage Examples

Once integrated with Claude Desktop, you can:

- "Search for videos about machine learning and get transcripts"
- "Find the latest videos on climate change and analyze their content"
- "Get the transcript of this YouTube video: https://www.youtube.com/watch?v=..."
- "Compare different perspectives on AI ethics from YouTube videos"

## Error Handling

- **Missing API Key**: Server will warn and search functionality will be limited
- **Invalid Video IDs**: Clear error messages for transcript requests
- **API Limits**: Respects YouTube API quotas and rate limits
- **Missing Transcripts**: Handles videos without available captions

## Dependencies

- `fastmcp`: MCP server framework
- `google-api-python-client`: YouTube Data API access
- `youtube-transcript-api`: Transcript extraction

## License

This project is open source and available under standard licensing terms.
