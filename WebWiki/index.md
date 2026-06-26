<!-- 1. 提早與 Google 伺服器建立握手連線，最高可省下 100-300ms 建立連線的時間 -->
<link rel="preconnect" href="https://script.google.com">
<link rel="preconnect" href="https://script.google.com" crossorigin>

<style>
  /* 讓 iframe 容器具備 Minimal 質感的載入動畫 */
  .gas-container {
    position: relative;
    width: 100%;
    height: 85vh; /* 依工程管理畫面高度自行調整 */
    background: #252525;
    border: 1px solid #2e2e2e;
    border-radius: 8px;
    overflow: hidden;
  }

  .gas-container iframe {
    width: 100%;
    height: 100%;
    border: none;
    opacity: 0;
    transition: opacity 0.3s ease; /* 載入完成後優雅淡入 */
    position: relative;
    z-index: 2;
  }

  /* 仿 Minimal 質感的微光 Skeleton 載入特效 */
  .gas-loading {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: var(--md-accent-fg-color, #e69f43);
    font-size: 14px;
    z-index: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
  }

  .spinner {
    width: 30px;
    height: 30px;
    border: 3px solid #2e2e2e;
    border-top: 3px solid var(--md-accent-fg-color, #e69f43);
    border-radius: 50%;
    animation: spin 0.8s linear infinite;
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }
</style>

<div class="gas-container">
  <!-- 2. 改為直接在 DOM 樹生成前由 Script 寫入最精準的 src，避免 about:blank 的二次轉跳 -->
  <div class="gas-loading" id="gasLoading">
    <div class="spinner"></div>
    <span>系統載入中...</span>
  </div>
  
  <script>
    (function() {
        const gasBaseUrl = "https://script.google.com/macros/s/AKfycbwOJUVdnJtiBwPVecqhn9NOZnFaI2AfoOnNf-yrPL38zlBtvIlYL65ffHqMEwTUFnBd/exec";
        
        // 解析並穿透網址參數
        const parentUrl = window.location.protocol + "//" + window.location.host + window.location.pathname;
        const searchParams = new URLSearchParams(window.location.search);
        searchParams.set('parentUrl', parentUrl);
        const iframeUrl = gasBaseUrl + "?" + searchParams.toString();
        
        // 使用 document.write 可以在瀏覽器解析 HTML 到這裡時，直接把 src 塞進去，比等 DOMReady 更快發出請求
        document.write(`
          <iframe id="gasFrame" src="${iframeUrl}" allow="camera; microphone; geolocation" onload="onGasFrameLoad()"></iframe>
        `);
    })();

    // 當 GAS Web App 真正載入完成後，隱藏 Spinner 並優雅淡入畫面
    function onGasFrameLoad() {
        document.getElementById('gasLoading').style.display = 'none';
        document.getElementById('gasFrame').style.opacity = '1';
    }
  </script>
</div>