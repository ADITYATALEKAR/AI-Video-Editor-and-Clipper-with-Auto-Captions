# AI Video Clipper - Auto Captions and Thumbnails

AI-powered tool that automatically converts long videos into short clips with intelligent segmentation. Features include automated caption generation using Whisper, thumbnail creation, and configurable output settings. Perfect for content creators turning lengthy videos into social media shorts for TikTok, Instagram Reels, and YouTube Shorts.

## ✨ Features

- 🤖 **Intelligent Video Segmentation** - Automatically identifies optimal clip segments from long videos
- 📝 **Auto Caption Generation** - Uses OpenAI Whisper for accurate speech-to-text transcription
- 🖼️ **Automatic Thumbnails** - Creates eye-catching thumbnails from video frames
- ⚙️ **Highly Configurable** - Customizable clip duration, quality, resolution, and styling
- 📱 **Social Media Ready** - Optimized for TikTok, Instagram Reels, YouTube Shorts (9:16 aspect ratio)
- 🎨 **Professional Captions** - Customizable font, color, and outline styling
- 📊 **Batch Processing** - Process multiple clips from a single video automatically
- 🔧 **Easy Configuration** - JSON-based configuration with sensible defaults

## 🚀 Quick Start

### Prerequisites

1. **Python 3.8+**
2. **FFmpeg** - Install from [ffmpeg.org](https://ffmpeg.org/download.html)
3. **Required Python packages:**
   ```bash
   pip install openai-whisper ffmpeg-python
   ```

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/AI-Video-Clipper-Auto-Captions-and-Thumbnails.git
   cd AI-Video-Clipper-Auto-Captions-and-Thumbnails
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Verify FFmpeg installation:
   ```bash
   ffmpeg -version
   ```

### Basic Usage

#### Command Line
```bash
# Basic usage - process a video with default settings
python video_editor.py your_video.mp4

# Custom output directory
python video_editor.py your_video.mp4 --output-dir my_clips

# Show video information
python video_editor.py your_video.mp4 --info

# Show current configuration
python video_editor.py --show-config
```

#### Python Script
```python
from video_editor import VideoEditorApp

# Initialize the editor
editor = VideoEditorApp()

# Process a video
result = editor.process_video("your_video.mp4", "output_clips")

if result['status'] == 'success':
    print(f"Generated {result['clips_generated']} clips!")
    for clip in result['clips']:
        print(f"- {clip['file_path']} ({clip['duration']:.1f}s)")
```

## 🛠️ Configuration

The tool uses a `video_config.json` file for configuration. Default settings are created automatically on first run.

### Configuration Options

```json
{
  "video_settings": {
    "clip_duration": 12,           // Duration of each clip in seconds
    "overlap_seconds": 2,          // Overlap between clips
    "max_clips": 20,              // Maximum number of clips to generate
    "output_resolution": "1080:1920", // Resolution (9:16 for shorts)
    "video_quality": 18           // Video quality (CRF value, lower = better)
  },
  "caption_settings": {
    "font_size": 24,              // Caption font size
    "font_color": "white",        // Caption text color
    "outline_color": "black",     // Caption outline color
    "outline_width": 2,           // Caption outline thickness
    "enable_captions": true       // Enable/disable captions
  },
  "output_settings": {
    "create_thumbnails": true,    // Generate thumbnails
    "output_format": "mp4",       // Output video format
    "preserve_audio": true        // Keep audio in clips
  }
}
```

### Customizing Settings

```python
# Update configuration programmatically
editor = VideoEditorApp()
editor.update_config({
    "video_settings": {
        "clip_duration": 15,
        "max_clips": 10
    },
    "caption_settings": {
        "font_size": 28,
        "font_color": "yellow"
    }
})
```

## 📁 Output Structure

After processing, you'll get organized output:

```
clips/
├── clip_000_0s.mp4           # Original clip
├── clip_000_0s_captioned.mp4 # Clip with captions
├── clip_000_0s_thumb.jpg     # Thumbnail
├── clip_000_0s.srt          # Subtitle file
├── clip_001_10s.mp4
├── clip_001_10s_captioned.mp4
└── ...
```

## 🎯 Use Cases

- **Content Creators** - Turn long streams/videos into engaging shorts
- **Social Media Managers** - Batch create content for multiple platforms  
- **Educators** - Break down lectures into digestible segments
- **Marketers** - Create highlight reels from webinars/presentations
- **Podcasters** - Generate video clips for social promotion

## 🔧 Advanced Features

### Intelligent Segmentation
The tool automatically finds interesting segments by:
- Analyzing video length and optimal clip distribution
- Adding natural variance to avoid mechanical cuts
- Balancing overlap to maintain context

### Caption Styling
Customize captions with:
- Font size and color options
- Outline thickness and color
- Positioning and timing
- SRT file generation for manual editing

### Batch Processing
```python
# Process multiple videos
videos = ["video1.mp4", "video2.mp4", "video3.mp4"]
for video in videos:
    result = editor.process_video(video, f"clips_{video.stem}")
    print(f"Processed {video}: {result['clips_generated']} clips")
```

## 📋 Requirements

Create a `requirements.txt` file:
```
openai-whisper>=20231117
torch>=1.9.0
ffmpeg-python>=0.2.0
```

## 🐛 Troubleshooting

### Common Issues

1. **FFmpeg not found**
   ```bash
   # Ubuntu/Debian
   sudo apt update && sudo apt install ffmpeg
   
   # macOS
   brew install ffmpeg
   
   # Windows: Download from ffmpeg.org
   ```

2. **Whisper model download fails**
   - Ensure stable internet connection
   - Model downloads automatically on first use
   - Check firewall/proxy settings

3. **Out of memory errors**
   - Reduce `max_clips` in configuration
   - Use smaller Whisper model: `whisper.load_model("tiny")`
   - Process shorter videos

4. **Poor quality output**
   - Decrease `video_quality` CRF value (lower = better)
   - Increase `output_resolution`
   - Check input video quality

### Debug Mode
```python
import logging
logging.getLogger().setLevel(logging.DEBUG)

# Run with detailed logging
editor = VideoEditorApp()
result = editor.process_video("debug_video.mp4")
```


## 📊 Performance

**Typical Processing Times:**
- 10-minute video → 15 clips: ~3-5 minutes
- Caption generation: ~30-60 seconds per clip
- Thumbnail creation: ~5-10 seconds per clip

---

**Made for content creators everywhere**

*Star ⭐ this repo if you find it useful!*
