index.html
Aplicación para viajes en bici taxi 
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bici-Taxi App</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
          integrity="sha256-p4NxAoJBhIINfL1L-5i+pTIS8NAyL9eE2UqLY7Tl8T8="
          crossorigin=""/>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <header>
        <h1>Bici-Taxi</h1>
        <nav>
            <button id="btn-cliente">Soy cliente</button>
            <button id="btn-conductor">Soy conductor</button>
        </nav>
    </header>

    <main id="app-container">
        </main>

    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"
            integrity="sha256-20nEFjYyKq7W8pA11F686R1Q+vR9jS+G7b8l2D+c9Q="
            crossorigin=""></script>
    <script src="script.js"></script>
</body>
</html>
body {
    font-family: sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f4f4f4;
}

header {
    background-color: #333;
    color: white;
    padding: 1rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

h1 {
    margin: 0;
}

nav button {
    background-color: #555;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    cursor: pointer;
    border-radius: 5px;
    margin-left: 10px;
}

#app-container {
    padding: 1rem;
    text-align: center;
}

.cliente-view, .conductor-view {
    padding: 2rem;
    background-color: white;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

.hidden {
    display: none;
}

#mapa {
    height: 400px; /* Tamaño del mapa */
    width: 100%;
    margin-top: 1rem;
    border-radius: 8px;
}
// Obtenemos los elementos del DOM
const appContainer = document.getElementById('app-container');
const btnCliente = document.getElementById('btn-cliente');
const btnConductor = document.getElementById('btn-conductor');

// Vistas de la aplicación
const clienteView = `
    <div class="cliente-view">
        <h2>Pide tu Bici-Taxi</h2>
        <div id="mapa"></div> <button>Solicitar Bici-Taxi</button>
    </div>
`;

const conductorView = `
    <div class="conductor-view">
        <h2>Panel del Conductor</h2>
        <div id="mapa"></div> <div id="solicitudes">
            <p>No hay solicitudes pendientes.</p>
        </div>
    </div>
`;

// Función para renderizar la vista del cliente e inicializar el mapa
function renderizarCliente() {
    appContainer.innerHTML = clienteView;
    inicializarMapa();
}

// Función para renderizar la vista del conductor e inicializar el mapa
function renderizarConductor() {
    appContainer.innerHTML = conductorView;
    inicializarMapa();
}

// Nueva función para inicializar el mapa con Leaflet
function inicializarMapa() {
    // Coordenadas aproximadas para La Habana, Cuba
    const latitud = 23.13302;
    const longitud = -82.38304;
    const zoomInicial = 10;

    // Crea el mapa y lo centra en las coordenadas
    const mapa = L.map('mapa').setView([latitud, longitud], zoomInicial);

    // Agrega una capa de mapa base de OpenStreetMap
    L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19,
        attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
    }).addTo(mapa);
}

// Event Listeners para los botones de navegación
btnCliente.addEventListener('click', renderizarCliente);
btnConductor.addEventListener('click', renderizarConductor);

// Renderizar la vista del cliente por defecto al cargar la página
window.addEventListener('load', renderizarCliente);
