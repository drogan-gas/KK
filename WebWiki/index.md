<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>🏭設備安裝工程管理系統</title>
    <style>
        html, body {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            background-color: #f8fafc;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
        }
        iframe {
            width: 100%;
            height: 100%;
            border: none;
            display: block;
        }
    </style>
</head>
<body>
    <iframe id="gasFrame" src="about:blank" allow="camera; microphone; geolocation"></iframe>

    <script>
        (function() {
            const gasBaseUrl = "https://script.google.com/macros/s/AKfycbwOJUVdnJtiBwPVecqhn9NOZnFaI2AfoOnNf-yrPL38zlBtvIlYL65ffHqMEwTUFnBd/exec";
            
            // 取得目前的網址參數與當前網頁 base URL，並合併穿透至 iframe
            const parentUrl = window.location.protocol + "//" + window.location.host + window.location.pathname;
            const searchParams = new URLSearchParams(window.location.search);
            searchParams.set('parentUrl', parentUrl);
            
            const iframeUrl = gasBaseUrl + "?" + searchParams.toString();
            document.getElementById('gasFrame').src = iframeUrl;
        })();
    </script>
</body>
</html>