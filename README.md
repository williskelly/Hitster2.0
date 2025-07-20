<!doctype html>
<html lang="fr">
<head>
  <meta charset="utf-8" />
  <title>Lecture rapide Spotify</title>
  <style>
    body{display:flex;justify-content:center;align-items:center;height:100vh;font-family:sans-serif}
    #info{text-align:center}
  </style>
</head>
<body>
  <div id="info">
    <h1 id="title">Chargement…</h1>
    <audio id="player" controls></audio>
  </div>

<script>
(async () => {
  const id = new URLSearchParams(location.search).get('id');
  if (!id) { document.getElementById('title').textContent = 'ID manquant'; return; }

  const r = await fetch(`https://spotifycharts-embed-backend.vercel.app/track/${id}`);
  const t = await r.json();
  document.getElementById('title').textContent = `${t.name} – ${t.artists.join(', ')}`;

  const player = document.getElementById('player');
  player.src = t.preview_url;
  player.play().catch(()=>{});
})();
</script>
</body>
</html>
