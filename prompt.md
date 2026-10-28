# Crie um aplicativo SaaS chamado Grounded (MVP Funcional)

## 1. VISÃO DO PRODUTO E PRIORIDADE MÁXIMA
Grounded é uma plataforma de otimização de currículos para processos seletivos.

- O app deve ser 100% funcional imediatamente na primeira geração, rodando direto no navegador (client-side) sem depender de chamadas externas de IA ou backend para a entrega de valor inicial.
- Sem autenticação ou cadastro: o usuário entra e usa imediatamente.
- Histórico e clipes devem ser salvos no `localStorage` para persistência entre recarregamentos.

## 2. DESIGN SYSTEM E IDENTIDADE VISUAL
- Nome: Grounded
- Slogan: "Transforme vagas em oportunidades."
- Estilo: Inspirado em Notion, Linear e Stripe Dashboard (minimalista, profissional, bordas arredondadas e sombras suaves).
- Componentes: exclusivamente shadcn/ui e ícones Lucide.
- Cores:
  - Primária: #6D1F33 (Vinho)
  - Marrom terroso: #8B5E3C
  - Cinza concreto: #A7A6A1
  - Carvão: #3A3A3A
  - Bege claro: #EAE3D9
  - Fundo padrão: #F7F3EE (Light mode com suporte a Dark mode).
- Internacionalização (i18n): Seletor global no topo para alternar entre Português (Brasil) e English (US).

## 3. PÁGINA INICIAL (ONBOARDING & TESTE IMEDIATO)
Criar uma seção de destaque "Experimente Agora em 30 Segundos":
- Dois botões de vagas pré-configuradas:
  - 🏢 Testar com vaga da Microsoft (Software Engineer)
  - 💜 Testar com vaga do Nubank (Product Engineer)
- Botão de currículo rápido:
  - 📄 Carregar currículo de exemplo (Full Stack Developer realista)
Ao clicar nesses botões, os dados devem preencher os formulários automaticamente.

Campos de entrada manuais:
- Vaga: Campo para URL e uma Textarea alternativa com placeholder: "Ou cole a descrição completa da vaga aqui".
- Currículo: Área de upload (PDF/DOCX simulado) e botão para colar/editar o texto do currículo estruturado.
- Botão de ação principal: "Analisar Compatibilidade ATS"

## 4. MOTOR ATS LOCAL (CLIENT-SIDE)
Implementar serviço desacoplado em TypeScript (`AtsAnalyzer` e `ResumeOptimizer`) que:
- Extrai palavras-chave e competências da vaga (ex: React, TypeScript, Azure, CI/CD, Docker, Git).
- Compara com as competências e experiências do currículo.
- Calcula o ATS Score de 0 a 100% com base na taxa de correspondência.
- Separa:
  - ✅ Competências Encontradas (badges verdes)
  - ❌ Competências Ausentes (badges vermelhos/alerta)
- Gera recomendações automáticas baseadas em regras (ex: "Docker aparece na vaga mas não no currículo", "Destaque seus projetos com TypeScript").

## 5. GERADOR DE CURRÍCULO OTIMIZADO E COMPARADOR
O sistema deve gerar uma versão otimizada do currículo sem alucinações:
- Prioriza e traz para o topo as competências que batem com a vaga.
- Reordena as experiências e projetos destacando as tecnologias correspondentes.
- Tela de Comparação com abas ou colunas lado a lado:
  - Currículo Original vs. Currículo Otimizado (com diff visual do que foi destacado/reordenado).
- Botão "Exportar": visual limpo ATS-friendly com disparo de impressão para PDF (`window.print()`).

## 6. ASSISTENTE CIVI (CHAT LOCAL)
Um painel de chat lateral com o assistente "Civi":
- Contém perguntas rápidas clicáveis:
  - "Por que meu score ficou em X%?"
  - "Como posso melhorar para essa vaga?"
  - "Quais competências devo priorizar nos meus estudos?"
- Responde com base no resultado da análise calculada localmente.

## 7. ÁREA DE CURRÍCULOS (CLIPES) E DASHBOARD
- Cada análise salva vira um "Clipe" unindo Vaga + Currículo Otimizado com status (Otimizado, Em Análise, Exportado).
- O app deve iniciar com 3 clipes de exemplo já gravados no histórico.
- Dashboard com KPIs: Vagas Analisadas, Média de ATS Score, Currículos Otimizados e Gráfico (Recharts) de competências mais pedidas vs. competências ausentes.
