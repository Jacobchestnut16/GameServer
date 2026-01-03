# Rust Servers

Server stats and join-able links/ip-addresses

---

<div class="game-grid" id="cards"></div>

<script>
const GAME_NAME = "Rust";

async function loadGameCards() {
  const container = document.getElementById("cards");

  try {
    // Fetch server data
    const res = await fetch(`https://gameservers.chestnutsprogramming.com/ptero/servers/${GAME_NAME}`);
    const servers = await res.json();

    // Fetch background image
    const imgRes = await fetch(`https://gameservers.chestnutsprogramming.com/images/${GAME_NAME}`);
    const imgData = await imgRes.json();
    const bgImage = imgData["image-assets"];

    container.innerHTML = servers.map(s => `
      <div class="game-card" data-url="${s["ip"]}:${s["port"]}">
        <img src="/assets/${bgImage}" alt="${s.title}">
        <span class="dark">
          <h4>${s.title}</h4><br>
          Game: ${s.game}<br>
          Port: ${s.port}<br>
            <div style="display:flex; gap: 5px;">
            Status:  <div class="${
                        s.state === "running" 
                        ? "success" 
                        : (
                            s.state === "offline" 
                            ? "fail" 
                            : "warn")
                        }">${s.state}</div>
            </div>
          <button class="copy-btn">Copy URL</button>
        </span>
      </div>
    `).join('');

    // Add click handlers to copy buttons
    document.querySelectorAll(".copy-btn").forEach(btn => {
      btn.addEventListener("click", (e) => {
        const url = e.target.closest(".game-card").dataset.url;
        navigator.clipboard.writeText(url)
          .then(() => alert(`Copied: ${url}`))
          .catch(err => alert("Failed to copy URL: " + err));
      });
    });

  } catch (err) {
    container.innerHTML = `<p style="color:red;">Failed to load servers: ${err}</p>`;
  }
}

loadGameCards();
</script>

---

© JakeByte Survivors