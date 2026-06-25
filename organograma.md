<div id="app-organograma">Carregando dados da cadeia de comando...</div>

<script>
(async () => {
  const url = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vSw-LdIv-3xH3eswHp06gAaxJI8e9aJcrfyuBPPhBIyc6lwHww33rXMhYei5JzTfDxAc96w2kBZ2DWb/pub?output=csv';
  
  try {
    const res = await fetch(url);
    const data = await res.text();
    const rows = data.split('\n').slice(1);
    
    let html = `
      <style>
        .container { font-family: sans-serif; color: white; }
        .grid-topo { display: flex; justify-content: center; gap: 10px; margin-bottom: 20px; }
        .card-topo { background: #1a252f; border: 1px solid #f1c40f; padding: 10px; border-radius: 5px; text-align: center; width: 200px; }
        .grid-baixo { display: flex; gap: 20px; justify-content: center; }
        .coluna { background: #0b0e14; border: 1px solid #34495e; padding: 15px; width: 300px; }
        .item { padding: 5px; border-bottom: 1px solid #2c3e50; font-size: 0.9em; }
      </style>
      <div class="container">
        <div id="topo" class="grid-topo"></div>
        <div class="grid-baixo">
          <div class="coluna"><h3>PILOTOS</h3><div id="pilotos"></div></div>
          <div class="coluna"><h3>OPERADORES</h3><div id="operadores"></div></div>
        </div>
      </div>
    `;

    document.getElementById('app-organograma').innerHTML = html;

    rows.forEach(row => {
      const [id, nome, badge, patente] = row.split(',');
      if(!nome) return;
      const p = patente.trim();

      if (['Alto Comando', 'Comando', 'Sub-Comando'].includes(p)) {
        document.getElementById('topo').innerHTML += `<div class="card-topo"><b>${p}</b><br>${nome}</div>`;
      } else if (p.toLowerCase().includes('piloto')) {
        document.getElementById('pilotos').innerHTML += `<div class="item">${p} - ${nome}</div>`;
      } else {
        document.getElementById('operadores').innerHTML += `<div class="item">${p} - ${nome}</div>`;
      }
    });
  } catch (e) {
    document.getElementById('app-organograma').innerHTML = "Erro ao carregar dados. Verifique se a planilha está publicada.";
  }
})();
</script>
