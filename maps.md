# 🗺️ Mapa Tático de QTHs — GSA

Utilize o mapa interativo abaixo para localizar os principais pontos estratégicos e coordenadas da cidade.

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<div id="gta-map" style="width: 100%; height: 650px; background: #0b0e14; border: 1px solid #232b3c; border-radius: 8px;"></div>

<script>
  // Inicializa o mapa com um sistema de coordenadas plano (para mapas de jogos)
  var map = L.map('gta-map', {
    crs: L.CRS.Simple,
    minZoom: -3,
    maxZoom: 2,
    colors: '#fff'
  });

  // Dimensões da imagem do mapa (ajusta a escala do plano)
  var bounds = [[0, 0], [4000, 4000]];
  
  // Link de uma imagem de alta qualidade do mapa do GTA V (Estilo Satélite/Atlas)
  var imageURL = 'https://i.imgur.com/v8tT9Z1.jpg'; 
  
  L.imageOverlay(imageURL, bounds).addTo(map);
  map.fitBounds(bounds);

  // === CONFIGURAÇÃO DOS ÍCONES PARA OS QTHs ===
  var iconePolicia = L.icon({
    iconUrl: 'https://cdn-icons-png.flaticon.com/512/3063/3063166.png', // Ícone de distintivo/polícia
    iconSize: [32, 32],
    iconAnchor: [16, 32],
    popupAnchor: [0, -32]
  });

  var iconePerigo = L.icon({
    iconUrl: 'https://cdn-icons-png.flaticon.com/512/564/564619.png', // Ícone de alerta/perigo
    iconSize: [32, 32],
    iconAnchor: [16, 32],
    popupAnchor: [0, -32]
  });

  // === ADICIONANDO OS PRINCIPAIS QTHs ===
  // Sintaxe: L.marker([Y, X], {icon: nomeDoIcone}).addTo(map).bindPopup('Texto que aparece ao clicar');
  
  // Exemplo 1: QTH Batalhão Principal (Região Central do Mapa)
  L.marker([1800, 2100], {icon: iconePolicia})
    .addTo(map)
    .bindPopup('<b>📌 QTH: 1º BPM Hardline</b><br>Base Principal de Operações e Linha de Voo GSA.');

  // Exemplo 2: QTH Ponto de Atenção / Rota de Fuga Comum
  L.marker([2500, 1500], {icon: iconePerigo})
    .addTo(map)
    .bindPopup('<b>⚠️ QTH: Área de Risco / Boosting</b><br>Local com alto índice de confrontos e início de fuga.');

  // === FUNÇÃO AUXILIAR PARA VOCÊ PEGAR AS COORDENADAS ===
  // Ao clicar em qualquer lugar do mapa, ele avisa a coordenada no console do navegador (F12) 
  // Assim fica fácil para você descobrir onde colocar os novos marcadores!
  map.on('click', function(e) {
    console.log("Coordenadas clicadas: [" + e.latlng.lat.toFixed(0) + ", " + e.latlng.lng.toFixed(0) + "]");
  });
</script>
