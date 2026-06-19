<style>
    .main-container { max-width: 1200px; margin: 0 auto; text-align: center; font-family: 'Segoe UI', sans-serif; }
    .titulo-principal { color: #f0a500 !important; margin-bottom: 20px; font-weight: bold; font-size: 2em; }
    
    .btn-cadastro { 
        display: inline-block !important; 
        background: #f0a500 !important; 
        color: #000000 !important; 
        padding: 12px 24px !important; 
        border-radius: 6px !important; 
        text-decoration: none !important; 
        font-weight: bold !important; 
        margin-bottom: 25px !important; 
        transition: 0.3s !important; 
    }
    .btn-cadastro:hover { background: #d48e00 !important; color: #000000 !important; }
    
    .table-container { 
        background: #141923 !important; 
        border-radius: 12px; 
        overflow-x: auto !important; 
        border: 1px solid #232b3c; 
        margin-top: 20px;
    }
    
    .tabela-membros { width: 100% !important; border-collapse: collapse !important; margin: 0 !important; display: table !important; }
    .tabela-membros th { background: #1c2434 !important; color: #f0a500 !important; padding: 12px !important; font-size: 0.85em !important; text-transform: uppercase; border: 1px solid #232b3c !important; }
    .tabela-membros td { padding: 12px !important; border: 1px solid #1a202c !important; text-align: center !important; color: #e2e8f0 !important; font-size: 0.95em; }
    
    .col-adv { background-color: rgba(240, 165, 0, 0.02); }
    .cat-row { background: #1c2434 !important; font-weight: bold !important; text-align: left !important; padding-left: 20px !important; color: #f0a500 !important; text-transform: uppercase; letter-spacing: 1px; }
    .tabela-membros tr:hover { background: #1a202c !important; }
    
    .check-marcado { color: #f0a500 !important; font-weight: bold; }
    .adv-marcado { color: #ff4d4d !important; font-weight: bold; }
    .check-vazio { color: #4a5568 !important; }
</style>

<div id="container-geral-membros">
    <div class="main-container">
        <h1 class="titulo-principal">1º BPM - HARDLINE</h1>
        <a href="https://script.google.com/macros/s/AKfycbwtJEC35f80OO07rPrQ8fuWDcHbqnEQIQyUh8iVRwP-WB-KfIVM_IICr-rweX2eX864/exec" target="_blank" class="btn-cadastro">+ Cadastrar Novo Membro</a>
        <div class="table-container">
            <table class="tabela-membros">
                <tbody>
                    <tr>
                        <td style="padding: 40px !important; color: #a0aec0;">Carregando dados sincronizados...</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</div>

<script>
  (function() {
    // Pequeno delay para garantir que o Docsify montou a página no navegador antes do script rodar
    setTimeout(() => {
        const baseUrl = "https://docs.google.com/spreadsheets/d/e/2PACX-1vSw-LdIv-3xH3eswHp06gAaxJI8e9aJcrfyuBPPhBIyc6lwHww33rXMhYei5JzTfDxAc96w2kBZ2DWb/pub?output=csv";
        const URL = baseUrl + "&_t=" + new Date().getTime();

        const containerGeral = document.getElementById("container-geral-membros");
        if (!containerGeral || typeof Papa === 'undefined') return;

        function limparTexto(str) {
            if (!str) return "";
            return str.toString().normalize("NFD").replace(/[\u0300-\u036f]/g, "").trim().toUpperCase();
        }

        Papa.parse(URL, {
            download: true,
            header: true,
            skipEmptyLines: true,
            complete: function(res) {
                // Mapeamento e tratamento das colunas vindas do Sheets
                let dadosLimpos = res.data.map(linha => {
                    let novaLinha = {};
                    for (let chave in linha) {
                        let chaveLimpa = chave.normalize("NFD").replace(/[\u0300-\u036f]/g, "").replace(/[^a-zA-Z0-9]/g, "").toUpperCase();
                        novaLinha[chaveLimpa] = linha[chave];
                    }
                    novaLinha.PATENTE_ORIGINAL = linha.Patente || linha.PATENTE || novaLinha.PATENTE || "-";
                    novaLinha.NOME_ORIGINAL = linha.Nome || linha.NOME || novaLinha.NOME || "-";
                    return novaLinha;
                });

                // Filtra apenas quem tem ID preenchido
                let membros = dadosLimpos.filter(m => m.ID && m.ID.toString().trim() !== "");

                // Definição dos blocos exatos de exibição
                const blocosociais = [
                    { nome: "ALTO COMANDO / COMANDO", patentes: ["ALTO COMANDO", "COMANDO", "SUB-COMANDO"] },
                    { nome: "CORPO DE PILOTOS", patentes: ["PILOTO VETERANO", "PILOTO SENIOR", "PILOTO OFICIAL", "PILOTO ESTAGIARIO", "ASPIRANTE A PILOTO"] },
                    { nome: "CORPO DE OPERADORES", patentes: ["OPERADOR VETERANO", "OPERADOR SENIOR", "OPERADOR OFICIAL", "TRIPULANTE OPERACIONAL", "ASPIRANTE OPERADOR"] }
                ];

                // Montagem dinâmica da estrutura da tabela com proteção contra sobreposição do Docsify
                let tabelaHtml = `
                <div class="main-container">
                    <h1 class="titulo-principal">1º BPM - HARDLINE</h1>
                    <a href="https://script.google.com/macros/s/AKfycbwtJEC35f80OO07rPrQ8fuWDcHbqnEQIQyUh8iVRwP-WB-KfIVM_IICr-rweX2eX864/exec" target="_blank" class="btn-cadastro">+ Cadastrar Novo Membro</a>

                    <div class="table-container">
                        <table class="tabela-membros">
                            <thead>
                                <tr>
                                    <th rowspan="2">ID</th>
                                    <th rowspan="2">NOME</th>
                                    <th rowspan="2">BADGE</th>
                                    <th rowspan="2">PATENTE</th>
                                    <th rowspan="2">UNIDADE</th>
                                    <th colspan="3" style="color: #ff4d4d !important;">ADVERTÊNCIAS</th>
                                    <th colspan="2">CURSOS</th>
                                </tr>
                                <tr>
                                    <th style="color: #f0a500 !important;">ADV 1</th>
                                    <th style="color: #f0a500 !important;">ADV 2</th>
                                    <th style="color: #f0a500 !important;">ADV 3</th>
                                    <th>C.F.A</th>
                                    <th>P.O.E</th>
                                </tr>
                            </thead>
                            <tbody>`;

                let temMembros = false;

                // Agrupamento inteligente por blocos
                blocosociais.forEach(bloco => {
                    const filtrados = membros.filter(m => bloco.patentes.includes(limparTexto(m.PATENTE)));
                    
                    if (filtrados.length > 0) {
                        temMembros = true;
                        tabelaHtml += `<tr><td colspan="10" class="cat-row">${bloco.nome}</td></tr>`;
                        
                        filtrados.forEach(m => {
                            let id = m.ID || "-";
                            let nome = m.NOME_ORIGINAL || "-";
                            let badge = m.BADGE || "-";
                            let patente = m.PATENTE_ORIGINAL || "-";
                            let unidade = m.UNIDADE || "-";
                            
                            // Processamento visual de advertências
                            let advTexto = (m.ADVERTENCIAS || m.ADV || "").toString().toUpperCase().replace(/\s+/g, '');
                            let adv1 = (advTexto.includes("ADV1") || advTexto.includes("ADV2") || advTexto.includes("ADV3")) ? '<span class="adv-marcado">☑</span>' : '<span class="check-vazio">☐</span>';
                            let adv2 = (advTexto.includes("ADV2") || advTexto.includes("ADV3")) ? '<span class="adv-marcado">☑</span>' : '<span class="check-vazio">☐</span>';
                            let adv3 = (advTexto.includes("ADV3")) ? '<span class="adv-marcado">☑</span>' : '<span class="check-vazio">☐</span>';

                            // Processamento visual de cursos realizados
                            let cursos = (m.CURSOS || "").toString().toUpperCase().replace(/\s+/g, '');
                            let cfa = (cursos.includes("C.F.A") || cursos.includes("CFA")) ? '<span class="check-marcado">☑</span>' : '<span class="check-vazio">☐</span>';
                            let poe = (cursos.includes("P.O.E") || cursos.includes("POE")) ? '<span class="check-marcado">☑</span>' : '<span class="check-vazio">☐</span>';

                            tabelaHtml += `<tr>
                                <td><b>${id}</b></td>
                                <td style="text-align:left !important; padding-left:15px !important;">${nome}</td>
                                <td>${badge}</td>
                                <td>${patente}</td>
                                <td>${unidade}</td>
                                <td class="col-adv">${adv1}</td>
                                <td class="col-adv">${adv2}</td>
                                <td class="col-adv">${adv3}</td>
                                <td>${cfa}</td>
                                <td>${poe}</td>
                            </tr>`;
                        });
                    }
                });

                if (!temMembros) {
                    tabelaHtml += `<tr><td colspan="10" style="padding:30px; color:#ff4d4d;">Nenhum membro ativo mapeado na planilha.</td></tr>`;
                }

                tabelaHtml += `</tbody></table></div></div>`;
                
                // Sobrescreve o contêiner geral com a tabela limpa e estruturada
                containerGeral.innerHTML = tabelaHtml;
            }
        });
    }, 50);
  })();
</script>
