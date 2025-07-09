<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Upscaler Pro</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            color: #fff;
        }
        
        header {
            text-align: center;
            padding: 30px 0;
            width: 100%;
            max-width: 1200px;
        }
        
        h1 {
            font-size: 3.5rem;
            margin-bottom: 10px;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
            background: linear-gradient(to right, #ff8a00, #da1b60);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
            max-width: 700px;
            margin: 0 auto 25px;
        }
        
        .container {
            display: flex;
            flex-wrap: wrap;
            gap: 30px;
            width: 100%;
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .upload-section {
            flex: 1;
            min-width: 300px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .preview-section {
            flex: 2;
            min-width: 500px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .section-title {
            font-size: 1.8rem;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
            color: #ffd166;
        }
        
        .upload-area {
            border: 3px dashed rgba(255, 255, 255, 0.4);
            border-radius: 15px;
            padding: 40px 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            background: rgba(0, 0, 0, 0.1);
        }
        
        .upload-area:hover {
            background: rgba(0, 0, 0, 0.2);
            border-color: #ffd166;
        }
        
        .upload-icon {
            font-size: 5rem;
            margin-bottom: 20px;
            color: #ffd166;
        }
        
        .upload-text {
            font-size: 1.2rem;
            margin-bottom: 15px;
        }
        
        .upload-btn {
            background: linear-gradient(to right, #ff8a00, #da1b60);
            color: white;
            border: none;
            padding: 12px 30px;
            font-size: 1.1rem;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            margin-top: 10px;
        }
        
        .upload-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .controls {
            margin-top: 30px;
        }
        
        .control-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-size: 1.1rem;
        }
        
        select, input {
            width: 100%;
            padding: 12px;
            border-radius: 10px;
            border: none;
            background: rgba(0, 0, 0, 0.2);
            color: white;
            font-size: 1rem;
        }
        
        .upscale-btn {
            background: linear-gradient(to right, #00c6ff, #0072ff);
            color: white;
            border: none;
            width: 100%;
            padding: 15px;
            font-size: 1.2rem;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            margin-top: 20px;
        }
        
        .upscale-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 20px rgba(0, 114, 255, 0.4);
        }
        
        .preview-container {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            justify-content: center;
        }
        
        .image-box {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 15px;
            padding: 15px;
            text-align: center;
            width: 100%;
            max-width: 450px;
        }
        
        .image-box h3 {
            margin-bottom: 15px;
            color: #ffd166;
        }
        
        .image-preview {
            width: 100%;
            border-radius: 10px;
            max-height: 400px;
            object-fit: contain;
            background: #000;
        }
        
        .placeholder {
            width: 100%;
            height: 300px;
            background: rgba(0, 0, 0, 0.1);
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: rgba(255, 255, 255, 0.5);
            font-size: 1.2rem;
        }
        
        .image-info {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
            font-size: 0.9rem;
            opacity: 0.8;
        }
        
        .comparison-container {
            width: 100%;
            margin-top: 30px;
            display: none;
        }
        
        .comparison-title {
            text-align: center;
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: #ffd166;
        }
        
        .comparison-box {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 15px;
            padding: 20px;
        }
        
        .comparison-slider {
            position: relative;
            max-width: 800px;
            margin: 0 auto;
            overflow: hidden;
            border-radius: 10px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
        }
        
        .comparison-before, .comparison-after {
            position: absolute;
            top: 0;
            left: 0;
            height: 100%;
            overflow: hidden;
        }
        
        .comparison-before {
            width: 50%;
            z-index: 2;
        }
        
        .comparison-before img, .comparison-after img {
            width: 800px;
            height: auto;
            display: block;
        }
        
        .comparison-resize {
            position: absolute;
            top: 0;
            left: 50%;
            width: 3px;
            height: 100%;
            background: white;
            cursor: ew-resize;
            z-index: 3;
        }
        
        .comparison-resize::before {
            content: "";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: white;
            opacity: 0.7;
        }
        
        .comparison-resize::after {
            content: "↔";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: #333;
            font-size: 20px;
            font-weight: bold;
        }
        
        .download-btn {
            display: block;
            background: linear-gradient(to right, #0f9d58, #00b09b);
            color: white;
            border: none;
            padding: 12px 30px;
            font-size: 1.1rem;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            margin: 30px auto 0;
            text-align: center;
            text-decoration: none;
            width: fit-content;
        }
        
        .download-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .loading {
            display: none;
            text-align: center;
            padding: 20px;
        }
        
        .spinner {
            border: 5px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top: 5px solid #ffd166;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            margin: 0 auto 20px;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        footer {
            margin-top: 40px;
            text-align: center;
            padding: 20px;
            font-size: 0.9rem;
            opacity: 0.8;
            width: 100%;
            max-width: 1200px;
        }
        
        @media (max-width: 900px) {
            .container {
                flex-direction: column;
            }
            
            .preview-section, .upload-section {
                min-width: 100%;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1><i class="fas fa-expand-alt"></i> Image Upscaler Pro</h1>
        <p class="subtitle">Enhance your images with our AI-powered upscaling technology. Increase resolution without quality loss.</p>
    </header>
    
    <div class="container">
        <div class="upload-section">
            <h2 class="section-title"><i class="fas fa-cloud-upload-alt"></i> Upload Image</h2>
            
            <div class="upload-area" id="dropArea">
                <i class="fas fa-file-upload upload-icon"></i>
                <p class="upload-text">Drag & drop your image here</p>
                <p>OR</p>
                <button class="upload-btn">Select Image</button>
                <input type="file" id="fileInput" accept="image/*" style="display: none">
            </div>
            
            <div class="controls">
                <div class="control-group">
                    <label for="upscaleFactor"><i class="fas fa-search-plus"></i> Upscale Factor</label>
                    <select id="upscaleFactor">
                        <option value="2">2x (Recommended)</option>
                        <option value="3">3x</option>
                        <option value="4">4x (Max)</option>
                    </select>
                </div>
                
                <div class="control-group">
                    <label for="noiseReduction"><i class="fas fa-broom"></i> Noise Reduction</label>
                    <select id="noiseReduction">
                        <option value="low">Low</option>
                        <option value="medium" selected>Medium</option>
                        <option value="high">High</option>
                    </select>
                </div>
                
                <div class="control-group">
                    <label for="sharpness"><i class="fas fa-cut"></i> Sharpness Enhancement</label>
                    <select id="sharpness">
                        <option value="low">Low</option>
                        <option value="medium" selected>Medium</option>
                        <option value="high">High</option>
                    </select>
                </div>
                
                <button class="upscale-btn" id="upscaleBtn">
                    <i class="fas fa-magic"></i> Upscale Image
                </button>
            </div>
        </div>
        
        <div class="preview-section">
            <h2 class="section-title"><i class="fas fa-image"></i> Preview</h2>
            
            <div class="preview-container">
                <div class="image-box">
                    <h3>Original Image</h3>
                    <div class="original-preview">
                        <div class="placeholder" id="originalPlaceholder">
                            <p>No image selected</p>
                        </div>
                        <img class="image-preview" id="originalPreview" style="display: none">
                    </div>
                    <div class="image-info">
                        <span>Size: <span id="originalSize">0 KB</span></span>
                        <span>Dimensions: <span id="originalDimensions">0×0</span></span>
                    </div>
                </div>
                
                <div class="image-box">
                    <h3>Upscaled Image</h3>
                    <div class="upscaled-preview">
                        <div class="placeholder" id="upscaledPlaceholder">
                            <p>Upscaled image will appear here</p>
                        </div>
                        <img class="image-preview" id="upscaledPreview" style="display: none">
                    </div>
                    <div class="image-info">
                        <span>Size: <span id="upscaledSize">0 KB</span></span>
                        <span>Dimensions: <span id="upscaledDimensions">0×0</span></span>
                    </div>
                </div>
            </div>
            
            <div class="loading" id="loadingIndicator">
                <div class="spinner"></div>
                <p>Processing your image with AI enhancement...</p>
                <p>This may take a few seconds</p>
            </div>
            
            <div class="comparison-container" id="comparisonContainer">
                <h3 class="comparison-title">Before & After Comparison</h3>
                <div class="comparison-box">
                    <div class="comparison-slider" id="comparisonSlider">
                        <img id="comparisonAfter" class="comparison-after">
                        <div class="comparison-before">
                            <img id="comparisonBefore">
                        </div>
                        <div class="comparison-resize" id="comparisonResize"></div>
                    </div>
                </div>
                
                <a href="#" class="download-btn" id="downloadBtn">
                    <i class="fas fa-download"></i> Download Upscaled Image
                </a>
            </div>
        </div>
    </div>
    
    <footer>
        <p>© 2023 Image Upscaler Pro | AI-Powered Image Enhancement | All processing happens in your browser - no server upload required</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // DOM Elements
            const fileInput = document.getElementById('fileInput');
            const dropArea = document.getElementById('dropArea');
            const originalPreview = document.getElementById('originalPreview');
            const upscaledPreview = document.getElementById('upscaledPreview');
            const originalPlaceholder = document.getElementById('originalPlaceholder');
            const upscaledPlaceholder = document.getElementById('upscaledPlaceholder');
            const upscaleBtn = document.getElementById('upscaleBtn');
            const loadingIndicator = document.getElementById('loadingIndicator');
            const comparisonContainer = document.getElementById('comparisonContainer');
            const downloadBtn = document.getElementById('downloadBtn');
            const comparisonBefore = document.getElementById('comparisonBefore');
            const comparisonAfter = document.getElementById('comparisonAfter');
            const comparisonResize = document.getElementById('comparisonResize');
            const comparisonSlider = document.getElementById('comparisonSlider');
            
            // Image info elements
            const originalSize = document.getElementById('originalSize');
            const upscaledSize = document.getElementById('upscaledSize');
            const originalDimensions = document.getElementById('originalDimensions');
            const upscaledDimensions = document.getElementById('upscaledDimensions');
            
            // Variables to store image data
            let originalImage = null;
            let upscaledImage = null;
            
            // Event listeners for file selection
            dropArea.addEventListener('click', () => fileInput.click());
            fileInput.addEventListener('change', handleFileSelect);
            
            // Drag and drop events
            ['dragenter', 'dragover', 'dragleave', 'drop'].forEach(eventName => {
                dropArea.addEventListener(eventName, preventDefaults, false);
            });
            
            function preventDefaults(e) {
                e.preventDefault();
                e.stopPropagation();
            }
            
            ['dragenter', 'dragover'].forEach(eventName => {
                dropArea.addEventListener(eventName, highlight, false);
            });
            
            ['dragleave', 'drop'].forEach(eventName => {
                dropArea.addEventListener(eventName, unhighlight, false);
            });
            
            function highlight() {
                dropArea.style.borderColor = '#ffd166';
                dropArea.style.backgroundColor = 'rgba(0, 0, 0, 0.2)';
            }
            
            function unhighlight() {
                dropArea.style.borderColor = 'rgba(255, 255, 255, 0.4)';
                dropArea.style.backgroundColor = 'rgba(0, 0, 0, 0.1)';
            }
            
            dropArea.addEventListener('drop', handleDrop, false);
            
            function handleDrop(e) {
                const dt = e.dataTransfer;
                const files = dt.files;
                if (files.length) {
                    handleFiles(files[0]);
                }
            }
            
            function handleFileSelect(e) {
                const file = e.target.files[0];
                if (file) {
                    handleFiles(file);
                }
            }
            
            function handleFiles(file) {
                if (!file.type.match('image.*')) {
                    alert('Please select an image file.');
                    return;
                }
                
                const reader = new FileReader();
                reader.onload = function(e) {
                    originalImage = new Image();
                    originalImage.onload = function() {
                        // Display original image
                        originalPreview.src = originalImage.src;
                        originalPreview.style.display = 'block';
                        originalPlaceholder.style.display = 'none';
                        
                        // Update image info
                        const dimensions = `${originalImage.width}×${originalImage.height}`;
                        originalDimensions.textContent = dimensions;
                        originalSize.textContent = formatFileSize(file.size);
                        
                        // Reset upscaled image
                        upscaledPreview.style.display = 'none';
                        upscaledPlaceholder.style.display = 'block';
                        comparisonContainer.style.display = 'none';
                        
                        // Clear previous results
                        upscaledImage = null;
                    };
                    originalImage.src = e.target.result;
                };
                reader.readAsDataURL(file);
            }
            
            // Upscale button event
            upscaleBtn.addEventListener('click', upscaleImage);
            
            // Format file size
            function formatFileSize(bytes) {
                if (bytes === 0) return '0 Bytes';
                const k = 1024;
                const sizes = ['Bytes', 'KB', 'MB'];
                const i = Math.floor(Math.log(bytes) / Math.log(k));
                return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
            }
            
            // Upscale image function
            function upscaleImage() {
                if (!originalImage) {
                    alert('Please select an image first.');
                    return;
                }
                
                // Show loading indicator
                loadingIndicator.style.display = 'block';
                upscaledPlaceholder.style.display = 'none';
                
                // Simulate processing delay
                setTimeout(() => {
                    // Create a canvas to simulate upscaling
                    const canvas = document.createElement('canvas');
                    const scaleFactor = parseInt(document.getElementById('upscaleFactor').value);
                    const noiseReduction = document.getElementById('noiseReduction').value;
                    const sharpness = document.getElementById('sharpness').value;
                    
                    // Calculate new dimensions
                    const newWidth = originalImage.width * scaleFactor;
                    const newHeight = originalImage.height * scaleFactor;
                    
                    // Set canvas dimensions
                    canvas.width = newWidth;
                    canvas.height = newHeight;
                    
                    const ctx = canvas.getContext('2d');
                    
                    // Draw original image to canvas (simulating upscale)
                    ctx.drawImage(originalImage, 0, 0, newWidth, newHeight);
                    
                    // Apply some filters to simulate enhancement
                    applyImageEnhancement(ctx, canvas, noiseReduction, sharpness);
                    
                    // Get the upscaled image data
                    const upscaledDataURL = canvas.toDataURL('image/jpeg', 0.9);
                    
                    // Create upscaled image
                    upscaledImage = new Image();
                    upscaledImage.onload = function() {
                        // Display upscaled image
                        upscaledPreview.src = upscaledImage.src;
                        upscaledPreview.style.display = 'block';
                        
                        // Update image info
                        const dimensions = `${newWidth}×${newHeight}`;
                        upscaledDimensions.textContent = dimensions;
                        
                        // Estimate file size (this is just an approximation)
                        const sizeEstimate = originalImage.src.length * (scaleFactor * 0.75);
                        upscaledSize.textContent = formatFileSize(sizeEstimate);
                        
                        // Hide loading indicator
                        loadingIndicator.style.display = 'none';
                        
                        // Show comparison and download
                        showComparison();
                    };
                    upscaledImage.src = upscaledDataURL;
                }, 2000); // Simulate 2 seconds processing time
            }
            
            // Apply filters to simulate image enhancement
            function applyImageEnhancement(ctx, canvas, noiseReduction, sharpness) {
                const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
                const data = imageData.data;
                
                // Apply noise reduction simulation
                if (noiseReduction !== 'low') {
                    const strength = noiseReduction === 'medium' ? 1 : 2;
                    for (let i = 0; i < data.length; i += 4) {
                        // Simple noise reduction by averaging nearby pixels
                        if (i > 4 && i < data.length - 8) {
                            data[i] = (data[i] + data[i - 4]) / 2;
                            data[i + 1] = (data[i + 1] + data[i - 3]) / 2;
                            data[i + 2] = (data[i + 2] + data[i - 2]) / 2;
                        }
                    }
                }
                
                // Apply sharpness simulation
                if (sharpness !== 'low') {
                    const strength = sharpness === 'medium' ? 0.3 : 0.5;
                    for (let i = 4; i < data.length - 4; i += 4) {
                        // Simple sharpening filter
                        data[i] = data[i] + (data[i] - data[i - 4]) * strength;
                        data[i + 1] = data[i + 1] + (data[i + 1] - data[i - 3]) * strength;
                        data[i + 2] = data[i + 2] + (data[i + 2] - data[i - 2]) * strength;
                    }
                }
                
                ctx.putImageData(imageData, 0, 0);
            }
            
            // Show before/after comparison
            function showComparison() {
                comparisonBefore.src = originalImage.src;
                comparisonAfter.src = upscaledImage.src;
                comparisonContainer.style.display = 'block';
                
                // Initialize comparison slider
                let isResizing = false;
                
                function initSlider() {
                    const width = comparisonSlider.offsetWidth;
                    comparisonBefore.style.width = width + 'px';
                    comparisonAfter.style.width = width + 'px';
                    comparisonResize.style.left = (width / 2) + 'px';
                }
                
                initSlider();
                window.addEventListener('resize', initSlider);
                
                // Mouse events for slider
                comparisonResize.addEventListener('mousedown', function(e) {
                    isResizing = true;
                });
                
                document.addEventListener('mousemove', function(e) {
                    if (!isResizing) return;
                    
                    const sliderRect = comparisonSlider.getBoundingClientRect();
                    const x = e.clientX - sliderRect.left;
                    
                    if (x < 50) return;
                    if (x > sliderRect.width - 50) return;
                    
                    comparisonResize.style.left = x + 'px';
                    comparisonBefore.style.width = x + 'px';
                });
                
                document.addEventListener('mouseup', function(e) {
                    isResizing = false;
                });
                
                // Setup download button
                downloadBtn.href = upscaledImage.src;
                downloadBtn.download = 'upscaled-image.jpg';
            }
        });
    </script>
</body>
</html>
