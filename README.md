<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="google-site-verification" content="AGUARDANDO_CODIGO" />
    
    <title>Mundo das IAs | O Guia Profissional 2026</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-slate-50 text-slate-900">
    <div class="max-w-6xl mx-auto px-4 py-12">
        <header class="text-center mb-16">
            <h1 class="text-5xl font-extrabold mb-4 text-blue-600">Mundo das IAs</h1>
            <p class="text-xl text-slate-600">Diretório atualizado das melhores inteligências artificiais para sua profissão.</p>
        </header>

        <div id="cards-container" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            </div>

        <footer class="mt-20 py-8 border-t text-center text-slate-500">
            <p>&copy; 2026 Mundo das IAs - Renda Automática com Tecnologia</p>
            <div class="mt-2">
                <a href="#" class="hover:underline">Privacidade</a> | 
                <a href="#" class="hover:underline">Sobre Nós</a>
            </div>
        </footer>
    </div>

    <script>
        // Substitua pelo seu link CSV quando quiser atualizar
        const urlCSV = "https://docs.google.com/spreadsheets/d/e/2PACX-1vTpSTfK25-ua58vCKKZ7IxNGn4ZQ2EaoqOD261M4fhTJkvA-slW2kL8hAL5jWTq2rbcSkAhVB5nqekW/pub?output=csv";

        async function carregarIAs() {
            try {
                const response = await fetch(urlCSV);
                const data = await response.text();
                const linhas = data.split('\n').slice(1);
                const container = document.getElementById('cards-container');
                container.innerHTML = ""; // Limpa antes de carregar

                linhas.forEach(linha => {
                    const colunas = linha.split(',');
                    if (colunas.length >= 4) {
                        const [profissao, nome, desc, link] = colunas;
                        container.innerHTML += `
                            <div class="bg-white p-6 rounded-2xl shadow-md border border-slate-200 hover:scale-105 transition-transform duration-300">
                                <span class="bg-blue-100 text-blue-700 text-xs font-bold px-3 py-1 rounded-full uppercase italic">${profissao}</span>
                                <h3 class="text-2xl font-bold mt-4 text-slate-800">${nome}</h3>
                                <p class="text-slate-600 mt-2 mb-6 h-12 overflow-hidden">${desc}</p>
                                <a href="${link}" target="_blank" class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-3 rounded-xl block text-center font-bold shadow-lg transition">Experimentar IA</a>
                            </div>
                        `;
                    }
                });
            } catch (e) {
                console.error("Erro ao carregar os dados:", e);
            }
        }
        carregarIAs();
    </script>
</body>
</html>
