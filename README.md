<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Banco Sara - Beta v0.0.1</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, Arial, sans-serif;
        }
        body {
            background: linear-gradient(180deg, #f9f6ed 0%, #ffffff 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 40px 20px;
        }
        .logo-container {
            width: 64px;
            height: 64px;
            background: #d4983d;
            border-radius: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 16px;
            box-shadow: 0 4px 12px rgba(212, 152, 61, 0.25);
        }
        .logo-simbolo {
            color: #ffffff;
            font-size: 36px;
            font-weight: bold;
            line-height: 1;
        }
        h1 {
            font-size: 28px;
            color: #1a202c;
            margin-bottom: 8px;
            font-weight: 700;
        }
        .subtitulo {
            color: #6b7280;
            font-size: 15px;
            margin-bottom: 16px;
        }
        .tag-demo {
            background: #fef3c7;
            color: #92400e;
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 13px;
            margin-bottom: 40px;
            font-weight: 500;
        }
        .perfis-container {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            max-width: 700px;
            width: 100%;
            margin-bottom: 40px;
        }
        @media (max-width: 600px) {
            .perfis-container {
                grid-template-columns: 1fr;
            }
        }
        .card-perfil {
            background: #ffffff;
            border: 2px solid transparent;
            border-radius: 16px;
            padding: 30px 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
        }
        .card-perfil.selecionado {
            border-color: #3b82f6;
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.15);
        }
        .card-perfil:hover {
            transform: translateY(-4px);
            box-shadow: 0 6px 16px rgba(0, 0, 0, 0.08);
        }
        .icone-perfil {
            width: 48px;
            height: 48px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 14px;
            font-size: 24px;
            color: #ffffff;
        }
        .aluno .icone-perfil { background: #3b82f6; }
        .professor .icone-perfil { background: #22c55e; }
        .colaborador .icone-perfil { background: #d4983d; }
        .nome-perfil {
            font-size: 17px;
            font-weight: 600;
            color: #1a202c;
            margin-bottom: 6px;
        }
        .desc-perfil {
            font-size: 12px;
            color: #6b7280;
            line-height: 1.4;
        }
        .btn-entrar {
            background: linear-gradient(90deg, #d4983d, #e0a84a);
            color: #ffffff;
            border: none;
            padding: 16px 40px;
            border-radius: 12px;
            font-size: 17px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 12px rgba(212, 152, 61, 0.3);
        }
        .btn-entrar:hover {
            transform: scale(1.03);
            box-shadow: 0 6px 18px rgba(212, 152, 61, 0.4);
        }
        .btn-entrar:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }
        .rodape {
            margin-top: auto;
            padding-top: 60px;
            font-size: 12px;
            color: #9ca3af;
            text-align: center;
        }

        /* Área de Demonstração */
        .area-demo {
            display: none;
            width: 100%;
            max-width: 500px;
            background: #ffffff;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
            margin-top: 20px;
        }
        .area-demo.ativa {
            display: block;
        }
        .titulo-demo {
            font-size: 22px;
            color: #1a202c;
            margin-bottom: 20px;
            text-align: center;
            font-weight: 700;
        }
        .info-card {
            background: #f9fafb;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 15px;
        }
        .info-label {
            font-size: 13px;
            color: #6b7280;
            margin-bottom: 5px;
        }
        .info-valor {
            font-size: 18px;
            font-weight: 600;
            color: #1a202c;
        }
        .saldo-valor {
            font-size: 32px;
            color: #22c55e;
            font-weight: bold;
        }
        .btn-voltar {
            background: #e5e7eb;
            color: #374151;
            border: none;
            padding: 12px 24px;
            border-radius: 10px;
            font-size: 15px;
            cursor: pointer;
            margin-top: 20px;
            width: 100%;
            font-weight: 500;
        }
        .btn-voltar:hover {
            background: #d1d5db;
        }
        .grafico-container {
            margin-top: 15px;
            padding: 15px;
            background: #f3f4f6;
            border-radius: 10px;
        }
        .grafico-barras {
            height: 80px;
            display: flex;
            align-items: flex-end;
            justify-content: center;
            gap: 10px;
        }
        .barra {
            width: 25px;
            background: #d4983d;
            border-radius: 4px 4px 0 0;
        }
        .tendencia {
            margin-top: 10px;
            font-weight: 600;
            text-align: center;
        }
        .alta { color: #22c55e; }
        .lista-historico {
            margin-top: 10px;
            font-size: 14px;
            color: #4b5563;
            line-height: 1.8;
        }
        .item-positivo { color: #16a34a; }
        .item-negativo { color: #dc2626; }
        .btn-acao {
            width: 100%;
            padding: 12px;
            margin: 5px 0;
            color: #ffffff;
            border: none;
            border-radius: 8px;
            font-size: 15px;
            cursor: pointer;
            font-weight: 500;
        }
        .btn-add { background: #22c55e; }
        .btn-rem { background: #ef4444; }
        .btn-ver { background: #3b82f6; }
    </style>
</head>
<body>

<!-- Tela Inicial -->
<div id="telaInicial" style="text-align: center;">
    <div class="logo-container">
        <span class="logo-simbolo">₿</span>
    </div>
    <h1>Banco Sara</h1>
    <p class="subtitulo">Versão Beta 0.0.1 • Demonstração Rápida</p>
    <div class="tag-demo">Sem necessidade de login</div>

    <div class="perfis-container">
        <div class="card-perfil aluno" id="cardAluno" onclick="selecionarPerfil('aluno')">
            <div class="icone-perfil">↗</div>
            <div class="nome-perfil">Aluno</div>
            <div class="desc-perfil">Ver saldo e histórico de Saras</div>
        </div>

        <div class="card-perfil professor" id="cardProfessor" onclick="selecionarPerfil('professor')">
            <div class="icone-perfil">📖</div>
            <div class="nome-perfil">Professor</div>
            <div class="desc-perfil">Adicionar/remover Saras dos alunos</div>
        </div>

        <div class="card-perfil colaborador" id="cardColaborador" onclick="selecionarPerfil('colaborador')">
            <div class="icone-perfil">🗂</div>
            <div class="nome-perfil">Colaborador</div>
            <div class="desc-perfil">Ver gráficos e dados gerais</div>
        </div>
    </div>

    <button class="btn-entrar" id="btnEntrar" onclick="entrarDemonstracao()" disabled>Entrar na Demonstração →</button>

    <div class="rodape">
        © 2026 Banco Sara • Versão Beta 0.0.1 • Para apresentação e demonstração
    </div>
</div>

<!-- Área de Demonstração -->
<div class="area-demo" id="areaDemo">
    <h2 class="titulo-demo" id="tituloDemo"></h2>
    <div id="conteudoDemo"></div>
    <button class="btn-voltar" onclick="voltar()">← Voltar</button>
</div>

<script>
let perfilSelecionado = null;

function selecionarPerfil(perfil) {
    perfilSelecionado = perfil;
    
    document.querySelectorAll('.card-perfil').forEach(card => {
        card.classList.remove('selecionado');
    });
    
    document.getElementById('card' + perfil.charAt(0).toUpperCase() + perfil.slice(1)).classList.add('selecionado');
    document.getElementById('btnEntrar').disabled = false;
}

function entrarDemonstracao() {
    if (!perfilSelecionado) return;
    
    document.getElementById('telaInicial').style.display = 'none';
    document.getElementById('areaDemo').classList.add('ativa');
    
    const tituloDemo = document.getElementById('tituloDemo');
    const conteudoDemo = document.getElementById('conteudoDemo');
    
    if (perfilSelecionado === 'aluno') {
        tituloDemo.textContent = 'Área do Aluno';
        conteudoDemo.innerHTML = `
            <div class="info-card">
                <div class="info-label">Nome</div>
                <div class="info-valor">João Silva</div>
            </div>
            <div class="info-card">
                <div class="info-label">Saldo de Saras</div>
                <div class="saldo-valor">250 Saras</div>
            </div>
            <div class="info-card">
                <div class="info-label">Última Movimentação</div>
                <div class="info-valor">+50 Saras • 21/08/2026</div>
            </div>
            <div class="info-card">
                <div class="info-label">Histórico</div>
                <div class="lista-historico">
                    <div class="item-positivo">+50 Saras - 21/08</div>
                    <div class="item-positivo">+30 Saras - 19/08</div>
                    <div class="item-negativo">-20 Saras - 15/08</div>
                    <div class="item-positivo">+40 Saras - 12/08</div>
                </div>
            </div>
        `;
    } 
    else if (perfilSelecionado === 'professor') {
        tituloDemo.textContent = 'Área do Professor';
        conteudoDemo.innerHTML = `
            <div class="info-card">
                <div class="info-label">Professor</div>
                <div class="info-valor">Vanessa Mendes</div>
            </div>
            <div class="info-card">
                <div class="info-label">Turma Responsável</div>
                <div class="info-valor">9º Ano A • 32 Alunos</div>
            </div>
            <div class="info-card">
                <div class="info-label">Ações Disponíveis</div>
                <div style="margin-top:10px;">
                    <button class="btn-acao btn-add">+ Adicionar Saras ao Aluno</button>
                    <button class="btn-acao btn-rem">− Remover Saras do Aluno</button>
                    <button class="btn-acao btn-ver">Ver Lista de Alunos</button>
                </div>
            </div>
        `;
    }
    else if (perfilSelecionado === 'colaborador') {
        tituloDemo.textContent = 'Área do Colaborador';
        conteudoDemo.innerHTML = `
            <div class="info-card">
                <div class="info-label">Colaborador</div>
                <div class="info-valor">Marcelo (Chefe)</div>
            </div>
            <div class="info-card">
                <div class="info-label">Total de Alunos no Sistema</div>
                <div class="info-valor">100 Alunos</div>
            </div>
            <div class="info-card">
                <div class="info-label">Total de Saras em Circulação</div>
                <div class="saldo-valor">24.580 Saras</div>
            </div>
            <div class="grafico-container">
                <p style="text-align:center; color:#374151; font-weight:600; margin-bottom:10px;">Movimentação Mensal</p>
                <div class="grafico-barras">
                    <div class="barra" style="height: 40px;"></div>
                    <div class="barra" style="height: 55px;"></div>
                    <div class="barra" style="height: 30px;"></div>
                    <div class="barra" style="height: 65px;"></div>
                    <div class="barra" style="height: 50px; background: #22c55e;"></div>
                </div>
                <div class="tendencia alta">↑ ALTA • Crescimento Positivo</div>
            </div>
        `;
    }
}

function voltar() {
    document.getElementById('areaDemo').classList.remove('ativa');
    document.getElementById('telaInicial').style.display = 'block';
    perfilSelecionado = null;
    document.querySelectorAll('.card-perfil').forEach(card => {
        card.classList.remove('selecionado');
    });
    document.getElementById('btnEntrar').disabled = true;
}
</script>
</body>
</html>
