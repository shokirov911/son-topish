<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Sonni top!</title>
<style>
  /* Ranglarni shu yerdan o'zgartiring */
  :root {
    --fon1: #1e1b4b;
    --fon2: #4338ca;
    --asosiy: #6366f1;
    --katta: #ea580c;
    --kichik: #2563eb;
    --togri: #16a34a;
  }
  * { box-sizing: border-box; }
  body {
    margin: 0; min-height: 100vh; padding: 16px;
    display: flex; align-items: center; justify-content: center;
    font-family: system-ui, Arial, sans-serif;
    background: linear-gradient(135deg, var(--fon1), var(--fon2));
  }
  .karta {
    width: 100%; max-width: 380px; padding: 28px;
    background: #fff; color: #1f2937; text-align: center;
    border-radius: 20px; box-shadow: 0 20px 50px rgba(0, 0, 0, .35);
  }
  h1 { margin: 0 0 6px; font-size: 28px; }
  p { margin: 0 0 18px; color: #6b7280; }
  input {
    width: 100%; padding: 12px; font-size: 24px; text-align: center;
    border: 2px solid #e5e7eb; border-radius: 12px; outline: none;
  }
  input:focus { border-color: var(--asosiy); }
  button {
    width: 100%; margin-top: 12px; padding: 14px; font-size: 18px;
    color: #fff; background: var(--asosiy);
    border: 0; border-radius: 12px; cursor: pointer;
  }
  button:hover { filter: brightness(1.1); }
  #xabar { min-height: 32px; margin-top: 16px; font-size: 18px; font-weight: 600; }
  .katta { color: var(--katta); }
  .kichik { color: var(--kichik); }
  .togri { color: var(--togri); }
  #tarix { margin-top: 8px; font-size: 14px; color: #6b7280; }
</style>
</head>
<body>
  <div class="karta">
    <h1>🎯 Sonni top!</h1>
    <p>Men 1 dan 100 gacha son o'yladim.</p>
    <input id="son" type="number" min="1" max="100" placeholder="?">
    <button id="tugma">Tekshirish</button>
    <div id="xabar"></div>
    <div id="tarix"></div>
  </div>

<script>
  const son = document.getElementById("son");
  const tugma = document.getElementById("tugma");
  const xabar = document.getElementById("xabar");
  const tarix = document.getElementById("tarix");

  let sir, urinishlar, tugadi;

  function yangiOyin() {
    sir = Math.floor(Math.random() * 100) + 1;   // 1 dan 100 gacha tasodifiy son
    urinishlar = [];
    tugadi = false;
    xabar.textContent = "";
    tarix.textContent = "";
    son.value = "";
    son.disabled = false;
    tugma.textContent = "Tekshirish";
    son.focus();
  }

  function yoz(matn, sinf) {
    xabar.textContent = matn;
    xabar.className = sinf;
  }

  function tekshir() {
    if (tugadi) { yangiOyin(); return; }

    const taxmin = Number(son.value);
    if (!Number.isInteger(taxmin) || taxmin < 1 || taxmin > 100) {
      yoz("1 dan 100 gacha son kiriting.", "");
      return;
    }

    urinishlar.push(taxmin);
    tarix.textContent = "Urinishlar: " + urinishlar.join(", ");
    son.value = "";
    son.focus();

    if (taxmin < sir) {
      yoz("⬆ Men o'ylagan son KATTAROQ", "katta");
    } else if (taxmin > sir) {
      yoz("⬇ Men o'ylagan son KICHIKROQ", "kichik");
    } else {
      yoz("🎉 To'g'ri! " + urinishlar.length + " ta urinishda topdingiz.", "togri");
      tugadi = true;
      son.disabled = true;
      tugma.textContent = "Yangi o'yin";
    }
  }

  tugma.addEventListener("click", tekshir);
  son.addEventListener("keydown", function (e) {
    if (e.key === "Enter") tekshir();
  });

  yangiOyin();
</script>
</body>
</html># son-topish
