<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mundo das IAs | Guia 2026</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-slate-50 text-slate-900">
    <div class="max-w-6xl mx-auto px-4 py-12">
        <header class="text-center mb-16">
            <h1 class="text-5xl font-extrabold mb-4 text-blue-600">Mundo das IAs</h1>
            <p class="text-xl text-slate-600">As melhores ferramentas para automatizar seu trabalho.</p>
        </header>
        <div id="cards-container" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 text-center">
            <p id="loading-msg" class="col-span-full text-lg text-slate-400">Carregando diretório de inteligências...</p>
        </div>
    </div>

    <script>
        const urlCSV = "https://docs.google.com/spreadsheets/d/1JWFx-YfcyHPvsbI9RYO6YGUfHlS37TmoB6jcyYVzRFo/edit?usp=sharing";

        function parseCSV(text) {
            // Esta função ignora vírgulas problemáticas
            const lines = text.split(/\r?\n/);
            return lines.map(line => {
                const result = [];
                let current = '';
                let inQuotes = false;
                for (let char of line) {
                    if (char === '"') inQuotes = !inQuotes;
                    else if (char === ',' && !inQuotes) {
                        result.push(current);
                        current = '';
                    } else current += char;
                }
                result.push(current);
                return result;
            });
        }

        async function carregarIAs() {
            try {
                const response = await fetch(urlCSV);
                const text = await response.text();
                const data = parseCSV(text).slice(1); // Pula cabeçalho
                const container = document.getElementById('cards-container');
                
                if (data.length === 0) throw new Error("Sem dados");
                container.innerHTML = ""; 

                data.forEach(col => {
                    if (col.length >= 4 && col[1].trim() !== "") {
                        const [profissao, nome, desc, link] = col;
                        container.innerHTML += `
                            <div class="bg-white p-6 rounded-2xl shadow-md border border-slate-200 hover:scale-105 transition-transform duration-300 flex flex-col justify-between text-left">
                                <div>
                                    <span class="bg-blue-100 text-blue-700 text-xs font-bold px-3 py-1 rounded-full uppercase">${profissao}</span>
                                    <h3 class="text-2xl font-bold mt-4 text-slate-800">${nome}</h3>
                                    <p class="text-slate-600 mt-2 mb-6 line-clamp-3">${desc}</p>
                                </div>
                                <a href="${link}" target="_blank" class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-3 rounded-xl block text-center font-bold shadow-lg transition mt-auto">Acessar IA</a>
                            </div>
                        `;
                    }
                });
            } catch (e) {
                document.getElementById('loading-msg').innerText = "Erro ao carregar dados. Verifique se a planilha está publicada.";
            }
        }
        carregarIAs();
    </script>
</body>
</html>
