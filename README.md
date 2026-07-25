<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nexus Forex AI - Next Candle Predictor</title>
    <style>
        :root {
            --bg-color: #07090e;
            --card-bg: #101622;
            --accent-glow: #00f2fe;
            --accent-green: #00ff87;
            --text-main: #f0f3f9;
            --text-muted: #b0c4de;
            --border: #1e293b;
        }
        body {
            font-family: 'Segoe UI', Tahoma, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 15px 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            box-sizing: border-box;
            background-image: radial-gradient(circle at 50% 0%, #111e38 0%, var(--bg-color) 70%);
        }
        .container {
            background: var(--card-bg);
            border: 1px solid var(--border);
            padding: 22px;
            border-radius: 20px;
            width: 100%;
            max-width: 440px;
            box-sizing: border-box;
            display: flex;
            flex-direction: column;
            gap: 18px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.6);
        }
        .header {
            text-align: center;
        }
        .header h2 {
            margin: 0;
            font-size: 22px;
            color: #fff;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        .header p {
            color: var(--accent-glow);
            font-size: 12px;
            margin: 5px 0 0 0;
        }
        .api-group {
            background: rgba(15, 23, 42, 0.8);
            border: 1px solid var(--border);
            padding: 12px 14px;
            border-radius: 14px;
        }
        .api-group label {
            font-size: 14px;
            color: var(--accent-glow);
            display: block;
            margin-bottom: 6px;
            font-weight: 700;
        }
        .api-input-row {
            display: flex;
            gap: 10px;
        }
        .api-input {
            flex: 1;
            background: #07090e;
            border: 1px solid var(--border);
            color: var(--text-main);
            padding: 10px;
            border-radius: 10px;
            font-size: 14px;
        }
        .btn-save {
            background: var(--accent-green);
            color: #07090e;
            border: none;
            padding: 0 16px;
            border-radius: 10px;
            font-weight: 800;
            font-size: 13px;
            cursor: pointer;
        }
        .upload-group {
            display: flex;
            flex-direction: column;
            gap: 14px;
        }
        .upload-item {
            display: flex;
            align-items: center;
            background: rgba(15, 23, 42, 0.6);
            border: 1px solid var(--border);
            padding: 12px 16px;
            border-radius: 16px;
            gap: 14px;
        }
        .circle-icon {
            width: 48px;
            height: 48px;
            background: linear-gradient(135deg, #00f2fe, #2962ff);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            flex-shrink: 0;
        }
        .upload-details {
            flex-grow: 1;
        }
        .upload-details label {
            font-size: 14px;
            color: var(--text-main);
            display: block;
            margin-bottom: 5px;
            font-weight: 700;
        }
        input[type=file] {
            font-size: 12px;
            color: var(--text-muted);
            width: 100%;
        }
        .preview-img {
            width: 100%;
            max-height: 180px;
            object-fit: contain;
            border-radius: 12px;
            display: none;
            background: #000;
            border: 1px solid var(--border);
        }
        .btn-submit {
            background: linear-gradient(135deg, #00f2fe, #4facfe);
            color: #07090e;
            border: none;
            padding: 15px;
            border-radius: 14px;
            font-weight: 800;
            font-size: 15px;
            text-transform: uppercase;
            letter-spacing: 1px;
            cursor: pointer;
            text-align: center;
            box-shadow: 0 5px 20px rgba(0,242,254,0.3);
        }
        .result-card {
            background: var(--card-bg);
            border: 1px solid var(--border);
            padding: 20px;
            border-radius: 20px;
            width: 100%;
            max-width: 440px;
            box-sizing: border-box;
            margin-top: 18px;
            white-space: pre-wrap;
            font-size: 14px;
            line-height: 1.7;
            display: none;
            box-shadow: 0 15px 35px rgba(0,0,0,0.6);
        }
        .result-header {
            color: var(--accent-glow);
            font-weight: 800;
            margin-bottom: 10px;
            border-bottom: 1px solid var(--border);
            padding-bottom: 8px;
            text-transform: uppercase;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h2>⚡ Nexus Forex AI</h2>
            <p>Institutional Next Candle Predictor</p>
        </div>
        
        <div class="api-group">
            <label>🔑 Gemini API Key:</label>
            <div class="api-input-row">
                <input type="password" id="api_key_input" class="api-input" placeholder="এপিআই কি দিন">
                <button type="button" class="btn-save" onclick="saveApiKey()">Save</button>
            </div>
        </div>

        <div class="upload-group">
            <div class="upload-item">
                <div class="circle-icon">📁</div>
                <div class="upload-details">
                    <label>স্টোরেজ থেকে চার্ট আপলোড</label>
                    <input type="file" id="file_input" accept="image/*" onchange="previewFile(event)">
                </div>
            </div>

            <div class="upload-item">
                <div class="circle-icon">📸</div>
                <div class="upload-details">
                    <label>সরাসরি ক্যামেরা দিয়ে তুলুন</label>
                    <input type="file" id="camera_input" accept="image/*" capture="environment" onchange="previewFile(event)">
                </div>
            </div>
        </div>

        <img id="preview" class="preview-img">

        <button type="button" class="btn-submit" onclick="startAnalysis()">🚀 এনালাইসিস শুরু করুন</button>
    </div>

    <div id="result_card" class="result-card">
        <div class="result-header">📊 এআই মার্কেট সিগন্যাল ও ক্যান্ডেল বিশ্লেষণ:</div>
        <div id="result_content">ফলাফল এখানে আসবে...</div>
    </div>

    <script>
        let selectedFile = null;

        window.onload = function() {
            const savedKey = localStorage.getItem('nexus_gemini_api_key');
            if (savedKey) {
                document.getElementById('api_key_input').value = savedKey;
            }
        };

        function saveApiKey() {
            const key = document.getElementById('api_key_input').value;
            if (key.trim() !== "") {
                localStorage.setItem('nexus_gemini_api_key', key);
                alert('API Key সফলভাবে সেভ হয়েছে!');
            } else {
                alert('দয়া করে সঠিক এপিআই কি দিন।');
            }
        }

        function previewFile(event) {
            selectedFile = event.target.files[0];
            if (selectedFile) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const output = document.getElementById('preview');
                    output.src = e.target.result;
                    output.style.display = 'block';
                };
                reader.readAsDataURL(selectedFile);
            }
        }

        async function startAnalysis() {
            const apiKey = document.getElementById('api_key_input').value;
            if (!apiKey) {
                alert('দয়া করে আপনার জেমিনি এপিআই কি দিন।');
                return;
            }
            if (!selectedFile) {
                alert('দয়া করে একটি চার্ট ছবি সিলেক্ট করুন বা তুলুন।');
                return;
            }

            const resultCard = document.getElementById('result_card');
            const resultContent = document.getElementById('result_content');
            resultCard.style.display = 'block';
            resultContent.innerHTML = '⏳ এনালাইসিস চলছে, দয়া করে অপেক্ষা করুন...';

            try {
                const base64Data = await toBase64(selectedFile);
                const mimeType = selectedFile.type;

                const promptText = "You are an elite institutional Forex Technical Analyst and Price Action Master. Analyze this trading chart image with extreme precision. Provide a comprehensive breakdown in the following structured format:\n\n1. **Market Trend:** (Clearly state whether it is UPTREND or DOWNTREND)\n2. **Next Candle Prediction:** (Clearly state 🟢 GREEN CANDLE or 🔴 RED CANDLE)\n3. **Identified Candle Name & Pattern:** (Mention the exact name and details of the last candlestick pattern/formation, e.g., Hammer, Engulfing, Doji, Pin Bar, Marubozu, etc.)\n4. **Detailed Technical Reason:** (Provide a clear, concise technical explanation of why the next candle will be green or red based on the market structure and candles).";

                const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-3.5-flash:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{
                            parts: [
                                { text: promptText },
                                { inline_data: { mime_type: mimeType, data: base64Data } }
                            ]
                        }]
                    })
                });

                const data = await response.json();
                if (data.candidates && data.candidates[0].content && data.candidates[0].content.parts[0].text) {
                    resultContent.innerHTML = data.candidates[0].content.parts[0].text;
                } else if (data.error) {
                    resultContent.innerHTML = `⚠️ এরর: ${data.error.message}`;
                } else {
                    resultContent.innerHTML = '⚠️ ফলাফল পাওয়া যায়নি। সঠিক API Key দিয়ে আবার চেষ্টা করুন।';
                }
            } catch (err) {
                resultContent.innerHTML = `⚠️ সংযোগে সমস্যা হয়েছে: ${err.message}`;
            }
        }

        function toBase64(file) {
            return new Promise((resolve, reject) => {
                const reader = new FileReader();
                reader.readAsDataURL(file);
                reader.onload = () => resolve(reader.result.split(',')[1]);
                reader.onerror = error => reject(error);
            });
        }
    </script>
</body>
</html>