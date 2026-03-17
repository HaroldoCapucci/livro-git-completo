```markdown'''
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Capítulo 14: Automação com GitHub Actions

**Páginas estimadas:** 30  
**Tempo de leitura:** 80–100 minutos  
**Objetivos do capítulo:**  
- Compreender o conceito de integração contínua (CI) e entrega contínua (CD)  
- Conhecer a estrutura de um workflow no GitHub Actions  
- Criar workflows automatizados para testes, build e deploy  
- Utilizar actions prontas do Marketplace  
- Trabalhar com matrizes (matrix builds) para testar múltiplas versões  
- Gerenciar segredos e variáveis de ambiente com segurança  
- Produzir e consumir artefatos  
- Criar uma action personalizada simples  
- Aplicar na prática com exemplos reais: testes automatizados e geração de PDF do livro  

---

## 14.1 Introdução à Automação e CI/CD

Até agora, você aprendeu a versionar código, colaborar via pull requests e gerenciar projetos. Mas o desenvolvimento moderno vai além: exige automação para garantir qualidade e agilidade. É aqui que entram os conceitos de **Integração Contínua (CI)** e **Entrega Contínua (CD)** .

- **CI (Continuous Integration):** prática de integrar código frequentemente ao repositório principal, executando testes automatizados a cada push, para detectar problemas rapidamente.  
- **CD (Continuous Delivery/Deployment):** extensão da CI que automatiza a entrega do software em ambientes de homologação ou produção.

O **GitHub Actions** é a solução nativa do GitHub para CI/CD. Ele permite criar fluxos de trabalho automatizados diretamente no repositório, baseados em eventos (push, pull request, schedule, etc.). Com ele, você pode:

- Executar testes em múltiplas plataformas e versões de linguagem.  
- Compilar código e gerar artefatos.  
- Fazer deploy automático em servidores ou nuvem.  
- Publicar pacotes em registries (npm, Docker Hub, etc.).  
- E muito mais – tudo gratuito para repositórios públicos e com uma generosa cota para privados.

Neste capítulo, você aprenderá a dominar o GitHub Actions, desde os conceitos básicos até a criação de workflows complexos, com exemplos práticos aplicados ao seu próprio livro.

---

## 14.2 Conceitos Fundamentais

Um workflow no GitHub Actions é definido por um arquivo YAML dentro da pasta `.github/workflows/` do repositório. Vamos entender seus componentes principais .

### 14.2.1 Workflow

É um processo automatizado composto por um ou mais **jobs**. Ele é acionado por um **evento** (ex: push, pull_request, schedule).

### 14.2.2 Evento

É o gatilho que inicia o workflow. Exemplos:
- `push`: quando commits são enviados para o repositório.  
- `pull_request`: quando um PR é aberto, sincronizado ou fechado.  
- `schedule`: agendamento no formato cron.  
- `workflow_dispatch`: execução manual via interface do GitHub.  
- `repository_dispatch`: acionado por API externa.

### 14.2.3 Job

Um job é um conjunto de **steps** executados no mesmo **runner**. Por padrão, jobs são executados em paralelo, mas podem ser configurados para depender de outros jobs.

### 14.2.4 Step

Cada step pode ser um comando shell ou uma **action** (reutilizável). Steps compartilham o mesmo sistema de arquivos (podem gerar artefatos que serão usados por steps posteriores no mesmo job).

### 14.2.5 Runner

É a máquina (virtual ou auto-hospedada) que executa o job. O GitHub fornece runners hospedados com Linux (Ubuntu), Windows e macOS. Você também pode configurar seus próprios runners.

### 14.2.6 Action

São unidades modulares de código reutilizável. Podem ser escritas em JavaScript, TypeScript ou container Docker, e publicadas no **GitHub Marketplace**. Usar actions prontas evita reinventar a roda.

---

## 14.3 Criando Seu Primeiro Workflow

Vamos criar um workflow simples que é executado a cada push e exibe uma mensagem.

### 14.3.1 Estrutura de pastas

No seu repositório, crie a pasta `.github/workflows/` (se não existir). Dentro dela, crie um arquivo `primeiro-workflow.yml`.

### 14.3.2 Conteúdo do arquivo

```yaml
name: Meu Primeiro Workflow

on: [push]  # gatilho: qualquer push

jobs:
  job1:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout do código
        uses: actions/checkout@v4  # action oficial para baixar o repositório

      - name: Executar um script simples
        run: echo "Olá, GitHub Actions!"
```

14.3.3 Explicação

· name: nome opcional do workflow.
· on: define os eventos que disparam o workflow. Neste caso, qualquer push.
· jobs: contém os jobs.
· job1: identificador do job.
· runs-on: tipo de runner (ubuntu-latest).
· steps: lista de passos.
· uses: actions/checkout@v4: action que baixa o repositório para o runner.
· run: executa um comando shell.

14.3.4 Fazendo o push

Após criar o arquivo, faça commit e push para o repositório. Acesse a aba "Actions" do seu repositório no GitHub. Você verá o workflow sendo executado. Clique nele para ver os logs.

14.3.5 Exercício prático 14.1

Crie o workflow acima no seu repositório e observe a execução. Altere o comando echo para listar os arquivos do diretório com ls -la.

---

14.4 Explorando Eventos de Gatilho

O GitHub Actions oferece uma vasta gama de eventos . Vamos explorar os mais úteis.

14.4.1 push e pull_request

```yaml
on:
  push:
    branches: [ main, develop ]   # executa apenas nas branches main e develop
  pull_request:
    branches: [ main ]             # executa quando PR é aberto para main
    types: [opened, synchronize, reopened]  # tipos de atividade
```

14.4.2 schedule (cron)

```yaml
on:
  schedule:
    - cron: '0 2 * * 1'   # toda segunda-feira às 2h UTC
```

O formato cron tem cinco campos: minuto, hora, dia do mês, mês, dia da semana.

14.4.3 workflow_dispatch (manual)

```yaml
on:
  workflow_dispatch:
    inputs:
      environment:
        description: 'Ambiente para deploy'
        required: true
        default: 'homolog'
        type: choice
        options:
          - homolog
          - producao
```

Isso permite executar o workflow manualmente pela interface, passando parâmetros.

14.4.4 repository_dispatch (API)

```yaml
on:
  repository_dispatch:
    types: [deploy-command]
```

Você pode acionar via API REST do GitHub.

14.4.5 Filtros avançados

É possível filtrar por caminhos de arquivo:

```yaml
on:
  push:
    paths:
      - 'src/**'        # executa só se alterar arquivos em src/
      - '!src/legado/**' # exceto a pasta legado
```

14.4.6 Exercício prático 14.2

Crie um workflow que seja executado:

· Em push para a branch main, mas apenas se houver alterações em capitulos/.
· Agendado para toda sexta-feira às 18h.
· Com possibilidade de execução manual recebendo um parâmetro "notificar" (booleano).

Teste cada gatilho (para o agendado, aguarde ou use workflow_dispatch para testar).

---

14.5 Matrix Builds e Estratégias

Uma das funcionalidades mais poderosas é a matrix strategy, que permite executar um job com diferentes combinações de parâmetros (versões de linguagem, sistemas operacionais, etc.) .

14.5.1 Exemplo de matrix simples

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [14, 16, 18]
    steps:
      - uses: actions/checkout@v4
      - name: Usar Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm install
      - run: npm test
```

Esse workflow executa três jobs em paralelo, um para cada versão do Node.js.

14.5.2 Matrix com múltiplas dimensões

```yaml
strategy:
  matrix:
    os: [ubuntu-latest, windows-latest]
    node: [16, 18]
    include:
      - os: ubuntu-latest
        node: 20
    exclude:
      - os: windows-latest
        node: 16
```

· include adiciona uma combinação extra.
· exclude remove combinações indesejadas.

14.5.3 Acessando valores da matrix

Use ${{ matrix.os }}, ${{ matrix.node }} nos steps.

14.5.4 Exercício prático 14.3

Crie um workflow que teste um projeto simples (ex: um script Python) em:

· Ubuntu com Python 3.9 e 3.10.
· Windows com Python 3.9.
  Use actions/setup-python@v5. O teste pode ser apenas python --version e python -c "print('ok')".

---

14.6 Utilizando Actions do Marketplace

O GitHub Marketplace contém milhares de actions prontas para as mais diversas tarefas . Algumas extremamente úteis:

14.6.1 actions/checkout (já usado)

Baixa o código do repositório.

14.6.2 actions/setup-node, setup-python, setup-java, etc.

Configuram a versão da linguagem/ferramenta.

14.6.3 actions/cache

Cacheia dependências (ex: node_modules) para acelerar execuções futuras.

```yaml
- name: Cache do npm
  uses: actions/cache@v4
  with:
    path: ~/.npm
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-node-
```

14.6.4 actions/upload-artifact e actions/download-artifact

Permitem salvar arquivos gerados (logs, builds) e compartilhá-los entre jobs ou disponibilizá-los para download.

14.6.5 actions/github-script

Executa scripts JavaScript com acesso ao contexto do GitHub (API).

14.6.6 softprops/action-gh-release

Cria releases automaticamente a partir de tags.

14.6.7 Encontrando actions

No próprio GitHub, acesse Marketplace (https://github.com/marketplace?type=actions) e pesquise.

14.6.8 Cuidados

· Sempre use a versão específica (ex: @v4) em vez de @main, para evitar mudanças inesperadas.
· Verifique a popularidade e manutenção da action.

14.6.9 Exercício prático 14.4

Crie um workflow que:

· Use actions/checkout.
· Use actions/setup-node para Node 18.
· Instale dependências (npm install).
· Use actions/cache para cachear node_modules.
· Execute um script de teste (mesmo que simples, como echo "testes ok").

---

14.7 Criando uma Action Personalizada

Você pode criar suas próprias actions para reutilização dentro da organização ou publicar no Marketplace . Há três tipos:

14.7.1 Action Docker

Usa um container Docker. Útil quando precisa de um ambiente específico.

14.7.2 Action JavaScript

Escrita em JavaScript (ou TypeScript), executada diretamente no runner (mais rápido).

14.7.3 Action Composta (Composite)

Combina múltiplos steps em uma action reutilizável.

14.7.4 Exemplo: Action composta simples

Crie uma pasta actions/saudacao/ na raiz do repositório. Dentro, um arquivo action.yml:

```yaml
name: "Saudação"
description: "Exibe uma saudação personalizada"
inputs:
  nome:
    description: "Nome da pessoa"
    required: true
    default: "Mundo"
runs:
  using: "composite"
  steps:
    - run: echo "Olá, ${{ inputs.nome }}!"
      shell: bash
```

Para usar essa action em um workflow:

```yaml
steps:
  - name: Checkout
    uses: actions/checkout@v4
  - name: Saudação personalizada
    uses: ./actions/saudacao
    with:
      nome: "Haroldo"
```

14.7.5 Publicando uma action

Para publicar no Marketplace, crie um repositório público com a action e adicione tags de versão. O GitHub detecta automaticamente.

14.7.6 Exercício prático 14.5

Crie uma action composta que receba um nome e exiba uma mensagem de boas-vindas. Em seguida, use-a em um workflow.

---

14.8 Exemplo Prático 1: Testes Automáticos com Node.js

Vamos criar um workflow real para um projeto Node.js com testes.

14.8.1 Estrutura do projeto (simulada)

Suponha um projeto com package.json e script de teste npm test.

14.8.2 Workflow test.yml

```yaml
name: CI - Testes

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [16.x, 18.x, 20.x]

    steps:
      - name: Checkout do código
        uses: actions/checkout@v4

      - name: Cache do npm
        uses: actions/cache@v4
        with:
          path: ~/.npm
          key: ${{ runner.os }}-node-${{ matrix.node-version }}-${{ hashFiles('**/package-lock.json') }}
          restore-keys: |
            ${{ runner.os }}-node-${{ matrix.node-version }}-

      - name: Configurar Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}

      - name: Instalar dependências
        run: npm ci

      - name: Executar testes
        run: npm test

      - name: Upload de logs (se falhar)
        if: failure()
        uses: actions/upload-artifact@v4
        with:
          name: logs-node-${{ matrix.node-version }}
          path: test-results.log
```

14.8.3 Explicação

· npm ci é mais rápido e confiável que npm install em CI.
· Cache armazena ~/.npm para evitar download de pacotes repetido.
· O step de upload só roda se os testes falharem (if: failure()), enviando logs para análise.

14.8.4 Exercício prático 14.6

Crie um projeto Node mínimo (ou use um existente) e implemente esse workflow. Simule um teste que falha e observe o artefato de log.

---

14.9 Exemplo Prático 2: Gerando PDF do Livro Automaticamente

Este exemplo é especialmente útil para você, autor. Vamos automatizar a geração do PDF do livro sempre que uma nova tag de versão for criada.

14.9.1 Pré-requisitos

· O livro está em Markdown, com capítulos na pasta capitulos/.
· Utilizamos Pandoc para gerar PDF (como discutido no início do livro).
· Precisamos de um runner com Pandoc e LaTeX instalados.

14.9.2 Workflow gerar-pdf.yml

```yaml
name: Gerar PDF do Livro

on:
  push:
    tags:
      - 'v*'  # dispara quando uma tag começando com 'v' é criada (ex: v1.0, v2.1)
  workflow_dispatch:  # também permite execução manual

jobs:
  build-pdf:
    runs-on: ubuntu-latest
    container:
      image: pandoc/latex:latest  # container oficial com Pandoc e LaTeX

    steps:
      - name: Checkout do repositório
        uses: actions/checkout@v4

      - name: Gerar PDF com Pandoc
        run: |
          mkdir -p output
          pandoc \
            --from markdown \
            --to pdf \
            --output output/livro.pdf \
            --pdf-engine=xelatex \
            capitulos/cap*.md

      - name: Criar Release
        id: create_release
        uses: softprops/action-gh-release@v2
        with:
          files: output/livro.pdf
          name: Release ${{ github.ref_name }}
          body: |
            PDF gerado automaticamente para a versão ${{ github.ref_name }}.
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

14.9.3 Explicação

· Usamos o container pandoc/latex que já tem tudo instalado.
· O Pandoc converte todos os capítulos (cap*.md) em um único PDF.
· A action softprops/action-gh-release anexa o PDF à release criada.
· ${{ github.ref_name }} é o nome da tag (ex: v1.0).
· secrets.GITHUB_TOKEN é um token automático fornecido pelo GitHub para autenticação.

14.9.4 Como testar

1. Crie uma tag local: git tag -a v0.1 -m "Versão de teste"
2. Envie a tag: git push origin v0.1
3. Acesse a aba Actions e veja o workflow executar.
4. Depois, verifique a aba Releases: deve haver uma release com o PDF anexado.

14.9.5 Exercício prático 14.7

Adapte o workflow acima para o seu repositório do livro. Se ainda não tem um arquivo de template LaTeX personalizado, pode usar o comando simples. Teste com uma tag.

---

14.10 Segredos e Variáveis de Ambiente

Em workflows, é comum precisar de tokens, senhas ou chaves de API. O GitHub fornece segredos criptografados .

14.10.1 Criando segredos

Vá em Settings → Secrets and variables → Actions no seu repositório. Clique em New repository secret. Dê um nome (ex: DOCKER_PASSWORD) e o valor.

14.10.2 Usando segredos no workflow

```yaml
- name: Login no Docker Hub
  run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin
```

Importante: segredos são mascarados nos logs (não aparecem em texto claro).

14.10.3 Variáveis de ambiente comuns

Você também pode definir variáveis de ambiente em nível de workflow, job ou step:

```yaml
env:
  NODE_ENV: production

jobs:
  exemplo:
    runs-on: ubuntu-latest
    env:
      API_URL: https://api.exemplo.com
    steps:
      - run: echo $API_URL
        env:
          TOKEN: ${{ secrets.TOKEN }}
```

14.10.4 Contexto github

O GitHub disponibiliza várias informações no contexto github, como:

· github.repository: nome do repositório
· github.ref: referência (branch/tag)
· github.event_name: nome do evento
· github.sha: hash do commit

14.10.5 Exercício prático 14.8

Crie um segredo chamado MEU_SEGREDO com um valor qualquer. Em um workflow, use echo ${{ secrets.MEU_SEGREDO }} e veja que ele aparece como *** nos logs. Tente também usar em uma variável de ambiente.

---

14.11 Artefatos e Caching

14.11.1 Artefatos

Artefatos são arquivos gerados durante o workflow que podem ser armazenados e baixados posteriormente. Por exemplo, binários compilados, logs, relatórios de teste.

· Upload: actions/upload-artifact@v4
· Download: actions/download-artifact@v4

Exemplo de upload:

```yaml
- name: Upload artefato
  uses: actions/upload-artifact@v4
  with:
    name: meu-artefato
    path: dist/
```

Artefatos podem ser baixados pela interface do GitHub ou por outro job.

14.11.2 Caching

O cache armazena dependências ou pastas para acelerar execuções futuras. Exemplo com npm:

```yaml
- name: Cache node_modules
  uses: actions/cache@v4
  with:
    path: node_modules
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
```

A chave (key) deve ser única para cada conjunto de dependências; hashFiles gera um hash do arquivo lock.

14.11.3 Diferença entre artefato e cache

· Cache: para acelerar execuções (dependências, compilações intermediárias).
· Artefato: para preservar resultados finais (relatórios, builds).

14.11.4 Exercício prático 14.9

Crie um workflow que:

· Gere um arquivo de log com date > log.txt.
· Faça upload desse arquivo como artefato.
· Em outro job, baixe o artefato e exiba seu conteúdo.

---

14.12 Boas Práticas e Segurança

14.12.1 Versionamento de actions

Sempre fixe a versão das actions (ex: @v4) em vez de @main ou @master, para evitar surpresas com mudanças.

14.12.2 Mínimo privilégio

Use permissões restritas nos workflows. Por padrão, o GITHUB_TOKEN tem permissões limitadas, mas você pode refiná-las:

```yaml
permissions:
  contents: read
  pull-requests: write
```

14.12.3 Evitar segredos em logs

Nunca faça echo de segredos diretamente. Use ${{ secrets.NOME }} apenas onde necessário.

14.12.4 Reutilização de workflows

Para evitar repetição, você pode usar workflows reutilizáveis (chamados por outros workflows) ou templates.

14.12.5 Monitoramento

A aba Actions mostra o histórico de execuções. Configure alertas para falhas (por e-mail ou Slack) usando actions de notificação.

14.12.6 Exercício prático 14.10

Revise um workflow seu e adicione permissões explícitas mínimas. Pesquise sobre workflow_call e tente criar um workflow reutilizável simples.

---

14.13 Integração com VS Code

O VS Code oferece extensões que facilitam o desenvolvimento de workflows.

14.13.1 Extensão "GitHub Actions"

· Nome: GitHub Actions (por GitHub)
· Funcionalidades:
  · Visualizar workflows e suas execuções diretamente no editor.
  · Editar arquivos YAML com syntax highlighting e validação.
  · Acionar workflows manualmente.

14.13.2 Extensão "YAML" (Red Hat)

Fornece validação de esquema para arquivos YAML, incluindo autocompletar para GitHub Actions (baseado no esquema oficial).

14.13.3 Criando workflows no VS Code

Com as extensões instaladas, crie um arquivo .github/workflows/novo.yml. O VS Code oferece snippets e validação em tempo real.

14.13.4 Depuração local

Embora não seja possível executar workflows localmente, você pode usar a ferramenta act (https://github.com/nektos/act) para testar workflows em container localmente, simulando o GitHub Actions.

14.13.5 Exercício prático 14.11

Instale as extensões mencionadas e crie um novo workflow diretamente no VS Code. Use os snippets para preencher a estrutura.

---

14.14 Exercícios de Fixação

1. O que é um workflow no GitHub Actions?
2. Quais são os principais eventos que podem disparar um workflow?
3. Como você limita um workflow para executar apenas em pushes para a branch main e em pull requests para main?
4. Explique o que é uma matrix strategy e dê um exemplo.
5. Qual a diferença entre actions/cache e actions/upload-artifact?
6. Como você armazena um token de acesso com segurança em um workflow?
7. Descreva um workflow que gere um PDF a partir de arquivos Markdown e o anexe a uma release.
8. Qual action você usaria para configurar o Node.js em uma versão específica?
9. Como você define uma variável de ambiente em nível de job?
10. (Desafio) Crie um workflow que, ao ser executado manualmente (workflow_dispatch), aceite um parâmetro "linguagem" e execute testes em Node.js ou Python conforme o valor escolhido. Use uma matrix condicional.

---

14.15 Resumo do Capítulo

· GitHub Actions permite automatizar tarefas de CI/CD diretamente no repositório.
· Workflows são definidos em YAML na pasta .github/workflows/.
· Eventos como push, pull_request, schedule e workflow_dispatch disparam os workflows.
· Jobs agrupam steps, que podem ser comandos ou actions reutilizáveis.
· Matrix strategy executa jobs em múltiplas combinações de parâmetros.
· O Marketplace oferece milhares de actions prontas.
· Podemos criar nossas próprias actions (compostas, Docker, JavaScript).
· Segredos e variáveis de ambiente protegem informações sensíveis.
· Artefatos e cache otimizam e preservam resultados.
· Boas práticas incluem versionar actions, definir permissões mínimas e evitar expor segredos.
· O VS Code possui extensões que auxiliam na criação e visualização de workflows.

Agora você pode automatizar praticamente qualquer tarefa do seu projeto diretamente no GitHub. No próximo capítulo, colocaremos tudo em prática com um projeto real: gerenciar um TCC usando Git.

---

14.16 Referências

· GitHub Docs: "Understanding GitHub Actions"
· GitHub Docs: "Workflow syntax for GitHub Actions"
· GitHub Marketplace: https://github.com/marketplace?type=actions
· "act" – Run GitHub Actions locally: https://github.com/nektos/act
· Blog do GitHub: "GitHub Actions: agora com execução manual e mais"
· Documentação das actions oficiais (actions/checkout, actions/setup-node, etc.)

```
