<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Password Redirect</title>
  <style>
    :root{font-family:Inter,system-ui,Segoe UI,Roboto,"Helvetica Neue",Arial}
    body{display:flex;align-items:center;justify-content:center;min-height:100vh;margin:0;background:#f3f4f6}
    .card{background:#fff;padding:28px;border-radius:12px;box-shadow:0 8px 24px rgba(15,23,42,0.08);width:360px;max-width:92%}
    h1{margin:0 0 8px;font-size:18px}
    p.subtitle{margin:0 0 18px;color:#6b7280;font-size:13px}
    label{display:block;font-size:13px;margin-bottom:6px}
    input[type=password]{width:100%;padding:10px 12px;border:1px solid #e5e7eb;border-radius:8px;font-size:15px}
    .actions{margin-top:14px;display:flex;gap:8px}
    button{flex:1;padding:10px 12px;border-radius:8px;border:0;background:#111827;color:#fff;font-size:15px;cursor:pointer}
    button.secondary{background:transparent;color:#111827;border:1px solid #e5e7eb}
    .msg{margin-top:12px;font-size:13px;color:#ef4444;min-height:18px}
    .hint{margin-top:12px;font-size:12px;color:#374151}
    .small{font-size:12px;color:#6b7280}
  </style>
</head>
<body>
  <main class="card">
    <h1>DOKUMENTASI KBE XXVIII</h1>
    <p class="subtitle">Isi password untuk melanjutkan ke dokumentasi.</p>

    <label for="pw">Password</label>
    <input id="pw" type="password" placeholder="Masukkan password" autocomplete="off" />

    <div class="actions">
      <button id="submitBtn">Lanjut</button>
      <button id="clearBtn" class="secondary" type="button">Bersihkan</button>
    </div>

    <div class="msg" id="msg"></div>
    <div class="hint small">PDD KBE 2025.</div>
  </main>

  <script>
    (function(){
      // === KONFIGURASI ===
      // Ganti nilai `correctPassword` dengan password yang Anda inginkan.
      // Ganti `redirectUrl` dengan link tujuan yang akan dikunjungi setelah password benar.
      // Contoh: const redirectUrl = 'https://contoh.com';
      const correctPassword = 'terimakasih pdd';
      const redirectUrl = 'https://drive.google.com/drive/folders/15ZewBXH1WN2HnIcnKcj1AmA1tEEmJR-7?usp=sharing';
      // ====================

      const pwInput = document.getElementById('pw');
      const submitBtn = document.getElementById('submitBtn');
      const clearBtn = document.getElementById('clearBtn');
      const msg = document.getElementById('msg');

      function showMessage(text, isError=true){
        msg.textContent = text;
        msg.style.color = isError ? '#ef4444' : '#16a34a';
      }

      function attempt(){
        const v = pwInput.value || '';
        if(!v){
          showMessage('Silakan masukkan password.');
          return;
        }
        if(v === correctPassword){
          showMessage('Password benar. Mengalihkan…', false);
          // delay kecil supaya user melihat pesan, lalu redirect
          setTimeout(()=>{
            // Jika Anda ingin membuka di tab baru, ganti dengan window.open(redirectUrl, '_blank')
            window.location.href = redirectUrl;
          }, 300);
        } else {
          showMessage('Password salah. Coba lagi.');
        }
      }

      submitBtn.addEventListener('click', attempt);
      clearBtn.addEventListener('click', ()=>{ pwInput.value=''; msg.textContent=''; pwInput.focus(); });
      pwInput.addEventListener('keydown', (e)=>{ if(e.key === 'Enter') attempt(); });

    })();
  </script>
</body>
</html>
