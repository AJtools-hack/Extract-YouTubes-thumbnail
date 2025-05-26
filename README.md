 <!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-VVMFTP1HCQ"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-VVMFTP1HCQ');
</script>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aj-Tools - YouTube Thumbnail Extractor</title>
    <meta name="description" content="Extract high-quality YouTube thumbnails in multiple resolutions: 360p, 480p, 720p HD, 1080p, 2K, and 4K. Mobile-friendly with instant preview and download.">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* CSS Variables */
        :root {
            --primary-color: #5C63FF;
            --primary-dark: #4549cc;
            --secondary-color: #F0F2FD;
            --text-color: #333333;
            --light-gray: #f8f9fa;
            --mid-gray: #e9ecef;
            --dark-gray: #6c757d;
            --error-color: #dc3545;
            --success-color: #28a745;
            --warning-color: #ffc107;
            --shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            --border-radius: 12px;
            --transition: all 0.3s ease;
        }

        /* Reset and Base Styles */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            line-height: 1.6;
            color: var(--text-color);
            background: linear-gradient(135deg, var(--secondary-color) 0%, #ffffff 100%);
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 1rem;
        }

        /* Header Styles */
        header {
            text-align: center;
            padding: 2rem 0;
            margin-bottom: 2rem;
        }

        .logo {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .logo i {
            font-size: 2.5rem;
            color: var(--primary-color);
        }

        h1 {
            font-size: 2.8rem;
            color: var(--primary-color);
            font-weight: 700;
            letter-spacing: -0.02em;
        }

        .subtitle {
            font-size: 1.1rem;
            color: var(--dark-gray);
            margin-top: 0.5rem;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }

        /* Input Section */
        .input-section {
            background: white;
            padding: 2rem;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            margin-bottom: 2rem;
            position: relative;
            overflow: hidden;
        }

        .input-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--primary-color) 0%, #7c83ff 100%);
        }

        .input-group {
            display: flex;
            gap: 0.5rem;
            align-items: stretch;
        }

        .input-wrapper {
            flex: 1;
            position: relative;
        }

        .input-icon {
            position: absolute;
            left: 1rem;
            top: 50%;
            transform: translateY(-50%);
            color: var(--dark-gray);
            z-index: 2;
        }

        #youtubeUrl {
            width: 100%;
            padding: 1rem 1rem 1rem 2.5rem;
            border: 2px solid var(--mid-gray);
            border-radius: var(--border-radius);
            font-size: 1rem;
            transition: var(--transition);
            background: white;
        }

        #youtubeUrl:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(92, 99, 255, 0.1);
        }

        #extractBtn {
            background: linear-gradient(135deg, var(--primary-color) 0%, #7c83ff 100%);
            color: white;
            border: none;
            padding: 1rem 1.5rem;
            border-radius: var(--border-radius);
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            transition: var(--transition);
            white-space: nowrap;
        }

        #extractBtn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(92, 99, 255, 0.3);
        }

        #extractBtn:active {
            transform: translateY(0);
        }

        .loading {
            opacity: 0.7;
            pointer-events: none;
        }

        .loading .btn-text {
            display: none;
        }

        .loading .spinner {
            display: inline-block;
        }

        .spinner {
            display: none;
            width: 16px;
            height: 16px;
            border: 2px solid transparent;
            border-top: 2px solid currentColor;
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .error-message {
            color: var(--error-color);
            margin-top: 1rem;
            font-size: 0.9rem;
            padding: 0.5rem;
            border-radius: 6px;
            background-color: rgba(220, 53, 69, 0.1);
            border-left: 4px solid var(--error-color);
            display: none;
        }

        /* Results Section */
        .results-section {
            background: white;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            margin-bottom: 2rem;
            overflow: hidden;
            display: none;
        }

        .results-header {
            background: linear-gradient(135deg, var(--primary-color) 0%, #7c83ff 100%);
            color: white;
            padding: 1.5rem 2rem;
            text-align: center;
        }

        .results-header h2 {
            font-size: 1.5rem;
            margin-bottom: 0.5rem;
        }

        .video-info {
            background: var(--light-gray);
            padding: 1rem 2rem;
            border-bottom: 1px solid var(--mid-gray);
        }

        .video-title {
            font-weight: 600;
            color: var(--text-color);
            margin-bottom: 0.5rem;
        }

        .video-id {
            font-size: 0.9rem;
            color: var(--dark-gray);
            font-family: monospace;
        }

        /* Thumbnail Grid */
        .thumbnails-grid {
            padding: 2rem;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.5rem;
        }

        .thumbnail-card {
            border: 1px solid var(--mid-gray);
            border-radius: var(--border-radius);
            overflow: hidden;
            transition: var(--transition);
            background: white;
        }

        .thumbnail-card:hover {
            transform: translateY(-4px);
            box-shadow: var(--shadow);
        }

        .thumbnail-header {
            padding: 1rem;
            background: var(--light-gray);
            border-bottom: 1px solid var(--mid-gray);
        }

        .resolution-title {
            font-weight: 600;
            margin-bottom: 0.25rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .resolution-badge {
            background: var(--primary-color);
            color: white;
            padding: 0.25rem 0.5rem;
            border-radius: 4px;
            font-size: 0.8rem;
            font-weight: 600;
        }

        .resolution-desc {
            font-size: 0.9rem;
            color: var(--dark-gray);
        }

        .thumbnail-content {
            position: relative;
        }

        .thumbnail-image {
            width: 100%;
            height: auto;
            display: block;
            transition: var(--transition);
        }

        .thumbnail-overlay {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(transparent, rgba(0, 0, 0, 0.8));
            padding: 1rem;
            transform: translateY(100%);
            transition: var(--transition);
        }

        .thumbnail-card:hover .thumbnail-overlay {
            transform: translateY(0);
        }

        .download-btn {
            background: var(--primary-color);
            color: white;
            text-decoration: none;
            padding: 0.75rem 1rem;
            border-radius: 6px;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            font-weight: 600;
            transition: var(--transition);
            width: 100%;
            justify-content: center;
        }

        .download-btn:hover {
            background: var(--primary-dark);
            transform: translateY(-1px);
        }

        /* No Results Section */
        .no-results {
            background: white;
            padding: 3rem 2rem;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            text-align: center;
            display: none;
        }

        .no-results i {
            font-size: 3rem;
            color: var(--dark-gray);
            margin-bottom: 1rem;
        }

        .no-results h2 {
            color: var(--text-color);
            margin-bottom: 1rem;
        }

        .no-results ul {
            text-align: left;
            max-width: 400px;
            margin: 1rem auto 0;
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 2rem 0;
            color: var(--dark-gray);
            font-size: 0.9rem;
        }

        footer p {
            margin-bottom: 0.5rem;
        }

        /* Mobile Responsiveness */
        @media (max-width: 768px) {
            .container {
                padding: 0.5rem;
            }

            header {
                padding: 1rem 0;
            }

            h1 {
                font-size: 2.2rem;
            }

            .subtitle {
                font-size: 1rem;
            }

            .input-section {
                padding: 1.5rem;
            }

            .input-group {
                flex-direction: column;
                gap: 1rem;
            }

            #extractBtn {
                width: 100%;
                justify-content: center;
            }

            .thumbnails-grid {
                grid-template-columns: 1fr;
                padding: 1rem;
                gap: 1rem;
            }

            .thumbnail-overlay {
                transform: translateY(0);
                position: relative;
                background: var(--light-gray);
                padding: 1rem;
            }

            .results-header,
            .video-info {
                padding: 1rem;
            }
        }

        @media (max-width: 480px) {
            h1 {
                font-size: 1.8rem;
            }

            .logo i {
                font-size: 2rem;
            }

            .input-section {
                padding: 1rem;
            }

            .thumbnails-grid {
                padding: 0.5rem;
            }
        }

        /* Accessibility */
        @media (prefers-reduced-motion: reduce) {
            * {
                animation-duration: 0.01ms !important;
                animation-iteration-count: 1 !important;
                transition-duration: 0.01ms !important;
            }
        }

        /* Focus styles for keyboard navigation */
        .download-btn:focus,
        #extractBtn:focus,
        #youtubeUrl:focus {
            outline: 2px solid var(--primary-color);
            outline-offset: 2px;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo">
                <i class="fas fa-tools"></i>
                <h1>Aj-Tools</h1>
            </div>
            <p class="subtitle">YouTube Thumbnail Extractor</p>
            <p class="subtitle">Extract high-quality thumbnails from YouTube videos in multiple resolutions: 360p, 480p, 720p HD, 1080p, 2K, and 4K. Simply paste any YouTube link and download instantly.</p>
        </header>

        <main>
            <div class="input-section">
                <form id="youtubeForm">
                    <div class="input-group">
                        <div class="input-wrapper">
                            <span class="input-icon"><i class="fas fa-link"></i></span>
                            <input type="url" id="youtubeUrl" placeholder="Paste YouTube video URL here..." 
                                   required autocomplete="url">
                        </div>
                        <button type="submit" id="extractBtn">
                            <span class="btn-text">
                                <i class="fas fa-search"></i> Extract Thumbnails
                            </span>
                            <span class="spinner"></span>
                        </button>
                    </div>
                    <div class="error-message" id="errorMsg"></div>
                </form>
            </div>

            <div class="no-results" id="noResults">
                <i class="fas fa-exclamation-triangle"></i>
                <h2>No Thumbnails Available</h2>
                <p>We couldn't retrieve thumbnails for this video. This might happen if:</p>
                <ul>
                    <li>The video is private or unlisted</li>
                    <li>The video has been deleted</li>
                    <li>The URL is not a valid YouTube video link</li>
                    <li>The video is too new (thumbnails not generated yet)</li>
                </ul>
            </div>

            <div class="results-section" id="resultsContainer">
                <div class="results-header">
                    <h2>Available Thumbnails</h2>
                    <p>Click on any thumbnail to download in your preferred resolution</p>
                </div>
                
                <div class="video-info" id="videoInfo">
                    <div class="video-title" id="videoTitle">Loading video information...</div>
                    <div class="video-id">Video ID: <span id="videoIdDisplay"></span></div>
                </div>

                <div class="thumbnails-grid">
                    <!-- 360p Thumbnail -->
                    <div class="thumbnail-card">
                        <div class="thumbnail-header">
                            <div class="resolution-title">
                                360p Quality
                                <span class="resolution-badge">360p</span>
                            </div>
                            <div class="resolution-desc">Basic quality (480×360)</div>
                        </div>
                        <div class="thumbnail-content">
                            <img id="thumb360" class="thumbnail-image" src="" alt="360p Thumbnail">
                            <div class="thumbnail-overlay">
                                <a href="#" class="download-btn" id="download360" download>
                                    <i class="fas fa-download"></i> Download 360p
                                </a>
                            </div>
                        </div>
                    </div>

                    <!-- 480p Thumbnail -->
                    <div class="thumbnail-card">
                        <div class="thumbnail-header">
                            <div class="resolution-title">
                                480p Quality
                                <span class="resolution-badge">480p</span>
                            </div>
                            <div class="resolution-desc">Standard quality (640×480)</div>
                        </div>
                        <div class="thumbnail-content">
                            <img id="thumb480" class="thumbnail-image" src="" alt="480p Thumbnail">
                            <div class="thumbnail-overlay">
                                <a href="#" class="download-btn" id="download480" download>
                                    <i class="fas fa-download"></i> Download 480p
                                </a>
                            </div>
                        </div>
                    </div>

                    <!-- 720p HD Thumbnail -->
                    <div class="thumbnail-card">
                        <div class="thumbnail-header">
                            <div class="resolution-title">
                                720p HD Quality
                                <span class="resolution-badge">HD</span>
                            </div>
                            <div class="resolution-desc">High quality (1280×720)</div>
                        </div>
                        <div class="thumbnail-content">
                            <img id="thumbHD" class="thumbnail-image" src="" alt="HD Thumbnail">
                            <div class="thumbnail-overlay">
                                <a href="#" class="download-btn" id="downloadHD" download>
                                    <i class="fas fa-download"></i> Download HD
                                </a>
                            </div>
                        </div>
                    </div>

                    <!-- 1080p Thumbnail -->
                    <div class="thumbnail-card">
                        <div class="thumbnail-header">
                            <div class="resolution-title">
                                1080p Quality
                                <span class="resolution-badge">1080p</span>
                            </div>
                            <div class="resolution-desc">Full HD quality (1920×1080)</div>
                        </div>
                        <div class="thumbnail-content">
                            <img id="thumb1080" class="thumbnail-image" src="" alt="1080p Thumbnail">
                            <div class="thumbnail-overlay">
                                <a href="#" class="download-btn" id="download1080" download>
                                    <i class="fas fa-download"></i> Download 1080p
                                </a>
                            </div>
                        </div>
                    </div>

                    <!-- 2K Thumbnail -->
                    <div class="thumbnail-card">
                        <div class="thumbnail-header">
                            <div class="resolution-title">
                                2K Quality
                                <span class="resolution-badge">2K</span>
                            </div>
                            <div class="resolution-desc">Ultra quality (2048×1152)</div>
                        </div>
                        <div class="thumbnail-content">
                            <img id="thumb2K" class="thumbnail-image" src="" alt="2K Thumbnail">
                            <div class="thumbnail-overlay">
                                <a href="#" class="download-btn" id="download2K" download>
                                    <i class="fas fa-download"></i> Download 2K
                                </a>
                            </div>
                        </div>
                    </div>

                    <!-- 4K Thumbnail -->
                    <div class="thumbnail-card">
                        <div class="thumbnail-header">
                            <div class="resolution-title">
                                4K Quality
                                <span class="resolution-badge">4K</span>
                            </div>
                            <div class="resolution-desc">Maximum quality (3840×2160)</div>
                        </div>
                        <div class="thumbnail-content">
                            <img id="thumb4K" class="thumbnail-image" src="" alt="4K Thumbnail">
                            <div class="thumbnail-overlay">
                                <a href="#" class="download-btn" id="download4K" download>
                                    <i class="fas fa-download"></i> Download 4K
                                </a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </main>

        <footer>
            <p><strong>Aj-Tools</strong> - YouTube Thumbnail Extractor © 2023</p>
            <p>This tool extracts thumbnails from publicly available YouTube videos for personal use.</p>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // DOM Elements
            const form = document.getElementById('youtubeForm');
            const urlInput = document.getElementById('youtubeUrl');
            const extractBtn = document.getElementById('extractBtn');
            const errorMsg = document.getElementById('errorMsg');
            const noResults = document.getElementById('noResults');
            const resultsContainer = document.getElementById('resultsContainer');
            const videoIdDisplay = document.getElementById('videoIdDisplay');
            const videoTitle = document.getElementById('videoTitle');
            
            // Thumbnail elements
            const thumbnails = {
                '360': { img: document.getElementById('thumb360'), download: document.getElementById('download360') },
                '480': { img: document.getElementById('thumb480'), download: document.getElementById('download480') },
                'HD': { img: document.getElementById('thumbHD'), download: document.getElementById('downloadHD') },
                '1080': { img: document.getElementById('thumb1080'), download: document.getElementById('download1080') },
                '2K': { img: document.getElementById('thumb2K'), download: document.getElementById('download2K') },
                '4K': { img: document.getElementById('thumb4K'), download: document.getElementById('download4K') }
            };

            // Hide results initially
            hideAllSections();

            // Form submission handler
            form.addEventListener('submit', function(e) {
                e.preventDefault();
                
                // Clear previous messages
                hideError();
                
                // Get and validate URL
                const youtubeUrl = urlInput.value.trim();
                if (!youtubeUrl) {
                    showError('Please enter a YouTube URL');
                    return;
                }
                
                // Extract video ID
                const videoId = extractVideoId(youtubeUrl);
                if (!videoId) {
                    showError('Please enter a valid YouTube video URL');
                    showNoResults();
                    return;
                }
                
                // Show loading state
                setLoadingState(true);
                
                // Extract thumbnails
                extractThumbnails(videoId);
            });

            // Real-time URL validation
            urlInput.addEventListener('input', function() {
                const url = this.value.trim();
                if (url && !extractVideoId(url)) {
                    this.style.borderColor = 'var(--error-color)';
                } else {
                    this.style.borderColor = '';
                }
            });

            // Auto-extract on paste
            urlInput.addEventListener('paste', function() {
                setTimeout(() => {
                    const url = this.value.trim();
                    if (url && extractVideoId(url)) {
                        form.dispatchEvent(new Event('submit'));
                    }
                }, 100);
            });

            function extractVideoId(url) {
                // Comprehensive regex patterns for YouTube URLs
                const patterns = [
                    /(?:youtube\.com\/(?:[^\/]+\/.+\/|(?:v|e(?:mbed)?)\/|.*[?&]v=)|youtu\.be\/)([^"&?\/\s]{11})/i,
                    /^([a-zA-Z0-9_-]{11})$/
                ];
                
                for (const pattern of patterns) {
                    const match = url.match(pattern);
                    if (match && match[1]) {
                        return match[1];
                    }
                }
                return null;
            }

            function extractThumbnails(videoId) {
                // YouTube thumbnail URLs with different qualities
                const thumbnailUrls = {
                    '360': `https://img.youtube.com/vi/${videoId}/hqdefault.jpg`,     // 480×360
                    '480': `https://img.youtube.com/vi/${videoId}/sddefault.jpg`,    // 640×480
                    'HD': `https://img.youtube.com/vi/${videoId}/maxresdefault.jpg`, // 1280×720
                    '1080': `https://img.youtube.com/vi/${videoId}/maxresdefault.jpg`, // Same as HD
                    '2K': `https://img.youtube.com/vi/${videoId}/maxresdefault.jpg`,   // Same as HD
                    '4K': `https://img.youtube.com/vi/${videoId}/maxresdefault.jpg`    // Same as HD
                };

                // Check if main thumbnail exists
                checkImageExists(thumbnailUrls.HD, (exists) => {
                    setLoadingState(false);
                    
                    if (exists) {
                        displayThumbnails(videoId, thumbnailUrls);
                    } else {
                        // Fallback to lower quality
                        checkImageExists(thumbnailUrls['480'], (exists480) => {
                            if (exists480) {
                                displayThumbnails(videoId, thumbnailUrls);
                            } else {
                                showNoResults();
                            }
                        });
                    }
                });
            }

            function displayThumbnails(videoId, urls) {
                // Update video info
                videoIdDisplay.textContent = videoId;
                videoTitle.textContent = `Video ID: ${videoId}`;
                
                // Set thumbnail images and download links
                Object.keys(thumbnails).forEach(quality => {
                    const thumbElement = thumbnails[quality];
                    const url = urls[quality];
                    
                    // Set image source
                    thumbElement.img.src = url;
                    thumbElement.img.onerror = function() {
                        // Fallback to lower quality if image fails to load
                        this.src = urls['480'] || urls['360'];
                    };
                    
                    // Set download link
                    thumbElement.download.href = url;
                    thumbElement.download.download = `aj-tools-thumbnail-${videoId}-${quality.toLowerCase()}.jpg`;
                    
                    // Add click handler for direct download
                    thumbElement.download.addEventListener('click', function(e) {
                        e.preventDefault();
                        downloadImage(url, this.download);
                    });
                });
                
                // Show results
                showResults();
            }

            function downloadImage(imageUrl, filename) {
                // Create a temporary anchor element to trigger download
                const link = document.createElement('a');
                link.href = imageUrl;
                link.download = filename;
                link.target = '_blank';
                
                // Add to DOM temporarily and trigger click
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
            }

            function checkImageExists(url, callback) {
                const img = new Image();
                img.onload = () => callback(true);
                img.onerror = () => callback(false);
                img.src = url;
            }

            function setLoadingState(loading) {
                if (loading) {
                    extractBtn.classList.add('loading');
                    extractBtn.disabled = true;
                } else {
                    extractBtn.classList.remove('loading');
                    extractBtn.disabled = false;
                }
            }

            function showError(message) {
                errorMsg.textContent = message;
                errorMsg.style.display = 'block';
            }

            function hideError() {
                errorMsg.style.display = 'none';
            }

            function showResults() {
                hideAllSections();
                resultsContainer.style.display = 'block';
            }

            function showNoResults() {
                hideAllSections();
                noResults.style.display = 'block';
            }

            function hideAllSections() {
                resultsContainer.style.display = 'none';
                noResults.style.display = 'none';
            }

            // Add smooth scrolling to results
            function scrollToResults() {
                setTimeout(() => {
                    const target = document.querySelector('.results-section:not([style*="display: none"])');
                    if (target) {
                        target.scrollIntoView({ behavior: 'smooth', block: 'start' });
                    }
                }, 100);
            }

            // Update form submission to include scrolling
            const originalShowResults = showResults;
            const originalShowNoResults = showNoResults;
            
            showResults = function() {
                originalShowResults();
                scrollToResults();
            };
            
            showNoResults = function() {
                originalShowNoResults();
                scrollToResults();
            };
        });
    </script>
</body>
</html>
