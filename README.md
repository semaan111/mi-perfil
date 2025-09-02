<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Mi perfil — Juan José Semaan</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;700;900&family=Inter:wght@900&display=swap" rel="stylesheet">
  <style>
    :root{ --bg:#0f1216; --fg:#e7f5ef; --brand:#6affb9; --muted:#9aa7ad; --card:#171b21; }
    *{box-sizing:border-box} html,body{height:100%}
    body{ margin:0; font-family:"Poppins",system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif;
      background: radial-gradient(1200px 600px at 50% -10%, #1a2128, #0f1216) no-repeat var(--bg);
      color:var(--fg); display:flex; flex-direction:column; align-items:center; gap:24px;
    }
    header{padding:32px 16px 8px; text-align:center}
    header h1{margin:0; font-size:clamp(24px,4vw,36px); font-weight:900; letter-spacing:.5px}
    header p{margin:6px 0 0; color:var(--muted)}
    .actions{display:flex; gap:12px; align-items:center; justify-content:center; flex-wrap:wrap; margin-top:8px}
    .btn-audio{ font-family:"Poppins",sans-serif; font-weight:900; background:#222; color:#6affb9;
      padding:12px 22px; border:none; border-radius:100px; cursor:pointer; font-size:18px;
      text-transform:uppercase; letter-spacing:1px; transition:background .25s ease, transform .1s ease;
    }
    .btn-audio:hover{background:#333} .btn-audio:active{background:#111; transform:translateY(1px)}
    .card{ width:min(900px,92vw); background:var(--card); border:1px solid #232a33; border-radius:16px; padding:18px; box-shadow:0 10px 30px rgba(0,0,0,.25); }
    .card h2{margin:0 0 12px; font-size:18px; font-weight:700}
    ul.files{list-style:none; padding:0; margin:0; display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:10px}
    ul.files li{background:#12161b; border:1px solid #202731; border-radius:12px; padding:10px; min-height:56px; display:flex; gap:10px; align-items:center}
    ul.files a{color:var(--fg); text-decoration:none; word-break:break-word}
    ul.files small{color:var(--muted); display:block; margin-top:4px}
    .chip{font-size:12px; padding:2px 8px; border:1px solid #2a3340; border-radius:999px; color:var(--muted)}
    footer{width:100%; text-align:center; padding:22px 12px; color:var(--muted); font-weight:900}
  </style>
</head>
<body>
  <header>
    <h1>Juan José Semaan / Product Designer</h1>
    <p>Portafolio ligero + archivos públicos</p>
    <div class="actions">
      <button id="btnPlay" class="btn-audio">▶️ Reproducir</button>
      <span id="audioHint" class="chip">Sube un .mp3 a <code>/assets</code></span>
    </div>
  </header>

  <main class="card">
    <h2>Archivos en <code>/assets</code></h2>
    <ul id="fileList" class="files"><li>Cargando lista…</li></ul>
  </main>

  <footer><p style="font-weight:900">Juan José Semaan / Product Designer</p></footer>

  <audio id="player" preload="none"></audio>
  <script>
    const OWNER="semaan111", REPO="mi-perfil", BRANCH="main", DIR="assets";
    const apiURL=`https://api.github.com/repos/${OWNER}/${REPO}/contents/${DIR}?ref=${BRANCH}`;
    const fileList=document.getElementById("fileList");
    const player=document.getElementById("player");
    const btnPlay=document.getElementById("btnPlay");
    const hint=document.getElementById("audioHint");

    async function loadFiles(){
      try{
        const res=await fetch(apiURL,{headers:{Accept:"application/vnd.github+json"}});
        if(!res.ok) throw new Error("¿Existe la carpeta /assets?");
        const data=await res.json();
        fileList.innerHTML="";
        const audios=[], others=[];
        for(const item of data){ if(item.type!=="file") continue;
          (/\.(mp3|wav|ogg)$/i.test(item.name)?audios:others).push(item);
        }
        const list=[...audios,...others];
        if(!list.length){ fileList.innerHTML=`<li>No hay archivos aún. Sube archivos a <em>/assets</em>.</li>`; }
        else{
          for(const f of list){
            const ext=(f.name.split(".").pop()||"").toUpperCase();
            const li=document.createElement("li");
            li.innerHTML=`<div><a href="${f.download_url}" target="_blank" rel="noopener">${f.name}</a><small>${ext} · ${(f.size/1024).toFixed(1)} KB</small></div>`;
            fileList.appendChild(li);
          }
        }
        if(audios.length){ player.src=audios[0].download_url; hint.textContent=`Reproduciendo: ${audios[0].name}`; }
        else{ player.removeAttribute("src"); hint.textContent="Sube un .mp3 a /assets"; }
      }catch(e){ fileList.innerHTML=`<li>Error al listar /assets. ${e.message}</li>`; }
    }
    btnPlay.addEventListener("click",async ()=>{
      if(!player.src){ alert("Aún no hay audio. Sube un .mp3 a /assets."); return; }
      if(player.paused){ await player.play(); btnPlay.textContent="⏸️ Pausar"; }
      else{ player.pause(); btnPlay.textContent="▶️ Reproducir"; }
    });
    loadFiles();
  </script>
</body>
</html>
