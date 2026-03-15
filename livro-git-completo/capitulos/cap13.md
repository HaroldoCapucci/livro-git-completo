```markdown
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Capítulo 13: Desenvolvimento com GitHub Copilot e IA

**Páginas estimadas:** 28  
**Tempo de leitura:** 70–90 minutos  
**Objetivos do capítulo:**  
- Compreender o que é GitHub Copilot e como ele funciona  
- Instalar e configurar o Copilot no VS Code  
- Dominar as sugestões de código inline (autocomplete)  
- Utilizar o Copilot Chat para interações naturais  
- Explorar comandos como /doc, /explain, /fix, /tests  
- Aprender a usar o @workspace para consultar todo o projeto  
- Conhecer o Agent Mode para tarefas autônomas  
- Adotar boas práticas e evitar armadilhas comuns  
- Integrar o Copilot ao fluxo de desenvolvimento com Git  

---

## 13.1 Introdução

A inteligência artificial está transformando a maneira como desenvolvemos software. O **GitHub Copilot**, criado pela GitHub em parceria com a OpenAI, é um assistente de programação baseado em IA que funciona diretamente dentro do seu editor. Ele não é um simples autocomplete: entende o contexto do seu código, suas intenções expressas em comentários e até mesmo conversas em linguagem natural, gerando desde trechos simples até funções completas, testes e documentação .

Neste capítulo, você aprenderá a usar o Copilot como um verdadeiro "par de programação" (pair programmer) . Veremos como instalá-lo, configurá-lo e, principalmente, como se comunicar com ele para extrair o máximo de produtividade, sempre com olhar crítico sobre o código gerado.

---

## 13.2 O que é GitHub Copilot?

### 13.2.1 Definição

GitHub Copilot é um serviço de IA que sugere código e funções inteiras em tempo real, diretamente no seu editor . Ele foi treinado em bilhões de linhas de código público de repositórios GitHub, abrangendo centenas de linguagens e frameworks .

### 13.2.2 Como funciona?

O Copilot analisa o contexto do seu projeto:
- O arquivo que você está editando
- Outros arquivos abertos no editor
- Comentários escritos em linguagem natural
- Nomes de funções e variáveis
- Estrutura do projeto

Com base nesse contexto, ele utiliza modelos de linguagem avançados para prever e sugerir o próximo trecho de código .

### 13.2.3 Planos e pré-requisitos

Para usar o Copilot, você precisa :
- Uma conta no GitHub
- Uma assinatura ativa (há plano Free com limitações mensais, ou trial de 30 dias)
- VS Code instalado
- Conexão estável com a internet (as sugestões são processadas na nuvem)

**Nota:** Organizações podem gerenciar assinaturas para equipes. Verifique com seu administrador se estiver em ambiente corporativo .

---

## 13.3 Instalação e Configuração

### 13.3.1 Instalando a extensão

1. Abra o VS Code.
2. Acesse a guia de Extensões (`Ctrl+Shift+X` ou `Cmd+Shift+X` no Mac).
3. Pesquise por "GitHub Copilot".
4. Escolha a extensão oficial (publicada por GitHub) e clique em **Install** .

Recomenda-se instalar também a extensão **GitHub Copilot Chat**, que adiciona a interface de conversa (embora versões recentes já incluam ambas em um único pacote) .

### 13.3.2 Autenticando

Após a instalação:
1. Um ícone do Copilot aparecerá na barra de status (canto inferior direito).
2. Clique no ícone ou aguarde a notificação para fazer login.
3. Siga o fluxo OAuth no navegador, autorizando o acesso à sua conta GitHub .
4. Após autorizar, volte ao VS Code – a autenticação estará completa.

Se precisar forçar o login: abra a Paleta de Comandos (`Ctrl+Shift+P`) e procure por "GitHub Copilot: Sign In" .

### 13.3.3 Verificando a ativação

- O ícone na barra de status deve mostrar "Copilot: Ready" (sem nenhum aviso).
- Abra um arquivo de código e comece a digitar. Sugestões em "cinza fantasma" (ghost text) devem aparecer .

### 13.3.4 Configurações iniciais recomendadas

Acesse as configurações do VS Code (`Ctrl+,`) e pesquise por "Copilot". Alguns ajustes úteis :

- `github.copilot.enable`: ativar/desativar para linguagens específicas.
- `editor.inlineSuggest.enabled`: manter ativado para ver sugestões inline.
- `github.copilot.editor.enableAutoCompletions`: controla se as sugestões aparecem automaticamente.
- `github.copilot.advanced`: permite ajustar delay de sugestões, útil em projetos grandes para evitar "ruído".

---

## 13.4 Sugestões Inline: O Coração do Copilot

### 13.4.1 Como aparecem as sugestões

Enquanto você digita, o Copilot exibe sugestões em texto cinza (ghost text) à frente do cursor . Elas podem ser:
- Uma única linha
- Múltiplas linhas (funções inteiras)
- Blocos de código (loops, condicionais, etc.)

### 13.4.2 Aceitando sugestões

- **Tab**: aceita a sugestão completa .
- **Ctrl+→** (Cmd+→ no Mac): aceita palavra por palavra .

### 13.4.3 Navegando entre alternativas

Se a primeira sugestão não for ideal, o Copilot geralmente tem outras opções :

- **Alt+] (Option+] no Mac)**: próxima sugestão.
- **Alt+[ (Option+[ no Mac)**: sugestão anterior.

### 13.4.4 Rejeitando ou ignorando

- **Esc**: descarta a sugestão atual.
- Simplesmente continue digitando; a sugestão desaparecerá e o Copilot tentará se adaptar ao que você escreve .

### 13.4.5 Forçando uma sugestão

Se nada aparecer e você quiser uma sugestão, use `Alt+\` (Option+\ no Mac) para acionar manualmente .

### 13.4.6 Exercício prático 13.1

1. Crie um arquivo `calculadora.js`.
2. Digite o comentário: `// Função que soma dois números`.
3. Observe a sugestão automática. Aceite com Tab.
4. Experimente navegar por alternativas com Alt+] e Alt+[.
5. Crie um arquivo `index.html` e digite `!` (ponto de exclamação) – o Copilot pode sugerir a estrutura básica do HTML5.

---

## 13.5 Trabalhando com Comentários Inteligentes

Uma das técnicas mais poderosas para guiar o Copilot é usar comentários descritivos .

### 13.5.1 Escrevendo intenções claras

Quanto mais específico o comentário, melhor a sugestão.

**Exemplo vago:**
```javascript
// processar dados
```

Exemplo eficaz:

```javascript
// Recebe um array de números, filtra apenas os pares e retorna a soma deles
```

O Copilot frequentemente gera o código completo para essa descrição .

13.5.2 Especificando entradas e saídas

```javascript
// Função que valida e-mail: retorna true se o formato for válido, false caso contrário
```

13.5.3 Descrevendo algoritmos

```javascript
// Ordena uma lista de objetos por data de criação, do mais recente para o mais antigo
```

13.5.4 Exercício prático 13.2

Crie um arquivo desafio.js e escreva comentários detalhados para:

· Uma função que calcula fatorial.
· Uma função que valida CPF (apenas a lógica, mesmo que simplificada).
· Uma função que busca dados de uma API e trata erros.

Observe como o Copilot reage a cada nível de detalhe.

---

13.6 Copilot Chat: Conversando com o Assistente

O Copilot Chat traz uma interface de conversa para dentro do VS Code, permitindo diálogos mais complexos .

13.6.1 Abrindo o Chat

· Atalho: Ctrl+Alt+I (Windows/Linux) ou Cmd+Option+I (Mac) .
· Ícone: Clique no ícone do Copilot na barra lateral (se disponível).
· Paleta de comandos: "Copilot Chat: Open Chat" .

13.6.2 Funcionalidades do Chat

Você pode fazer perguntas como :

· "Explique esta função:" (selecione o código antes)
· "Como faço para implementar autenticação JWT em Node.js?"
· "Encontre bugs neste trecho"
· "Sugira melhorias de performance"
· "Gere testes unitários para esta classe"

13.6.3 Comandos Especiais (Slash Commands)

No chat, você pode usar "/" seguido de comandos que direcionam a ação :

Comando Função
/doc Gera documentação/comentários para o código selecionado
/explain Explica o código selecionado linha a linha
/fix Tenta corrigir problemas no código
/tests Gera testes unitários
/optimize Sugere otimizações de performance

13.6.4 Variáveis de Contexto

Use # para incluir contexto específico :

· #selection: o código que você selecionou.
· #file: o arquivo atual.
· #editor: o editor atual.
· #codebase: todo o projeto (pode ser pesado).

13.6.5 Exercício prático 13.3

1. Escreva uma função simples com um bug proposital (ex: loop infinito ou condição errada).
2. Selecione a função.
3. No chat, use o comando /explain e veja a explicação.
4. Depois use /fix e veja a sugestão de correção.
5. Use /tests para gerar testes para a mesma função (após corrigida).

---

13.7 @workspace: Seu Projeto como Contexto

O participante @workspace é uma funcionalidade poderosa que permite ao Copilot entender todo o seu projeto .

13.7.1 O que faz?

Ao usar @workspace, o Copilot analisa:

· Todos os arquivos do workspace (respeitando .gitignore)
· Estrutura de diretórios
· Símbolos e definições
· Dependências

13.7.2 Exemplos de uso

· @workspace Onde está definida a constante de conexão com o banco?
· @workspace Como a autenticação é implementada atualmente?
· @workspace Quais arquivos dependem deste serviço?
· @workspace Mapeie todas as rotas da API e aponte as que não têm tratamento de erro

13.7.3 Aplicação prática

Em um projeto médio (ex: 30k linhas), @workspace pode responder em segundos, indicando arquivos e trechos relevantes .

13.7.4 Exercício prático 13.4

Se você tiver um projeto existente (pode ser o repositório do seu livro), abra-o no VS Code e experimente:

1. @workspace Quantos capítulos já foram escritos? (ele listará os arquivos cap*.md).
2. @workspace Qual a estrutura de pastas do projeto?
3. @workspace Onde eu uso a palavra 'rebase'? (busca contextual).

---

13.8 Agent Mode: Autonomia para Tarefas Complexas

O Agent Mode (modo agente) leva a automação a outro nível: o Copilot pode executar tarefas que envolvem múltiplos arquivos e etapas, de forma planejada .

13.8.1 Como ativar

No chat, selecione o modo "Agent" no menu suspenso (ao lado do campo de texto) .

13.8.2 Exemplo prático

Peça algo como:

"Crie um componente React de formulário de login com validação de campos e integração com uma API mock. Gere os arquivos necessários e organize na pasta src/components."

O agente:

· Analisa a estrutura do projeto
· Cria os arquivos (ex: LoginForm.jsx, LoginForm.css, api.js)
· Escreve o código completo
· Exibe um diff para você aceitar ou rejeitar cada alteração .

13.8.3 Cuidados com o Agent Mode

· Sem revise as alterações antes de aceitar.
· Em projetos grandes, defina bem o escopo para evitar mudanças indesejadas.
· Use com versionamento ativo (Git) para poder reverter se necessário.

13.8.4 Exercício prático 13.5

Em um projeto novo (pasta vazia), ative o Agent Mode e peça:

"Crie uma página HTML simples com um contador de cliques, usando CSS moderno e JavaScript separado. Coloque todos os arquivos na raiz."

Observe quantos arquivos são criados e como o agente organiza a solução.

---

13.9 Copilot e Testes: TDD Acelerado

O Copilot é excelente para gerar testes unitários, seja seguindo TDD ou cobrindo código existente .

13.9.1 Gerando testes para código existente

Selecione uma função e no chat use /tests. O Copilot gerará testes com base no contexto (framework que você costuma usar, estilo do projeto).

13.9.2 TDD com Copilot

1. Escreva o teste primeiro (descrevendo o comportamento esperado).
2. O Copilot pode sugerir a implementação que faz o teste passar.

Exemplo:

```javascript
// Teste para função de soma
test('soma 1 + 2 e retorna 3', () => {
  expect(soma(1, 2)).toBe(3);
});
```

Ao começar a escrever a função soma, o Copilot entenderá o contexto do teste e sugerirá a implementação.

13.9.3 Exercício prático 13.6

1. Escreva um teste para uma função que ainda não existe (ex: multiplicar(a, b)).
2. Veja se o Copilot sugere a implementação.
3. Aceite e execute o teste (se tiver Jest configurado, por exemplo).

---

13.10 Copilot para Documentação e Commits

13.10.1 Gerando documentação

Use /doc no chat sobre um trecho de código para gerar comentários estilo JSDoc, docstrings Python, etc. .

13.10.2 Gerando mensagens de commit

No VS Code, ao abrir o Source Control, você verá um ícone de "estrela" (✨) ao lado do campo de mensagem de commit . Clique para que o Copilot gere uma mensagem descritiva baseada nas alterações feitas.

Isso segue as boas práticas de Conventional Commits, poupando tempo e mantendo consistência .

13.10.3 Exercício prático 13.7

1. Faça uma alteração simples em um arquivo.
2. No Source Control, clique no ícone ✨ ao lado da mensagem de commit.
3. Veja a sugestão gerada. Aceite ou refine.
4. Commit.

---

13.11 Boas Práticas e Armadilhas Comuns

13.11.1 O que fazer (do's)

· Escreva comentários claros: seja específico sobre o que deseja .
· Revise o código gerado: o Copilot não é infalível. Sempre leia e entenda antes de confiar .
· Use testes: valide com testes automatizados o código sugerido .
· Forneça exemplos: se você tem um padrão de código, mostre alguns exemplos para o Copilot aprender .
· Mantenha arquivos relevantes abertos: o Copilot usa o contexto dos arquivos abertos para sugerir melhor .

13.11.2 O que evitar (don'ts)

· Não aceite cegamente: sugestões podem conter bugs, vulnerabilidades ou más práticas .
· Não compartilhe segredos: nunca coloque senhas, tokens ou chaves em prompts ou código que será enviado .
· Cuidado com dependências fantasmas: o Copilot pode sugerir APIs ou bibliotecas que não existem ou estão desatualizadas .
· Evite confiar em código de segurança crítico sem revisão profunda: especialmente criptografia, autenticação, etc.

13.11.3 Privacidade e dados

· O Copilot envia trechos de código para processamento na nuvem.
· Consulte a política da sua organização sobre uso de IA.
· Você pode desativar a coleta de telemetria nas configurações do VS Code .

13.11.4 Quando desligar o Copilot

Em projetos sensíveis ou quando estiver aprendendo um conceito do zero, pode ser útil desabilitar temporariamente para não "pular etapas" e garantir o entendimento.

---

13.12 Personalizando o Copilot

13.12.1 Instruções personalizadas (custom instructions)

Você pode criar um arquivo .github/copilot-instructions.md na raiz do projeto para dar diretrizes globais ao Copilot .

Exemplo:

```markdown
# Instruções para o Copilot

- Use async/await em vez de Promises .then()
- Prefira funções puras sempre que possível
- Siga o estilo do Prettier configurado
- Comente em português (ou inglês, conforme o projeto)
```

13.12.2 Modos de chat personalizados

Crie arquivos em .github/chatmodes/ para definir comportamentos específicos, como "revisor de código", "especialista em segurança", etc. .

13.12.3 Desativando para linguagens específicas

Nas configurações, use github.copilot.enable e defina como false para linguagens onde não deseja sugestões (ex: Markdown, se preferir escrever sem interferência).

---

13.13 Fluxo de Trabalho Integrado com Git

13.13.1 Copilot durante code reviews

Use o Copilot para ajudar a revisar código de Pull Requests (com extensões apropriadas) ou para explicar código de outros colaboradores .

13.13.2 Gerando mensagens de commit (já visto)

13.13.3 Documentando mudanças

Após implementar uma feature, use /doc para gerar documentação que pode ser incluída no README ou wiki.

13.13.4 Escrevendo guias de contribuição

Peça ao Copilot para esboçar um CONTRIBUTING.md com base na estrutura do projeto.

---

13.14 Exercícios de Fixação

1. Quais são os pré-requisitos para usar GitHub Copilot no VS Code?
2. Como você aceita uma sugestão inline? E como vê sugestões alternativas?
3. Qual a diferença entre usar /explain no chat e simplesmente ler o código?
4. O que faz o comando @workspace? Dê um exemplo de uso prático.
5. Em que cenário o Agent Mode é mais útil?
6. Como você pode gerar uma mensagem de commit automaticamente com Copilot?
7. Cite duas boas práticas ao usar código gerado por IA.
8. Como você configuraria o Copilot para NÃO sugerir em arquivos Markdown?
9. O que é um "slash command" no Copilot Chat? Dê três exemplos.
10. (Desafio) Em um projeto pessoal, crie um arquivo de instruções personalizadas e veja se o Copilot respeita as diretrizes ao gerar novos trechos.

---

13.15 Resumo do Capítulo

· GitHub Copilot é um assistente de IA que sugere código em tempo real, baseado no contexto do projeto.
· A instalação é simples: extensão + autenticação com conta GitHub.
· Sugestões inline aparecem como "ghost text"; aceite com Tab, navegue com Alt+]/[.
· Copilot Chat permite conversas, explicações, correções e geração de testes.
· @workspace contextualiza todo o projeto; Agent Mode executa tarefas complexas multiarquivo.
· Comandos como /doc, /explain, /fix agilizam tarefas comuns.
· O Copilot ajuda em commits, documentação e até code review.
· É essencial revisar o código gerado, manter boas práticas de segurança e personalizar o comportamento quando necessário.

Agora você tem um "par de programação" disponível 24/7. No próximo capítulo, exploraremos automação com GitHub Actions, integrando CI/CD aos seus projetos.

---

13.16 Referências

· Microsoft Learn: "Develop code features using GitHub Copilot Tools" 
· CODE Magazine: "Unleashing the Power of GitHub Copilot in Visual Studio Code" 
· PacificTech: "Copilot怎么用vscode" 
· Skywork.ai: "GitHub Copilot in VS Code: Complete Integration Guide" 
· Perficient Blogs: "Mastering GitHub Copilot in VS Code" e "Using GitHub Copilot in VS Code" 
· ClickUp: "How to Use GitHub Copilot with VS Code (2026 Guide)" 
· Tencent Cloud: "VS Code Copilot 完整使用教程（含图解）" 
· Xebia: "How to Use GitHub Copilot: The Complete Beginner's Guide" 

```
