# All Servers
Server stats and join-able links/ip-addresses

---

<div id="all-servers"></div>

<script>
async function loadAllServers() {
  const container = document.getElementById("all-servers");
  container.innerHTML = "";

  try {
    const res = await fetch("https://gameservers.chestnutsprogramming.com/ptero/servers");
    const allServers = await res.json();

    for (const [gameName, servers] of Object.entries(allServers)) {

      // Create section
      const section = document.createElement("section");
      section.style.marginBottom = "2rem";          // space between games
      section.style.padding = "1rem";
      section.style.border = "1px solid var(--border)";
      section.style.borderRadius = "12px";
      section.style.background = "var(--card)";
      section.innerHTML = `<h2>${gameName}</h2><div class="game-grid"></div>`;
      const grid = section.querySelector(".game-grid");

      // Fetch background image
      let bgImage = "default.png";
      try {
        const imgRes = await fetch(`https://gameservers.chestnutsprogramming.com/images/${encodeURIComponent(gameName)}`);
        const imgData = await imgRes.json();
        bgImage = imgData["image-assets"];
      } catch (err) {
        console.warn(`Failed to load image for ${gameName}:`, err);
      }

      // Create cards
      grid.innerHTML = servers.map(s => `
      <div class="game-card" data-url="${s["ip"]}:${s["port"]}">
        <img src="/assets/${bgImage}" alt="${s.title}">
        <span class="dark">
          <h4>${s.title}</h4><br>
          Game: ${s.game}<br>
          Port: ${s.port}<br>
          Status: ${s.state}<br>
          <button class="copy-btn">Copy URL</button>
        </span>
      </div>
      `).join('');

      // Copy button functionality
      grid.querySelectorAll(".copy-btn").forEach(btn => {
        btn.addEventListener("click", (e) => {
          const url = e.target.closest(".game-card").dataset.url;
          navigator.clipboard.writeText(url)
            .then(() => alert(`Copied: ${url}`))
            .catch(err => alert("Failed to copy URL: " + err));
        });
      });

      container.appendChild(section);
    }

  } catch (err) {
    container.innerHTML = `<p style="color:red;">Failed to load servers: ${err}</p>`;
  }
}

loadAllServers();
</script>


---

© JakeByte Survivors