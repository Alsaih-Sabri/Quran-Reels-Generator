# Product Requirements Document (PRD)
## Quran Reels Generator
 
---
 
## 1. Executive Summary
 
### 1.1 Product Overview
The Quran Reels Generator is an automated video creation tool designed to produce high-quality, short-form Islamic content (Reels/Shorts) featuring Quranic verses. The application combines recitation audio from renowned reciters with Uthmani script text overlays on aesthetic nature backgrounds, optimized for social media platforms like TikTok, Instagram, and YouTube Shorts.
 
### 1.2 Product Vision
To democratize Islamic content creation by providing an accessible, one-click solution for generating professional Quranic video content, enabling users to spread religious knowledge through modern social media channels.
 
### 1.3 Target Audience
- Islamic content creators
- Social media influencers focused on religious content
- Mosques and Islamic organizations
- Individual Muslims seeking to share Quranic verses
- Educational institutions teaching Quran
 
---
 
## 2. Product Architecture
 
### 2.1 Technology Stack
 
**Backend:**
- **Framework:** Flask (Python web framework)
- **Language:** Python 3.10+
- **Key Libraries:**
  - `moviepy==1.0.3` - Video editing and composition
  - `pydub` - Audio processing and trimming
  - `requests` - HTTP requests for API calls
  - `flask-cors` - Cross-origin resource sharing
 
**Frontend:**
- **Technology:** HTML5, CSS3, Vanilla JavaScript
- **UI Framework:** Custom CSS with modern design patterns
- **Fonts:** Google Fonts (Amiri, Cairo) + Dubai font family
 
**Media Processing:**
- **FFmpeg** - Video/audio encoding and processing
- **ImageMagick** - Text rendering and image manipulation
 
**External APIs:**
- `api.alquran.cloud` - Quranic text in Uthmani script
- `everyayah.com` - Audio recitations from various reciters
 
### 2.2 System Architecture
 
```
┌─────────────────┐
│   Web Browser   │
│   (UI.html)     │
└────────┬────────┘
         │ HTTP/REST
         ▼
┌─────────────────┐
│  Flask Server   │
│  (main.py)      │
│  Port: 5000     │
└────────┬────────┘
         │
    ┌────┴────┬──────────┬──────────┐
    ▼         ▼          ▼          ▼
┌────────┐ ┌──────┐ ┌────────┐ ┌────────┐
│External│ │FFmpeg│ │ImageMag│ │File    │
│APIs    │ │      │ │ick     │ │System  │
└────────┘ └──────┘ └────────┘ └────────┘
```
 
---
 
## 3. Core Features
 
### 3.1 Video Generation Pipeline
 
**Feature:** Automated video creation from Quranic verses
 
**User Flow:**
1. User selects reciter from dropdown (11 options)
2. User selects Surah (chapter) from 114 options
3. User specifies start and end verse numbers
4. User clicks "إنشاء الفيديو" (Generate Video)
5. System processes request in background
6. Real-time progress updates displayed
7. Video saved to outputs directory
8. Success notification shown
 
**Technical Implementation:**
- Background thread processing to prevent UI blocking
- Progress tracking with percentage and status messages
- Audio trimming to remove silence for perfect synchronization
- Dynamic text sizing based on verse length
- Random background video selection for variety
 
### 3.2 Reciter Selection
 
**Supported Reciters:**
1. Sheikh Abdul Basit Abdul Samad (عبدالباسط عبدالصمد)
2. Sheikh Abdul Basit Abdul Samad - Murattal (مرتل)
3. Sheikh Abdurrahman As-Sudais (عبدالرحمن السديس)
4. Sheikh Maher Al-Muaiqly (ماهر المعيقلي)
5. Sheikh Muhammad Siddiq Al-Minshawi - Mujawwad (محمد صديق المنشاوي)
6. Sheikh Saood Ash-Shuraym (سعود الشريم)
7. Sheikh Mishary Al-Afasy (مشاري العفاسي)
8. Sheikh Mahmoud Khalil Al-Hussary (محمود خليل الحصري)
9. Sheikh Abdullah Al-Hudhaify (عبدالله الحذيفي)
10. Sheikh Abu Bakr Ash-Shaatree (أبو بكر الشاطري)
11. Sheikh Mahmoud Ali Al-Banna (محمود علي البنا)
 
### 3.3 Text Rendering System
 
**Dynamic Font Sizing Algorithm:**
- **>60 words:** 16px font, 10 words per line
- **>40 words:** 20px font, 9 words per line
- **>25 words:** 25px font, 8 words per line
- **>15 words:** 30px font, 7 words per line
- **≤15 words:** 35px font, 6 words per line
 
**Text Properties:**
- Font: Dubai Bold (Arabic)
- Color: White
- Alignment: Center
- Position: Center screen
- Width constraint: 900px
- Method: Caption with auto-height
 
### 3.4 Background Video System
 
**Specifications:**
- Source: Nature videos stored in `/vision` directory
- Selection: Random to ensure variety
- Format: MP4
- Processing: Looped to match audio duration
- Naming convention: `nature_part*.mp4`
 
### 3.5 Audio Processing
 
**Features:**
- Automatic silence detection and trimming
- Threshold: dBFS - 16
- Fade-in: 0.2 seconds
- Fade-out: 0.2 seconds
- Format: MP3 (64kbps - 128kbps depending on reciter)
- Source: everyayah.com API
 
### 3.6 Progress Tracking
 
**Real-time Updates:**
- Percentage completion (0-100%)
- Status messages in Arabic
- Detailed log console
- Visual progress bar with animation
- Background thread execution
 
**Progress Stages:**
1. Clearing output folders (5%)
2. Preparing verses (10%)
3. Downloading audio per verse (10-80%)
4. Fetching text per verse (10-80%)
5. Building video segments (10-80%)
6. Concatenating segments (85%)
7. Writing final video (90%)
8. Completion (100%)
 
---
 
## 4. User Interface
 
### 4.1 Design System
 
**Color Palette:**
- Primary Gold: `#d4af37`
- Gold Light: `#f4d06f`
- Gold Dark: `#aa8a2e`
- Background Dark: `#0a0a12`
- Background Secondary: `#12121d`
- Background Card: `rgba(20, 20, 35, 0.8)`
- Text Primary: `#ffffff`
- Text Secondary: `rgba(255, 255, 255, 0.7)`
 
**Typography:**
- Primary: Cairo (Arabic sans-serif)
- Secondary: Amiri (Arabic serif)
- Monospace: Consolas (for logs)
 
**Visual Effects:**
- Glassmorphism (backdrop blur)
- Gradient overlays
- Particle animations
- Glow effects on gold elements
- Smooth transitions (0.3s ease)
 
### 4.2 Components
 
**Header:**
- Logo with animated pulse glow
- Bilingual title (Arabic/English)
- Social media links (YouTube, Instagram, Twitter, Facebook)
 
**Main Form:**
- Reciter dropdown
- Surah dropdown (114 options)
- Start verse number input with +/- buttons
- End verse number input with +/- buttons
- Generate button with loading state
 
**Progress Section:**
- Progress bar with shimmer animation
- Percentage indicator
- Status message
- Log console with scrollable output
 
**Success Message:**
- Checkmark icon
- Success text
- Fade-in animation
 
### 4.3 Responsive Design
 
**Mobile Optimizations:**
- Reduced padding on cards (25px)
- Smaller logo title (2rem)
- Adjusted button sizes
- Touch-friendly controls
- Vertical layout optimization
 
---
 
## 5. API Endpoints
 
### 5.1 GET `/`
**Description:** Serves the main UI HTML file
 
**Response:** HTML page
 
---
 
### 5.2 POST `/api/generate`
**Description:** Initiates video generation process
 
**Request Body:**
```json
{
  "reciter": "AbdulSamad_64kbps_QuranExplorer.Com",
  "surah": 1,
  "startAyah": 1,
  "endAyah": 7
}
```
 
**Response:**
```json
{
  "success": true,
  "message": "بدأ إنشاء الفيديو"
}
```
 
**Error Response:**
```json
{
  "error": "عملية إنشاء فيديو قيد التنفيذ بالفعل"
}
```
 
---
 
### 5.3 GET `/api/progress`
**Description:** Returns current generation progress
 
**Response:**
```json
{
  "percent": 45,
  "status": "جاري تحميل صوت الآية 3...",
  "log": ["[1] Clearing output folders...", "[2] Preparing 7 آيات..."],
  "is_running": true,
  "is_complete": false,
  "output_path": null,
  "error": null
}
```
 
---
 
### 5.4 GET `/api/config`
**Description:** Returns configuration data
 
**Response:**
```json
{
  "surahs": ["الفاتحة", "البقرة", ...],
  "verseCounts": {1: 7, 2: 286, ...},
  "reciters": {"الشيخ عبدالباسط عبدالصمد": "AbdulSamad_64kbps_QuranExplorer.Com", ...}
}
```
 
---
 
### 5.5 GET `/outputs/<filename>`
**Description:** Serves generated video files
 
**Response:** Video file (MP4)
 
---
 
## 6. File Structure
 
```
Quran-Reels-Generator/
├── main.py                 # Flask backend server
├── UI.html                 # Frontend interface
├── requirements.txt        # Python dependencies
├── LICENSE                 # License file
├── README.md              # Documentation
├── font.ttf               # Legacy font file
├── fonts/                 # Font directory
│   ├── DUBAI-BOLD.TTF
│   ├── DUBAI-LIGHT.TTF
│   ├── DUBAI-MEDIUM.TTF
│   └── DUBAI-REGULAR.TTF
├── vision/                # Background videos
│   └── nature_part*.mp4
└── outputs/               # Generated content (created at runtime)
    ├── audio/            # Temporary audio files
    └── video/            # Final video outputs
```
 
---
 
## 7. Video Output Specifications
 
### 7.1 Technical Specifications
 
**Video:**
- Format: MP4
- Codec: H.264 (libx264)
- FPS: 24
- Resolution: 1080x1920 (9:16 vertical)
- Orientation: Portrait
 
**Audio:**
- Codec: AAC
- Bitrate: 192kbps
- Channels: Stereo
 
**Optimization:**
- Fast start enabled (`-movflags +faststart`)
- Optimized for streaming
 
### 7.2 Naming Convention
 
```
QuranReel_{SurahName}_{StartVerse}-{EndVerse}_{Timestamp}.mp4
```
 
**Example:**
```
QuranReel_الفاتحة_1-7_20240201_123045.mp4
```
 
---
 
## 8. Data Sources
 
### 8.1 Quranic Text API
 
**Endpoint:** `https://api.alquran.cloud/v1/ayah/{surah}:{ayah}/quran-uthmani`
 
**Response Format:**
```json
{
  "data": {
    "text": "بِسْمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ"
  }
}
```
 
### 8.2 Audio Recitation API
 
**Endpoint:** `https://everyayah.com/data/{reciter_id}/{surah:03d}{ayah:03d}.mp3`
 
**Example:**
```
https://everyayah.com/data/AbdulSamad_64kbps_QuranExplorer.Com/001001.mp3
```
 
---
 
## 9. Constraints & Limitations
 
### 9.1 Technical Constraints
 
1. **Single Process:** Only one video can be generated at a time
2. **Memory:** Large verse ranges may consume significant memory
3. **Dependencies:** Requires FFmpeg and ImageMagick installation
4. **Network:** Requires internet connection for API calls
5. **Storage:** Generated videos stored locally (no cloud storage)
 
### 9.2 Content Constraints
 
1. **Verse Range:** Maximum 10 verses per video (default)
2. **Surah Coverage:** All 114 Surahs supported
3. **Verse Counts:** Validated against predefined verse counts
4. **Background Videos:** Limited to available nature videos
 
### 9.3 Platform Constraints
 
1. **Operating System:** Primarily designed for Windows (portable mode)
2. **Python Version:** Requires Python 3.10+
3. **Browser:** Modern browsers with JavaScript enabled
4. **Port:** Runs on localhost:5000 (must be available)
 
---
 
## 10. Error Handling
 
### 10.1 Error Scenarios
 
**API Failures:**
- Network timeout
- Invalid verse numbers
- Missing audio files
- API rate limiting
 
**Processing Errors:**
- FFmpeg failures
- ImageMagick errors
- Insufficient disk space
- Font rendering issues
 
**User Input Errors:**
- Invalid verse range
- Start verse > End verse
- Verse number exceeds Surah limit
 
### 10.2 Error Recovery
 
- Detailed error logging to `runlog.txt`
- User-friendly error messages in Arabic
- Progress state reset on failure
- Automatic cleanup of temporary files
 
---
 
## 11. Performance Considerations
 
### 11.1 Optimization Strategies
 
**Audio Processing:**
- Silence trimming reduces file size
- Fade effects for smooth transitions
- Parallel processing not implemented (sequential)
 
**Video Processing:**
- Background video looping instead of extending
- Text rendering cached per verse
- Segment-based composition
 
**Resource Management:**
- Temporary audio files cleaned after generation
- Video history preserved
- Background thread prevents UI blocking
 
### 11.2 Performance Metrics
 
**Typical Generation Time:**
- 1 verse: ~15-30 seconds
- 5 verses: ~1-2 minutes
- 10 verses: ~2-4 minutes
 
**Factors Affecting Performance:**
- Network speed (API calls)
- Verse length (text rendering)
- System resources (CPU, RAM)
- Background video duration
 
---
 
## 12. Security Considerations
 
### 12.1 Security Features
 
1. **Local Execution:** No cloud processing, data stays local
2. **CORS Enabled:** Controlled cross-origin access
3. **Input Validation:** Verse numbers validated against limits
4. **No Authentication:** Designed for single-user local use
 
### 12.2 Security Limitations
 
1. **No User Authentication:** Open access on localhost
2. **No Rate Limiting:** Can be overwhelmed with requests
3. **File System Access:** Direct access to local directories
4. **External Dependencies:** Relies on third-party APIs
 
---
 
## 13. Deployment
 
### 13.1 Manual Installation
 
**Prerequisites:**
- Python 3.10+
- FFmpeg installed and in PATH
- ImageMagick with legacy utilities
 
**Steps:**
```bash
# Clone repository
git clone [repository-url]
 
# Install dependencies
pip install -r requirements.txt
 
# Run application
python main.py
```
 
**Auto-launch:**
- Browser opens automatically to `http://127.0.0.1:5000`
 
### 13.2 Portable Version
 
**Features:**
- Bundled FFmpeg and ImageMagick
- No installation required
- Self-contained executable
- Fonts included
 
**Structure:**
```
bin/
├── ffmpeg/
│   ├── ffmpeg.exe
│   └── ffprobe.exe
└── imagemagick/
    ├── magick.exe
    └── config/
```
 
---
 
## 14. Future Enhancements
 
### 14.1 Potential Features
 
**Content:**
- Translation overlays (English, Urdu, etc.)
- Multiple background themes (mosques, geometric patterns)
- Custom background upload
- Verse-by-verse highlighting
- Tafsir (interpretation) text option
 
**Technical:**
- Batch video generation
- Queue system for multiple requests
- Cloud storage integration
- Video preview before generation
- Custom font selection
- Adjustable video dimensions
 
**User Experience:**
- Saved presets/templates
- Recent generations history
- Video editing capabilities
- Social media direct upload
- Thumbnail generation
- Watermark/branding options
 
**Performance:**
- Parallel processing for multiple verses
- Video generation caching
- Progressive video loading
- GPU acceleration support
 
---
 
## 15. Success Metrics
 
### 15.1 Key Performance Indicators (KPIs)
 
**Usage Metrics:**
- Number of videos generated per day
- Average verses per video
- Most popular reciters
- Most generated Surahs
 
**Technical Metrics:**
- Average generation time
- Success rate (completed vs. failed)
- Error frequency by type
- System resource utilization
 
**Quality Metrics:**
- Video output quality consistency
- Audio-text synchronization accuracy
- User satisfaction (if feedback collected)
 
---
 
## 16. Compliance & Ethics
 
### 16.1 Religious Considerations
 
- Accurate Quranic text (Uthmani script)
- Authentic recitations from verified sources
- Respectful presentation and design
- No modifications to sacred text
 
### 16.2 Copyright & Licensing
 
- Educational purposes disclaimer
- Attribution to content sources
- Open-source components properly licensed
- Recitation rights respected
 
### 16.3 Content Guidelines
 
- No commercial use without permission
- Proper attribution required
- Respectful usage encouraged
- Community guidelines adherence
 
---
 
## 17. Support & Maintenance
 
### 17.1 Documentation
 
- README.md with setup instructions
- Video tutorial available on YouTube
- Social media support channels
- Community-driven support
 
### 17.2 Maintenance Tasks
 
**Regular:**
- Dependency updates
- API endpoint monitoring
- Background video library expansion
- Bug fixes and patches
 
**Periodic:**
- Feature enhancements
- Performance optimization
- Security updates
- Documentation updates
 
---
 
## 18. Glossary
 
**Surah:** Chapter of the Quran (114 total)
**Ayah/Verse:** Individual verse within a Surah
**Uthmani Script:** Traditional Quranic text style
**Reciter/Qari:** Person who recites the Quran
**Murattal:** Clear, measured recitation style
**Mujawwad:** Melodious recitation style
**Reels/Shorts:** Short-form vertical videos for social media
**Tashkeel:** Arabic diacritical marks
 
---
 
## 19. Contact & Attribution
 
**Developer:** Arabian AI School
- YouTube: [@arabianAiSchool](https://youtube.com/@arabianAiSchool)
- Instagram: [@arabianaischool](https://instagram.com/arabianaischool)
- Twitter: [@arabianaischool](https://twitter.com/arabianaischool)
- Facebook: [@arabianaischool](https://facebook.com/arabianaischool)
 
**Tutorial:** https://youtu.be/TL1Gim1VT40
**Portable Version:** Available via Google Drive
 
---
 
## 20. Version History
 
**Current Version:** 1.0
- Initial release with core functionality
- 11 reciters supported
- All 114 Surahs available
- Automated video generation
- Real-time progress tracking
- Portable Windows version
 
---
 
**Document Version:** 1.0  
**Last Updated:** February 1, 2026  
**Status:** Active Development