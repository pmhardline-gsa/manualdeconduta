# 1º BPM - HARDLINE

<div style="text-align: center; margin-bottom: 25px;">
    <a href="https://script.google.com/macros/s/AKfycbwtJEC35f80OO07rPrQ8fuWDcHbqnEQIQyUh8iVRwP-WB-KfIVM_IICr-rweX2eX864/exec" target="_blank" class="btn-cadastro">+ Cadastrar Novo Membro</a>
</div>

<div class="table-container">
    <table id="tabela">
        <thead>
            <tr>
                <th rowspan="2">ID</th><th rowspan="2">NOME</th><th rowspan="2">BADGE</th><th rowspan="2">PATENTE</th><th rowspan="2">UNIDADE</th>
                <th colspan="3" style="color: #ff4d4d; letter-spacing: 1px;">ADVERTÊNCIAS</th><th colspan="2">CURSOS</th>
            </tr>
            <tr>
                <th style="color: #f0a500;">ADV 1</th><th style="color: #f0a500;">ADV 2</th><th style="color: #f0a500;">ADV 3</th><th>C.F.A</th><th>P.O.E</th>
            </tr>
        </thead>
        <tbody id="corpo-tabela">
            <tr><td colspan="10" style="color:#f0a500; padding: 20px;">Carregando dados do efetivo...</td></tr>
        </tbody>
    </table>
</div>

<style>
    .btn-cadastro { display: inline-block; background: #f0a500; color: #000 !important; padding: 12px 24px; border-radius: 6px; text-decoration: none; font-weight: bold; transition: 0.3s; }
    .btn-cadastro:hover { background: #d48e00; }
    .table-container { background: #141923; border-radius: 12px; overflow-x: auto; border: 1px solid #232b3c; margin-top: 20px; }
    table { width: 100%; border-collapse: collapse; }
    th { background: #1c2434; color: #f0a500 !important; padding: 12px; font-size: 0.8em; text-transform: uppercase; border: 1px solid #232b3c; }
    td { padding: 12px; border: 1px solid #1a202c; text-align: center; color: #e2e8f0 !important; }
    
    .col-adv { background-color: rgba(240, 165, 0, 0.04); border: 1px solid #1a202c; }
    .cat-row { background: #1c2434; font-weight: bold; text-align: left !important; padding-left: 20px !important; color: #f0a500 !important; text-transform: uppercase; letter-spacing: 1px; }
    tr:hover { background: #1a202c; }
    
    .check-marcado { color: #f0a500; font-weight: bold; }
    .adv-marcado { color: #ff4d4d; font-weight: bold; }
    .check-vazio { color: #4a5568; }
</style>

<script>
  (function() {
    function puxarDadosPlanilha() {
        const corpo = document.getElementById("corpo-tabela");
        
        // Se o Docsify ainda não terminou de criar o elemento na tela, tenta novamente em 100 milissegundos
        if (!corpo) {
            setTimeout(puxarDadosPlanilha, 100);
            return;
        }

        const baseUrl = "https://docs.google.com/spreadsheets/d/e/2PACX-1vSw-LdIv-3xH3eswHp06gAaxJI8e9aJcrfyuBPPhBIyc6lwHww33rXMhYei5JzTfDxAc96w2kBZ2DWb/pub?output=csv";
        const URL = baseUrl + "&_t=" + new Date().getTime();

        function limparString(str) {
            if (!str) return "";
            return str.toString().normalize("NFD").replace(/[\u0300-\u036f]/g, "").trim().toUpperCase();
        }

        const hierarquia = {
            "ALTO COMANDO": 1, "COMANDO": 2, "SUB-COMANDO": 3,
            "PILOTO VETERANO": 4, "PILOTO SENIOR": 5, "PILOTO OFICIAL": 6, "PILOTO ESTAGIARIO": 7, "ASPIRANTE A PILOTO": 8,
            "OPERADOR VETERANO": 9, "OPERADOR SENIOR": 10, "OPERADOR OFICIAL": 11, "TRIPULANTE OPERACIONAL": 12, "ASPIRANTE OPERADOR": 13
        };

        Papa.parse(URL, { 
            download: true, 
            header: true,
            skipEmptyLines: true,
            complete: function(res) {
                corpo.innerHTML = "";

                if (!res.data || res.data.length === 0) {
                    corpo.innerHTML = `<tr><td colspan="10" style="color:#ff4d4d; padding: 20px;">Nenhum dado encontrado. Verifique o link da planilha.</td></tr>`;
                    return;
                }

                let dadosNormalizados = res.data.map(linha => {
                    let novaLinha = {};
                    for (let chave in linha) {
                        let chaveLimpa = chave.normalize("NFD").replace(/[\u0300-\u036f]/g, "").replace(/[^a-zA-Z0-9]/g, "").toUpperCase();
                        novaLinha[chaveLimpa] = linha[chave];
                    }
                    novaLinha.PATENTE_ORIGINAL = linha.Patente || linha.PATENTE || novaLinha.PATENTE || "-";
                    novaLinha.NOME_ORIGINAL = linha.Nome || linha.NOME || novaLinha.NOME || "-";
                    return novaLinha;
                });

                let membrosValidos = dadosNormalizados.filter(m => m.ID && m.ID.toString().trim() !== "");

                membrosValidos.sort((a, b) => {
                    let patA = limparString(a.PATENTE);
                    let patB = limparString(b.PATENTE);
                    return (hierarquia[patA] || 99) - (hierarquia[patB] || 99);
                });

                const categorias = [
                    { nome: "ALTO COMANDO / COMANDO", patentes: ["ALTO COMANDO", "COMANDO", "SUB-COMANDO"] },
                    { nome: "CORPO DE PILOTOS", patentes: ["PILOTO VETERANO", "PILOTO SENIOR", "PILOTO OFICIAL", "PILOTO ESTAGIARIO", "ASPIRANTE A PILOTO"] },
                    { nome: "CORPO DE OPERADORES", patentes: ["OPERADOR VETERANO", "OPERADOR SENIOR", "OPERADOR OFICIAL", "TRIPULANTE OPERACIONAL", "ASPIRANTE OPERADOR"] }
                ];

                categorias.forEach(cat => {
                    const membrosDaCategoria = membrosValidos.filter(m => {
                        let pat = limparString(m.PATENTE);
                        return cat.patentes.includes(pat);
                    });
                    
                    if (membrosDaCategoria.length > 0) {
                        corpo.innerHTML += `<tr><td colspan="10" class="cat-row">${cat.nome}</td></tr>`;
                        
                        membrosDaCategoria.forEach(m => {
                            let id = m.ID || "-";
                            let nome = m.NOME_ORIGINAL || m.NOME || "-";
                            let badge = m.BADGE || "-";
                            let patente = m.PATENTE_ORIGINAL || "-";
                            let unidade = m.UNIDADE || "-";
                            
                            let advTexto = (m.ADVERTENCIAS || m.ADV || "").toString().toUpperCase().replace(/\s+/g, '');
                            let adv1 = (advTexto.includes("ADV1") || advTexto.includes("ADV2") || advTexto.includes("ADV3")) ? '<span class="adv-marcado">☑</span>' : '<span class="check-vazio">☐</span>';
                            let adv2 = (advTexto.includes("ADV2") || advTexto.includes("ADV3")) ? '<span class="adv-marcado">☑</span>' : '<span class="check-vazio">☐</span>';
                            let adv3 = (advTexto.includes("ADV3")) ? '<span class="adv-marcado">☑</span>' : '<span class="check-vazio">☐</span>';

                            let cursosLimpo = (m.CURSOS || "").toString().toUpperCase().replace(/\s+/g, '');
                            let cfa = (cursosLimpo.includes("C.F.A") || cursosLimpo.includes("CFA")) ? '<span class="check-marcado">☑</span>' : '<span class="check-vazio">☐</span>';
                            let poe = (cursosLimpo.includes("P.O.E") || cursosLimpo.includes("POE")) ? '<span class="check-marcado">☑</span>' : '<span class="check-vazio">☐</span>';

                            corpo.innerHTML += `<tr>
                                <td>${id}</td>
                                <td style="text-align:left; padding-left:15px;">${nome}</td>
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
            }
        });
    }

    // Inicializa a carga imediatamente
    puxarDadosPlanilha();
  })();
</script>
