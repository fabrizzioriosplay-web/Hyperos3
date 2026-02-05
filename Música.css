<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hype Music Player - Dynamic Island</title>
    <style>
        /* --- ESTILOS (CSS) --- */
        body {
            background-color: #000;
            color: white;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            margin: 0;
            height: 100vh;
        }

        /* Isla Dinámica */
        #dynamic-island {
            width: 120px;
            height: 35px;
            background: #000;
            border-radius: 20px;
            margin-top: 20px;
            transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            border: 1px solid #333;
            box-shadow: 0px 4px 15px rgba(255, 255, 255, 0.1);
            overflow: hidden;
            position: fixed;
            z-index: 1000;
        }

        #dynamic-island.active {
            width: 320px;
            height: 80px;
            background: #1a1a1a;
        }

        .island-content {
            font-size: 12px;
            text-align: center;
            padding: 10px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        /* Contenedor Principal */
        .main-container {
            margin-top: 150px;
            text-align: center;
            width: 90%;
            max-width: 400px;
        }

        .btn-import {
            background-color: #1DB954;
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 30px;
            font-weight: bold;
            cursor: pointer;
            font-size: 16px;
            transition: 0.3s;
        }

        .btn-import:hover {
            transform: scale(1.05);
            background-color: #1ed760;
        }

        #playlist {
            margin-top: 30px;
            text-align: left;
        }

        .track-item {
            background: #111;
            padding: 10px;
            margin: 5px 0;
            border-radius: 8px;
            cursor: pointer;
            border-left: 4px solid transparent;
        }

        .track-item:hover { background: #222; }
        .track-item.playing { border-left: 4px solid #1DB954; color: #1DB954; }

    </style>
</head>
<body>

    <div id="dynamic-island" onclick="handleIslandClick(event)" ondblclick="handleIslandDblClick()">
        <div class="island-content" id="island-text">Silencio</div>
    </div>

    <div class="main-container">
        <h1>Music App</h1>
        <p>Canciones actuales: 4K, Vicky, Hoy me voy al sol</p>
        
        <input type="file" id="file-input" accept="audio/*" multiple style="display: none;">
        <button class="btn-import" onclick="document.getElementById('file-input').click()">
            + Importar mi música
        </button>

        <div id="playlist">
            </div>
    </div>

    <audio id="player"></audio>

    <script>
        /* --- LÓGICA (JavaScript) --- */
        const player = document.getElementById('player');
        const island = document.getElementById('dynamic-island');
        const islandText = document.getElementById('island-text');
        const fileInput = document.getElementById('file-input');
        const playlistContainer = document.getElementById('playlist');

        let tracks = [];
        let currentIndex = -1;

        // Función para cargar canciones importadas
        fileInput.addEventListener('change', (e) => {
            const files = Array.from(e.target.files);
            files.forEach(file => {
                const track = {
                    name: file.name.replace(/\.[^/.]+$/, ""), // Quitar extensión
                    url: URL.createObjectURL(file)
                };
                tracks.push(track);
            });
            renderPlaylist();
        });

        function renderPlaylist() {
            playlistContainer.innerHTML = "";
            tracks.forEach((track, index) => {
                const div = document.createElement('div');
                div.className = `track-item ${index === currentIndex ? 'playing' : ''}`;
                div.innerText = track.name;
                div.onclick = () => playTrack(index);
                playlistContainer.appendChild(div);
            });
        }

        function playTrack(index) {
            if (index < 0 || index >= tracks.length) return;
            
            currentIndex = index;
            player.src = tracks[index].url;
            player.play();
            
            island.classList.add('active');
            islandText.innerHTML = `<b>Reproduciendo:</b><br>${tracks[index].name}`;
            renderPlaylist();
        }

        // Manejo de clicks en la Isla Dinámica
        function handleIslandClick(e) {
            // Evitar que el click simple interfiera con el doble click
            if (e.detail === 1) {
                setTimeout(() => {
                    if (e.detail === 1) {
                        if (player.paused) {
                            player.play();
                            islandText.style.opacity = "1";
                        } else {
                            player.pause();
                            islandText.style.opacity = "0.5";
                        }
                    }
                }, 200);
            }
        }

        // Doble click: Canción anterior
        function handleIslandDblClick() {
            if (currentIndex > 0) {
                playTrack(currentIndex - 1);
            } else {
                // Si es la primera, reiniciar la canción
                player.currentTime = 0;
                player.play();
            }
        }

        // Al terminar una canción, pasar a la siguiente
        player.onended = () => {
            if (currentIndex < tracks.length - 1) {
                playTrack(currentIndex + 1);
            }
        };

    </script>
</body>
</html>
