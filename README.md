<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jacque Pegue&Monte - Orçamentos</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap');
        body { font-family: 'Inter', sans-serif; background-color: #fff5f8; }
        .modal { display: none; }
        .modal.active { display: flex; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        
        @media print {
            body * { visibility: hidden; }
            #printable-area, #printable-area * { visibility: visible; }
            #printable-area { position: absolute; left: 0; top: 0; width: 100%; display: block !important; padding: 20px; }
            .no-print { display: none !important; }
        }
    </style>
</head>
<body class="pb-40">

    <header class="bg-white border-b border-pink-100 p-4 sticky top-0 z-30 shadow-sm">
        <div class="max-w-lg mx-auto flex justify-between items-center">
            <div class="flex items-center gap-2">
                <div class="bg-pink-600 p-1.5 rounded-lg">
                    <i data-lucide="sparkles" class="text-white w-4 h-4"></i>
                </div>
                <div>
                    <h1 class="text-lg font-extrabold text-pink-600 leading-none">Jacque Pegue&Monte</h1>
                    <p class="text-[8px] text-pink-400 font-bold uppercase tracking-widest mt-1">FESTA LINDA, preço que cabe no bolso</p>
                </div>
            </div>
            <div class="flex items-center gap-2 px-3 py-1.5 rounded-full">
                <i data-lucide="unlock" class="w-5 text-green-500"></i>
            </div>
        </div>
    </header>

    <main class="p-4 max-w-lg mx-auto space-y-4">
        <section class="bg-white rounded-2xl p-4 shadow-sm border border-pink-50 space-y-3">
            <div>
                <label class="text-[10px] font-bold text-pink-400 uppercase ml-1">Nome do Cliente</label>
                <input type="text" id="clientName" class="w-full bg-pink-50/30 border border-pink-100 rounded-xl px-4 py-2.5 text-sm font-semibold outline-none focus:border-pink-300" placeholder="Ex: Maria Souza">
            </div>
            <div class="grid grid-cols-2 gap-3">
                <div class="col-span-1">
                    <label class="text-[10px] font-bold text-pink-400 uppercase ml-1">Homenageado</label>
                    <input type="text" id="celebrantName" class="w-full bg-pink-50/30 border border-pink-100 rounded-xl px-4 py-2.5 text-sm font-semibold outline-none" placeholder="Nome">
                </div>
                <div class="col-span-1">
                    <label class="text-[10px] font-bold text-pink-400 uppercase ml-1">Tema</label>
                    <select id="selectedTheme" onchange="toggleOtherThemeField()" class="w-full bg-pink-50/30 border border-pink-100 rounded-xl px-4 py-2.5 text-sm font-semibold outline-none">
                        <option value="Personalizado">Personalizado</option>
                        <option value="Fazendinha">Fazendinha</option>
                        <option value="Fazendinha rosa">Fazendinha rosa</option>
                        <option value="Fazendinha do Mickey">Fazendinha do Mickey</option>
                        <option value="Patrulha Canina">Patrulha Canina</option>
                        <option value="Dragon Ball">Dragon Ball</option>
                        <option value="Chá de Panela">Chá de Panela</option>
                        <option value="Chá Revelação">Chá Revelação</option>
                        <option value="Aniversário 365 Sorrisos">Aniversário 365 Sorrisos</option>
                        <option value="Princesas">Princesas</option>
                        <option value="Rapunzel">Rapunzel</option>
                        <option value="Minnie">Minnie</option>
                        <option value="Mickey">Mickey</option>
                        <option value="Minecraft">Minecraft</option>
                        <option value="Tardezinha">Tardezinha</option>
                        <option value="Oh Baby">Oh Baby</option>
                        <option value="Emília">Emília</option>
                        <option value="Futebol">Futebol</option>
                        <option value="Lilo e Stitch">Lilo e Stitch</option>
                        <option value="Bluey">Bluey</option>
                        <option value="Bobbie Goods">Bobbie Goods</option>
                        <option value="Hello Kitty">Hello Kitty</option>
                        <option value="Safari">Safari</option>
                        <option value="Ovelhinha">Ovelhinha</option>
                        <option value="Vasco">Vasco</option>
                        <option value="São Paulo">São Paulo</option>
                        <option value="Super Mário">Super Mário</option>
                        <option value="Boiadeira">Boiadeira</option>
                        <option value="Bento e Totó">Bento e Totó</option>
                        <option value="Vingadores">Vingadores</option>
                        <option value="Moranguinho">Moranguinho</option>
                        <option value="Lego">Lego</option>
                        <option value="Barbie">Barbie</option>
                        <option value="Kuromi">Kuromi</option>
                        <option value="Homem Aranha">Homem Aranha</option>
                        <option value="Hot Wheels">Hot Wheels</option>
                        <option value="Feliz Ano Novo">Feliz Ano Novo</option>
                        <option value="Feliz Natal">Feliz Natal</option>
                        <option value="Formatura">Formatura</option>
                        <option value="ABC">ABC</option>
                        <option value="OUTRO">Outro Tema...</option>
                    </select>
                </div>
            </div>
            <div id="otherThemeContainer" class="hidden animate-in fade-in duration-300">
                <label class="text-[10px] font-bold text-pink-400 uppercase ml-1">Informe o Tema Desejado</label>
                <input type="text" id="otherThemeName" class="w-full bg-pink-50/30 border border-pink-100 rounded-xl px-4 py-2.5 text-sm font-semibold outline-none focus:border-pink-300" placeholder="Qual o tema da sua festa?">
            </div>
        </section>

        <div class="flex overflow-x-auto gap-2 no-scrollbar py-1" id="category-tabs"></div>
        <section id="items-grid" class="space-y-4"></section>
    </main>

    <footer class="fixed bottom-0 left-0 right-0 bg-white border-t border-pink-100 p-4 shadow-[0_-10px_25px_rgba(0,0,0,0.05)] z-40">
        <div class="max-w-lg mx-auto">
            <div class="flex justify-between items-end mb-4">
                <div>
                    <span class="text-[10px] font-bold text-gray-400 uppercase block">Total Estimado</span>
                    <span id="total-price" class="text-2xl font-extrabold text-gray-800 tracking-tight">R$ 0,00</span>
                </div>
                <div class="text-right">
                    <span class="text-[9px] font-bold text-pink-400 uppercase block">Chave PIX (Jacque)</span>
                    <button onclick="copyPix()" class="bg-pink-50 text-pink-600 px-3 py-1 rounded-lg text-[11px] font-bold border border-pink-100">62981695886</button>
                </div>
            </div>
            
            <div class="grid grid-cols-4 gap-2">
                <button onclick="resetApp()" id="btn-reset" class="flex items-center justify-center h-12 bg-gray-50 text-gray-600 rounded-xl border border-gray-100" title="Limpar">
                    <i data-lucide="trash-2"></i>
                </button>
                <button onclick="openInvite()" id="btn-invite" class="flex items-center justify-center h-12 bg-blue-50 text-blue-600 rounded-xl border border-blue-100" title="Reserva">
                    <i data-lucide="calendar"></i>
                </button>
                <button onclick="prepareContract()" id="btn-contract" class="flex items-center justify-center h-12 bg-pink-50 text-pink-600 rounded-xl border border-pink-200" title="Resumo">
                    <i data-lucide="file-text"></i>
                </button>
                <button onclick="sendToWhatsApp()" id="btn-send" class="col-span-1 flex items-center justify-center gap-2 h-12 bg-green-600 text-white rounded-xl font-bold text-sm">
                    <i data-lucide="send" class="w-5"></i> ENVIAR
                </button>
            </div>
        </div>
    </footer>

    <div id="modal-invite" class="modal fixed inset-0 bg-black/60 z-[100] items-center justify-center p-4 backdrop-blur-sm">
        <div class="bg-white w-full max-w-xs rounded-3xl overflow-hidden text-center space-y-4 pb-6">
            <div class="bg-blue-600 p-4 text-white flex justify-between items-center">
                <h2 class="font-bold text-sm uppercase tracking-widest">Informações</h2>
                <button onclick="closeModal('modal-invite')"><i data-lucide="x"></i></button>
            </div>
            <div class="p-4 space-y-2">
                <i data-lucide="party-popper" class="w-10 h-10 text-blue-600 mx-auto"></i>
                <p class="text-sm font-bold text-gray-800">Reserva sob consulta!</p>
                <p class="text-[10px] text-gray-500">Envie o orçamento para verificarmos a disponibilidade da data desejada.</p>
            </div>
            <button onclick="closeModal('modal-invite')" class="mx-6 py-2 px-6 bg-blue-600 text-white rounded-xl font-bold text-xs">ENTENDI</button>
        </div>
    </div>

    <div id="modal-contract" class="modal fixed inset-0 bg-black/60 z-[100] items-center justify-center p-4 backdrop-blur-sm">
        <div class="bg-white w-full max-w-lg rounded-3xl overflow-hidden flex flex-col max-h-[90vh]">
            <div class="bg-pink-600 p-4 text-white flex justify-between items-center">
                <h2 class="font-bold text-sm uppercase tracking-widest">Resumo do Orçamento</h2>
                <button onclick="closeModal('modal-contract')"><i data-lucide="x"></i></button>
            </div>
            <div class="flex-1 overflow-y-auto p-6 bg-white" id="printable-area">
                <div id="c-items-list" class="space-y-4 text-[11px]"></div>
            </div>
            <div class="p-4 bg-gray-50 border-t flex gap-2 no-print">
                <button onclick="sendDetailedWhatsApp()" class="flex-1 py-3 bg-green-600 text-white rounded-xl font-bold text-xs flex items-center justify-center gap-2"><i data-lucide="send" class="w-4"></i> ENVIAR RESUMO WHATSAPP</button>
                <button onclick="window.print()" class="py-3 px-4 bg-pink-100 text-pink-600 rounded-xl font-bold text-xs flex items-center justify-center" title="Imprimir"><i data-lucide="printer" class="w-4"></i></button>
            </div>
        </div>
    </div>

    <script>
        const phoneNumber = "5562981695886";
        let cart = [];
        let currentTab = 'Tudo';

        const inventory = [
            { 
                id: 1, name: 'KIT BÁSICO', price: 116.00, icon: '🌟', category: 'Combos', 
                desc: '1 Painel Redondo\n1 Trio de Cilindros\n1 Tapete\n1 Boleira\n4 Bandejas\nBuchinhos ou flores\nNúmero de MDF' 
            },
            { 
                id: 2, name: 'KIT PREMIUM', price: 170.00, icon: '👑', category: 'Combos', 
                desc: '1 Painel Redondo\n1 Painel Romano\n1 Trio de Cilindros\n1 Mesa Fake\n1 Tapete\n1 Boleira\n6 Bandejas\nBuchinhos ou flores\nNúmero de MDF\nEscadinha para lembrancinhas' 
            },
            { 
                id: 3, name: 'KIT ADULTO', price: 152.00, icon: '🥂', category: 'Combos', 
                desc: '1 Painel Romano\n1 Happy Birthday\n1 Trio Mesas Ripadas ou 1 Trio de Cilindros\n1 Tapete\n1 Boleira\n4 Bandejas\nBuchinhos ou flores\nNúmero de MDF' 
            },
            {
                id: 4, name: 'ARCO DE BALÕES (1 M)', price: 60.00, icon: '🎈', category: 'Balões',
                desc: 'Arco de balões com 1 metro de comprimento.'
            },
            {
                id: 5, name: 'ARCO DE BALÕES (1,5 M)', price: 80.00, icon: '🎈', category: 'Balões',
                desc: 'Arco de balões com 1,5 metros de comprimento.'
            },
            {
                id: 6, name: 'ARCO DE BALÕES (2 M)', price: 100.00, icon: '🎈', category: 'Balões',
                desc: 'Arco de balões com 2 metros de comprimento.'
            }
        ];

        function init() { 
            renderCats(); 
            renderItems(); 
            lucide.createIcons();
        }

        function toggleOtherThemeField() {
            const select = document.getElementById('selectedTheme');
            const container = document.getElementById('otherThemeContainer');
            if (select.value === 'OUTRO') {
                container.classList.remove('hidden');
            } else {
                container.classList.add('hidden');
                document.getElementById('otherThemeName').value = '';
            }
        }

        function getThemeName() {
            const select = document.getElementById('selectedTheme');
            if (select.value === 'OUTRO') {
                return document.getElementById('otherThemeName').value || "Outro (nao informado)";
            }
            return select.value;
        }

        function renderCats() {
            const container = document.getElementById('category-tabs');
            const cats = ['Tudo', 'Combos', 'Balões'];
            container.innerHTML = cats.map(cat => `
                <button onclick="filterByCat('${cat}')" class="whitespace-nowrap px-4 py-1.5 rounded-full text-[10px] font-bold uppercase transition-all ${currentTab === cat ? 'bg-pink-600 text-white' : 'bg-white text-pink-400 border border-pink-100'}">
                    ${cat}
                </button>
            `).join('');
        }

        function filterByCat(cat) {
            currentTab = cat;
            renderCats();
            renderItems();
        }

        function renderItems() {
            const grid = document.getElementById('items-grid');
            grid.innerHTML = '';
            
            const filtered = currentTab === 'Tudo' ? inventory : inventory.filter(i => i.category === currentTab);

            filtered.forEach(item => {
                const inCart = cart.find(c => c.id === item.id);
                const div = document.createElement('div');
                div.className = `p-4 bg-white rounded-2xl border transition-all ${inCart ? 'border-pink-500 bg-pink-50/20 shadow-md scale-[1.01]' : 'border-pink-50 shadow-sm'}`;
                
                const formattedDesc = item.desc.replace(/\n/g, '<br>');

                div.innerHTML = `
                    <div class="flex items-start justify-between">
                        <div class="flex items-center gap-3">
                            <div class="w-10 h-10 bg-pink-50 rounded-xl flex items-center justify-center text-xl">${item.icon}</div>
                            <div>
                                <h3 class="text-sm font-extrabold text-gray-800 uppercase">${item.name}</h3>
                                <p class="text-pink-600 font-black text-sm">R$ ${item.price.toFixed(2)}</p>
                            </div>
                        </div>
                        <div class="flex items-center gap-2">
                            ${inCart ? `<button onclick="updateQty(${item.id}, -1)" class="w-8 h-8 bg-pink-100 text-pink-600 rounded-lg font-bold">-</button>` : ''}
                            <button onclick="updateQty(${item.id}, 1)" class="w-10 h-10 ${inCart ? 'bg-pink-600 text-white' : 'bg-pink-50 text-pink-600'} rounded-xl font-bold">
                                ${inCart ? inCart.qty : '+'}
                            </button>
                        </div>
                    </div>
                    <div class="mt-3 p-3 bg-gray-50 rounded-xl border border-dashed border-pink-200">
                        <p class="text-[11px] text-gray-700 leading-relaxed font-medium">
                            ${formattedDesc}
                        </p>
                    </div>
                `;
                grid.appendChild(div);
            });
            lucide.createIcons();
        }

        function updateQty(id, delta) {
            const idx = cart.findIndex(c => c.id === id);
            if(idx > -1) { 
                cart[idx].qty += delta; 
                if(cart[idx].qty <= 0) cart.splice(idx, 1); 
            } else { 
                cart.push({...inventory.find(i => i.id === id), qty: 1}); 
            }
            updateTotal(); 
            renderItems();
        }

        function updateTotal() {
            const total = cart.reduce((acc, i) => acc + (i.price * i.qty), 0);
            document.getElementById('total-price').textContent = `R$ ${total.toFixed(2)}`;
        }

        function prepareContract() {
            if(cart.length === 0) { alert("Adicione itens ao orçamento primeiro."); return; }
            const client = document.getElementById('clientName').value || "Não informado";
            const theme = getThemeName();
            const celebrant = document.getElementById('celebrantName').value || "---";

            const list = document.getElementById('c-items-list');
            list.innerHTML = `
                <div class="text-center mb-6">
                    <h2 class="font-black text-lg text-pink-600">ORÇAMENTO DETALHADO</h2>
                    <p class="text-[9px] text-gray-400">JACQUE PEGUE&MONTE</p>
                </div>
                <div class="bg-pink-50 p-3 rounded-xl mb-4 border border-pink-100">
                    <p><strong>Cliente:</strong> ${client}</p>
                    <p><strong>Tema:</strong> ${theme}</p>
                    <p><strong>Homenageado:</strong> ${celebrant}</p>
                </div>
            `;
            
            cart.forEach(i => {
                const formattedContractDesc = i.desc.split('\n').map(line => `• ${line}`).join('<br>');
                list.innerHTML += `
                    <div class="border-b border-pink-100 pb-3 mb-3">
                        <div class="flex justify-between font-bold text-gray-800 uppercase text-[12px]">
                            <span>${i.qty}x ${i.name}</span>
                            <span>R$ ${(i.price * i.qty).toFixed(2)}</span>
                        </div>
                        <p class="text-[10px] text-gray-500 mt-2 pl-2 leading-tight">
                            ${formattedContractDesc}
                        </p>
                    </div>`;
            });

            const totalVal = document.getElementById('total-price').textContent;
            list.innerHTML += `
                <div class="mt-6 p-4 bg-gray-900 text-white rounded-2xl flex justify-between items-center">
                    <span class="font-bold text-sm uppercase">Total Geral</span>
                    <span class="text-xl font-black">${totalVal}</span>
                </div>
                <p class="text-[9px] text-center text-gray-400 mt-4 italic">Valido por 48 horas. Reserva mediante sinal de 50%.</p>
            `;
            openModal('modal-contract');
        }

        function openInvite() { openModal('modal-invite'); }
        function closeModal(id) { document.getElementById(id).classList.remove('active'); }
        function openModal(id) { 
            document.getElementById(id).classList.add('active'); 
            lucide.createIcons(); 
        }
        
        function resetApp() { 
            if(cart.length > 0 && confirm("Deseja limpar todo o orçamento?")) {
                cart = []; 
                document.getElementById('clientName').value = '';
                document.getElementById('celebrantName').value = '';
                document.getElementById('selectedTheme').value = 'Personalizado';
                document.getElementById('otherThemeContainer').classList.add('hidden');
                document.getElementById('otherThemeName').value = '';
                updateTotal(); 
                renderItems(); 
            }
        }

        function copyPix() { 
            const pix = "62981695886";
            const el = document.createElement('textarea');
            el.value = pix;
            document.body.appendChild(el);
            el.select();
            document.execCommand('copy');
            document.body.removeChild(el);
            alert("PIX Copiado!"); 
        }

        function sendToWhatsApp() {
            if(cart.length === 0) { alert("Adicione itens para enviar o orçamento."); return; }
            
            const client = document.getElementById('clientName').value || "Cliente";
            const theme = getThemeName();
            const celebrant = document.getElementById('celebrantName').value || "---";
            const totalVal = document.getElementById('total-price').textContent;

            let msg = `GOSTARIA DE FECHAR ESSE ORCAMENTO\n\n`;
            msg += `CLIENTE: ${client}\n`;
            msg += `TEMA: ${theme}\n`;
            msg += `HOMENAGEADO: ${celebrant}\n`;
            msg += `-------------------------------------\n`;
            
            cart.forEach(i => {
                msg += `${i.qty}x ${i.name} (R$ ${(i.price * i.qty).toFixed(2)})\n`;
            });
            
            msg += `-------------------------------------\n`;
            msg += `TOTAL: ${totalVal}\n\n`;
            msg += `Aguardo confirmacao de disponibilidade.`;

            window.open(`https://wa.me/${phoneNumber}?text=${encodeURIComponent(msg)}`, '_blank');
        }

        function sendDetailedWhatsApp() {
            if(cart.length === 0) return;

            const client = document.getElementById('clientName').value || "Cliente";
            const theme = getThemeName();
            const celebrant = document.getElementById('celebrantName').value || "---";
            const totalVal = document.getElementById('total-price').textContent;

            let msg = `RESUMO DO ORCAMENTO - JACQUE PEGUE E MONTE\n\n`;
            msg += `CLIENTE: ${client}\n`;
            msg += `TEMA: ${theme}\n`;
            msg += `HOMENAGEADO: ${celebrant}\n`;
            msg += `-------------------------------------\n\n`;
            
            cart.forEach(i => {
                msg += `${i.qty}x ${i.name}\n`;
                msg += `Valor: R$ ${(i.price * i.qty).toFixed(2)}\n`;
                const lines = i.desc.split('\n');
                lines.forEach(line => {
                    msg += `- ${line}\n`;
                });
                msg += `\n`;
            });
            
            msg += `-------------------------------------\n`;
            msg += `TOTAL GERAL: ${totalVal}\n\n`;
            msg += `Reserva mediante sinal de 50%.\n`;
            msg += `Valido por 48 horas.`;

            window.open(`https://wa.me/${phoneNumber}?text=${encodeURIComponent(msg)}`, '_blank');
        }

        window.onload = init;
    </script>
</body>
</html>
