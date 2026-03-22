<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Radio Estasi - La radio del futuro</title>
    <style>
        /* TAVOLOZZA COLORI E STILE */
        :root {
            --bg: #000000;
            --accent: #FFD700; /* Giallo Estasi */
            --text: #ffffff;
            --text-dim: #bbbbbb;
        }

        body, html { 
            margin: 0; padding: 0; min-height: 100vh; 
            background-color: var(--bg); 
            color: var(--text); 
            font-family: Arial, Helvetica, sans-serif; 
        }

        .wrapper { display: flex; flex-direction: column; min-height: 100vh; }

        /* HEADER E PLAYER */
        header {
            background: #111;
            padding: 20px 10px;
            text-align: center;
            border-bottom: 3px solid var(--accent);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .logo h1 { margin: 0; color: var(--accent); letter-spacing: 3px; font-size: 2.2rem; }
        .logo p { margin: 5px 0; font-size: 0.9rem; text-transform: uppercase; color: var(--text-dim); }

        nav { margin: 15px 0; display: flex; flex-wrap: wrap; justify-content: center; gap: 15px; }
        nav a {
            color: var(--text);
            text-decoration: none;
            font-weight: bold;
            font-size: 0.85rem;
            text-transform: uppercase;
            cursor: pointer;
            transition: 0.3s;
        }
        nav a:hover { color: var(--accent); }

        .player-container { margin-top: 15px; background: #222; padding: 10px; border-radius: 50px; display: inline-block; }
        audio { height: 35px; width: 280px; filter: invert(1) hue-rotate(180deg) brightness(1.5); }

        /* AREA CONTENUTO */
        main {
            flex: 1;
            padding: 40px 20px;
            max-width: 900px;
            margin: 0 auto;
            width: 100%;
            box-sizing: border-box;
        }

        /* FOOTER */
        footer {
            background: #111;
            padding: 40px 20px;
            border-top: 1px solid #222;
            text-align: center;
        }

        .footer-links { margin-bottom: 20px; line-height: 2; }
        .footer-links a { 
            color: var(--text-dim); text-decoration: none; margin: 0 10px; font-size: 0.85rem; cursor: pointer;
        }
        .footer-links a:hover { color: var(--accent); }

        /* ANIMAZIONI E BOTTONI */
        .btn-giallo {
            background: var(--accent); color: #000; border: none; padding: 10px 20px;
            font-weight: bold; cursor: pointer; text-decoration: none; border-radius: 4px; display: inline-block;
        }
        
        .fade { animation: fadeIn 0.4s ease-in; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

<div class="wrapper">
    <header>
        <div class="logo">
            <h1>RADIO ESTASI</h1>
            <p>La radio del futuro</p>
        </div>
        
        <nav>
            <a onclick="loadPage('programmi')">Programmi</a>
            <a onclick="loadPage('repliche')">Repliche</a>
            <a onclick="loadPage('palinsesto')">Palinsesto</a>
            <a onclick="loadPage('radio')">La Radio</a>
            <a onclick="loadPage('eventi')">Eventi</a>
            <a onclick="loadPage('news')">News</a>
            <a onclick="loadPage('team')">Team</a>
        </nav>

        <div class="player-container">
            <audio id="main-player" controls>
                <source src="https://stream.zeno.fm/qvdruxs5fqvvv" type="audio/mpeg">
            </audio>
        </div>
    </header>

    <main id="content-area">
        </main>

    <footer>
        <div class="footer-links">
            <a onclick="loadPage('archivio')">Archivio Opere</a>
            <a onclick="loadPage('contatti')">Contattaci</a>
            <a href="https://tuo-link-lavora-con-noi" target="_blank">Lavora con noi</a>
            <a href="https://tuo-link-partecipa" target="_blank">Partecipa alla diretta</a>
            <a onclick="loadPage('privacy')">Privacy Policy</a>
        </div>
        <p style="font-size: 0.7rem; color: #555;">&copy; 2026 RADIO ESTASI. La Radio del Futuro.</p>
    </footer>
</div>

<script>
    /* --- DATABASE DEI CONTENUTI --- */
    const dynamicPages = {
        radio: `
            <h2 style="color: var(--accent);">LA RADIO</h2>
            <p>Radio Estasi è il punto di riferimento per chi cerca il suono di domani. Trasmettiamo h24 innovazione, creatività e vibrazioni dal futuro.</p>
            <p>Sintonizzati e lasciati trasportare.</p>
        `,
        programmi: `
            <h2 style="color: var(--accent);">PROGRAMMI</h2>
            <div style="background:#111; padding:15px; border-left:4px solid var(--accent); margin-bottom:15px;">
                <h3>Neon Nights</h3><p>Il meglio della synthwave ogni sera alle 22:00.</p>
            </div>
            <div style="background:#111; padding:15px; border-left:4px solid var(--accent);">
                <h3>Future Talk</h3><p>Interviste con i protagonisti del domani.</p>
            </div>
        `,
        repliche: `
            <h2 style="color: var(--accent);">REPLICHE</h2>
            <p>Non hai potuto seguire la diretta? Presto qui troverai l'archivio completo dei nostri podcast.</p>
        `,
        palinsesto: `
            <h2 style="color: var(--accent);">PALINSESTO</h2>
            <p>Le nostre trasmissioni seguono il ritmo del futuro. Consulta qui gli orari settimanali aggiornati.</p>
        `,
        eventi: `
            <h2 style="color: var(--accent);">EVENTI</h2>
            <p>Radio Estasi esce dagli schermi. Seguici nei nostri eventi live esclusivi.</p>
        `,
        news: `
            <h2 style="color: var(--accent);">NEWS</h2>
            <article>
                <h3>Radio Estasi attiva il nuovo stream</h3>
                <p>Migliorata la qualità audio per un'esperienza ancora più immersiva.</p>
            </article>
        `,
        team: `
            <h2 style="color: var(--accent);">IL TEAM</h2>
            <p>Voci, DJ e sognatori che rendono Radio Estasi realtà ogni giorno.</p>
        `,
        archivio: `<h2>ARCHIVIO OPERE</h2><p>L'eredità sonora di Radio Estasi.</p>`,
        contatti: `
            <h2 style="color: var(--accent);">CONTATTACI</h2>
            <p>Email: <strong>info@radioestasi.it</strong></p>
            <p>Seguici sui social per restare aggiornato.</p>
        `,
        privacy: `<h2>PRIVACY POLICY</h2><p>Informativa sul trattamento dei dati personali.</p>`
    };

    /* --- MOTORE DI NAVIGAZIONE --- */
    function loadPage(pageKey) {
        const contentArea = document.getElementById('content-area');
        
        // Effetto di caricamento
        if (dynamicPages[pageKey]) {
            contentArea.innerHTML = '<div class="fade">' + dynamicPages[pageKey] + '</div>';
        } else {
            contentArea.innerHTML = '<div class="fade"><h2>404</h2><p>Pagina non trovata.</p></div>';
        }
        
        // Riporta la pagina in alto ad ogni cambio
        window.scrollTo(0, 0);
    }

    // Carica la pagina "Radio" all'avvio del sito
    window.onload = () => loadPage('radio');
</script>

</body>
</html>
