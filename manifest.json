$('dl-svg').addEventListener('click', doSVG);
    $('dl-pdf').addEventListener('click', doPDF);
    $('btn-share').addEventListener('click', doShare);
    $('btn-copy').addEventListener('click', doCopy);
    $('btn-save').addEventListener('click', function () { saveHistory(false); });
    $('hist-clear').addEventListener('click', function () { writeHistory([]); renderHistory(); });
    $('scan-toggle').addEventListener('click', function () { scanning ? stopScanner() : startScanner(); });
    $('scan-file-btn').addEventListener('click', function () { $('scan-file').click(); });
    $('scan-file').addEventListener('change', function (e) { scanImage(e.target.files[0]); e.target.value = ''; });
    $('scan-copy').addEventListener('click', function () {
      var txt = $('scan-result-text').textContent;
      if (navigator.clipboard) navigator.clipboard.writeText(txt).then(function () { toast(t('toastCopied')); });
    });

    applyLang();
    switchTab('url');
    loadLib('qr').then(render).catch(function () {
      $('qr-holder').innerHTML = '<p class="text-xs text-rose-300 p-6 text-center max-w-[220px]">' + t('toastLib') + '</p>';
    });
  }
  if (document.readyState === 'loading') document.addEventListener('DOMContentLoaded', init); else init();

  /* ---------------- PWA ---------------- */
  var deferredPrompt = null, installBtn = $('install-btn');
  function hideInstall() { installBtn.classList.add('hid'); installBtn.classList.remove('flex'); }
  var isInstalled = (window.matchMedia && window.matchMedia('(display-mode: standalone)').matches) || window.navigator.standalone === true;
  if (isInstalled) hideInstall();
  window.addEventListener('beforeinstallprompt', function (e) { e.preventDefault(); deferredPrompt = e; });
  window.addEventListener('appinstalled', hideInstall);
  installBtn.addEventListener('click', function () {
    if (deferredPrompt) {
      deferredPrompt.prompt();
      deferredPrompt.userChoice.then(function (r) { deferredPrompt = null; if (r.outcome === 'accepted') hideInstall(); });
    } else {
      alert(t('installHelp'));
    }
  });
  if ('serviceWorker' in navigator) {
    window.addEventListener('load', function () { navigator.serviceWorker.register('./sw.js').catch(function () {}); });
  }
})();
</script>
</body>
</html>
