# JakeByte Survivors Servers

Gaymers Welcome

Join the [discord](https://discord.gg/zvE5SczzAc), and play along

## Private Server Games

<div class="game-grid" id="cards"></div>

<script>
async function loadGameCards() {
  const container = document.getElementById("cards");

  try {
    // Fetch server data
    const res = await fetch(`https://gameservers.chestnutsprogramming.com/ptero/games`);
    const servers = await res.json();
    const uniqueArr = [...new Set(servers)];

    uniqueArr.forEach(gameCardServe);

    async function gameCardServe(item, index) {

        const imgRes = await fetch(`https://gameservers.chestnutsprogramming.com/images/${item}`);
        const imgData = await imgRes.json();
        const bgImage = imgData["image-assets"];
        var link = `#/pages/${item}`;

        container.innerHTML += `
        <a class="game-card" href="${link}">
          <img src="assets/${bgImage}" alt="${item}">
          <span class="dark">${item}</span>
        </a>`
    }

  } catch (err) {
    container.innerHTML = `<p style="color:red;">Failed to load servers: ${err}</p>`;
  }
}

loadGameCards();
</script>

# Discord Plays

<div class="game-grid">

<a class="game-card">
  <img src="assets/cod-bo7.png" alt="Call of Duty Black Ops 7">
  <span class="dark">COD: Black Ops 7</span>
</a>

<a class="game-card">
  <img src="assets/cod-bo6.png" alt="Call of Duty Black Ops 6">
  <span class="dark">COD: Black Ops 6</span>
</a>

<a class="game-card" href="#/pages/rust">
  <img src="assets/rust.png" alt="Rust">
  <span class="dark">Rust</span>
</a>

<a class="game-card">
  <img src="assets/cod-coldwar.png" alt="Call of Duty Black Ops Cold War">
  <span class="dark">COD: Cold War</span>
</a>

<a class="game-card">
  <img src="assets/cod-mw3.png" alt="Call of Duty Modern Warfare III">
  <span class="dark">Modern Warfare III</span>
</a>

<a class="game-card" href="#/pages/minecraft">
  <img src="assets/minecraft.png" alt="Minecraft Java Edition">
  <span class="dark">Minecraft Java</span>
</a>

<a class="game-card">
  <img src="assets/peak.png" alt="Peak">
  <span class="dark">Peak</span>
</a>

<a class="game-card">
  <img src="assets/sons-of-the-forest.png" alt="Sons of the Forest">
  <span class="dark">Sons of the Forest</span>
</a>



</div>

---

© JakeByte Survivors
