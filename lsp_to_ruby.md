## LSP para Ruby: Aumente sua Produtividade e Qualidade de Código (com ajuda de IA)

Ao longo dos anos, a busca por código de qualidade e produtividade impulsionou o desenvolvimento de técnicas e ferramentas. Entre elas, os Servidores de Linguagem (Language Servers) Protocol (LSP) se destacam como soluções poderosas que podem transformar a maneira como você desenvolve e mantém seu código.

O LSP oferece autocompletação inteligente e análise de código em tempo real, facilitando a escrita e compreensão do código. Com ele, você navega facilmente pelo código, acessando definições de variáveis, funções e classes com apenas alguns cliques. O LSP também permite refatorar código de forma segura e eficiente, garantindo que as alterações sejam feitas em todo o projeto de forma consistente. Além disso, o LSP é compatível com diversas linguagens de programação, como Ruby, Python, Java, C++, JavaScript e muito mais.

Imagine que você está trabalhando em um grande projeto Ruby e precisa renomear uma variável global. Com o LSP, todas as referências à variável no projeto serão atualizadas automaticamente, evitando erros e economizando tempo.

---

### O que é LSP

- LSP (Language Server Protocol) é um protocolo de comunicação entre um editor de código e um servidor que fornece análises avançadas para uma linguagem específica. Ele permite que editores como Visual Studio Code, Sublime Text, Vim, entre outros, ofereçam funcionalidades avançadas de desenvolvimento, como autocompletar, verificação de erros, navegação de código e refatoração, independentemente da linguagem de programação utilizada.

- O LSP foi inicialmente desenvolvido em 2016 pela Microsoft, com a implementação do protocolo em seu popular editor Visual Studio Code. Após seu lançamento, o LSP foi rapidamente adotado por outras empresas, comunidades de código aberto e IDEs populares, como Eclipse e IntelliJ IDEA. Isso ocorreu devido aos benefícios de reduzir a complexidade no desenvolvimento de suporte a novas linguagens e melhorar a consistência e desempenho das ferramentas de edição.

Adotar LSP não é apenas uma questão de adicionar mais uma ferramenta ao seu fluxo de trabalho, mas sim de elevar o padrão do seu desenvolvimento de software. Ao utilizar as capacidades avançadas dos Servidores de Linguagem, você está investindo na qualidade do seu código, na sua própria produtividade e na satisfação geral do desenvolvimento.

No contexto da linguagem Ruby, um Ruby LSP é um servidor que entende o código Ruby e fornece essas funcionalidades aos editores que suportam o protocolo LSP. Isso significa que, ao usar um editor que suporta LSP, como VS Code, Sublime Text ou Vim, você pode obter suporte aprimorado para desenvolvimento em Ruby, com funcionalidades como:

- Autocompletar: Sugestões de código enquanto você digita.
- Navegação: Habilidade de pular para a definição de classes, métodos ou variáveis.
- Linting: Análise estática do código para detectar erros ou problemas de estilo.
- Formatação: Reformatar automaticamente o código de acordo com padrões definidos.
- Refatoração: Ferramentas para modificar e melhorar o código de maneira sistemática.

Existem várias implementações do Ruby LSP, cada uma com suas características específicas e níveis de suporte para diferentes funcionalidades do protocolo. Por exemplo, algumas implementações populares são:

- **Solargraph**: Implementa o LSP para Ruby, oferecendo recursos como autocompletar, navegação de código, diagnósticos, formatação, entre outros.
- **Steep**: Implementa o LSP para Ruby, mas com um foco específico em tipagem estática.
- **Sorbet**: Implementa o LSP para Ruby, focado principalmente em tipagem estática avançada e análise de tipos.

---

### OBS:

- Ruby LSP (Shopify): Esta é uma extensão para o Visual Studio Code que utiliza o Solargraph como servidor LSP para fornecer recursos avançados de linguagem para Ruby dentro do ambiente do VS Code. A Shopify desenvolveu o Ruby LSP para otimizar e melhorar o desenvolvimento de suas próprias aplicações Ruby/Ruby on Rails.

## Escolhendo o Ruby-Lsp da Shopify

No mundo dinâmico do desenvolvimento para a linguagem Ruby e o framework Ruby on Rails, escolher as ferramentas certas pode fazer toda a diferença na sua produtividade e na qualidade do seu código.

Entre as diversas opções de servidores LSP para a linguagem Ruby, como Solargraph, Steep e Sorbet; eu adotei o Ruby LSP da Shopify. Apesar de não ser um servidor LSP oficial, no momento (junho/2024) e o mais utilizado pela comunidade Ruby, ele oferece muitos dos mesmos benefícios e recursos, com integração profunda com **Ruby** e **Ruby on Rails**, suporte a recursos avançados como diagnósticos em tempo real e formatação automática, e é otimizado para produtividade. Além disso, sua configuração é simples e ele se integra perfeitamente ao VSCode, permitindo um fluxo de trabalho eficiente e alinhado com as melhores práticas de codificação.

## Como instalar o ruby-lsp

Para instalar e configurar o Ruby LSP (Language Server Protocol) da Shopify no seu ambiente de desenvolvimento, siga os passos abaixo. Esses passos incluem a instalação do Ruby LSP, configuração do VSCode e ajustes necessários no seu projeto **Ruby on Rails** ou **Ruby**.

#### Passo 1: Instalar o Ruby LSP

Primeiro, você precisa adicionar o Ruby LSP como uma dependência no seu projeto. Para fazer isso, adicione a gem ruby-lsp ao seu Gemfile:

```ruby
### Gemfile

group :development do
  gem 'ruby-lsp'
end
```

Em seguida, execute `bundle install` para instalar a gem:

```sh
bundle install
```

#### Passo 2: Configurar o VSCode

Para configurar o VSCode para usar o Ruby LSP, siga os passos abaixo:

- Instale a extensão Ruby LSP para VSCode:

  - Abra o VSCode.
  - Vá para a aba de extensões (Ctrl+Shift+X ou Cmd+Shift+X).
  - Procure por "Ruby LSP" e instale a extensão desenvolvida pela Shopify.

- Configure o VSCode:
  - Abra o arquivo de configurações do VSCode (settings.json). Você pode acessar esse arquivo pressionando Ctrl+Shift+P ou Cmd+Shift+P e digitando "Preferences: Open Settings (JSON)".
  - Adicione ou ajuste as seguintes configurações no seu settings.json para habilitar e configurar o Ruby LSP (sempre que modificar o settings.json, reinicie o VSCode):

```json
{
  "rubyLsp.enabled": true,
  "rubyLsp.features": {
    "documentSymbols": true,
    "documentFormatting": true,
    "diagnostics": true,
    "hover": true,
    "completion": true,
    "codeActions": true,
    "codeLens": true,
    "definition": true,
    "documentHighlight": true,
    "documentLink": true,
    "foldingRange": true,
    "references": true,
    "rename": true,
    "selectionRange": true,
    "signatureHelp": true,
    "workspaceSymbol": true
  },
  "rubyLsp.rubyExecutablePath": "/path/to/your/ruby", // Ajuste esse caminho para o executável Ruby no seu sistema
  "rubyLsp.useBundler": true, // Configure para usar o Bundler
  "rubyLsp.formatter": "auto", // Ou "rubocop" se você quiser usar o RuboCop para formatação
  "rubyLsp.lspServer.enabled": true
}
```

#### Passo 3: Configurar o RuboCop (Opcional)

Se você estiver usando o RuboCop para linting e formatação, crie um arquivo `.rubocop.yml` na raiz do seu projeto e configure-o conforme suas necessidades. Certifique-se de que o Ruby LSP e o Solargraph (se instalado) estão configurados para usar o mesmo arquivo de configuração do RuboCop para evitar conflitos.

#### Passo 4: Verifique a Instalação

Abra um arquivo Ruby ou **Ruby on Rails** no seu projeto e verifique se as funcionalidades do Ruby LSP estão funcionando. Você deve ver sugestões de autocompletar, diagnósticos em tempo real e outras funcionalidades fornecidas pelo servidor de linguagem.

### Extensões recomendáveis para o Visual Studio Code (VS Code)

Extensões que funcionam bem junto com um servidor Ruby LSP, ajudando a melhorar a produtividade e a qualidade do código Ruby. Aqui estão algumas delas:

- **Ruby**:

  - Ruby (Shopify): Esta extensão oferece suporte básico para Ruby, incluindo destaque de sintaxe e snippets de código. É uma boa base para trabalhar junto com um servidor LSP como Solargraph.

- **Ruby on Rails**:

  - Rails (Hridoy): Oferece snippets e suporte básico para o desenvolvimento em Ruby on Rails, facilitando a escrita de código Rails.

- **Rubocop**:
  - ruby-rubocop: Integra o RuboCop com o VS Code, fornecendo linting e auto-correção de estilo de código.

### Verificando se o Ruby LSP da Shopify está Funcionando:

1. **Verificação de Diagnósticos e Erros**:

   - Abra um arquivo Ruby no VS Code que tenha potenciais problemas, como erros de sintaxe ou variáveis não definidas.
   - O Ruby LSP da Shopify deve sublinhar visualmente esses problemas no código com linhas vermelhas ou laranjas.
   - Você também pode ver mensagens de erro ou avisos na área de problemas do VS Code (ícone de balão de diálogo na barra lateral esquerda).

2. **Autocompletar e Intellisense**:

   - Comece a digitar código Ruby em um arquivo.
   - O Ruby LSP deve oferecer sugestões de autocompletar com métodos, variáveis, classes e outros símbolos relevantes à medida que você digita.

3. **Hover para Informações**:

   - Passe o mouse sobre um método, classe ou variável para ver informações detalhadas sobre eles.
   - Isso geralmente inclui a definição, parâmetros e possíveis tipos de retorno.

4. **Navegação para Definição**:

   - Clique com o botão direito do mouse em um método, classe ou variável e selecione "Go to Definition" (Ir para a Definição).
   - O VS Code deve navegar para a declaração ou definição desse símbolo no código.

5. **Formatação de Código**:

   - Tente usar a formatação automática de código (geralmente com Shift + Alt + F no VS Code).
   - O Ruby LSP deve aplicar as regras de formatação corretas conforme configurado (como as regras do RuboCop).

6. **Renomear Símbolos**:
   - Selecione um símbolo (método, classe, variável) e use a opção de renomear (geralmente com F2 no VS Code).
   - O VS Code deve aplicar a alteração em todos os lugares onde o símbolo é utilizado, garantindo a consistência.

---

### Para saber mais

- [Documentação do LSP Ruby](https://github.com/Shopify/ruby-lsp)
- [Diretrizes de Contribuição do LSP Ruby](https://github.com/Shopify/ruby-lsp)
- [Repositório LSP Ruby no GitHub](https://github.com/Shopify/ruby-lsp/issues)
- [Comunidade LSP Ruby no Slack](https://github.com/Shopify/ruby-lsp/blob/main/README.md)

---

### Contribua para o LSP Ruby e torne a comunidade ainda mais forte!

1. **Relate bugs e sugestões**: Encontre problemas no LSP Ruby? Envie um relatório no GitHub para ajudar a melhorar a ferramenta.
2. **Traduza documentação**: Ajude a tornar o LSP Ruby acessível a mais pessoas traduzindo a documentação para o seu idioma nativo.
3. **Crie tutoriais e guias**: Compartilhe seu conhecimento com outros desenvolvedores criando tutoriais e guias sobre como usar o LSP Ruby.
4. **Participe da comunidade**: Junte-se à comunidade LSP Ruby no Discord e participe de discussões, faça perguntas e colabore com outros desenvolvedores.
5. **Contribua com código**: Se você tiver habilidades de programação, você pode contribuir diretamente para o código do LSP Ruby no GitHub.

Lembre-se: qualquer contribuição, grande ou pequena, é valiosa para o projeto LSP Ruby. Seja um agente de mudança e ajude a tornar o desenvolvimento Ruby ainda melhor!

---

### As extensões que eu tenho instaladas no VSCode:

    alexcvzz.vscode-sqlite
    aliariff.vscode-erb-beautify
    anbuselvanrocky.bootstrap5-vscode
    bradlc.vscode-tailwindcss
    bung87.rails
    bung87.vscode-gemfile
    christian-kohler.path-intellisense
    dbaeumer.vscode-eslint
    dracula-theme.theme-dracula
    esbenp.prettier-vscode
    formulahendry.auto-close-tag
    formulahendry.auto-rename-tag
    koichisasada.vscode-rdbg
    mechatroner.rainbow-csv
    misogi.ruby-rubocop
    ms-azuretools.vscode-docker
    ms-ceintl.vscode-language-pack-pt-br
    ms-vscode.powershell
    ms-vsliveshare.vsliveshare
    oderwat.indent-rainbow
    ritwickdey.liveserver
    shopify.ruby-extensions-pack
    shopify.ruby-lsp
    sianglim.slim
    tomoki1207.pdf
    visualstudioexptteam.intellicode-api-usage-examples
    visualstudioexptteam.vscodeintellicode
    vscode-icons-team.vscode-icons
    zignd.html-css-class-completion

### A minha configuração do VSCode(settings.json):

    {
      // Interface e Aparência
      "workbench.colorTheme": "Spinel",
      "workbench.preferredDarkColorTheme": "Dracula",
      "workbench.iconTheme": "vscode-icons",
      "editor.fontSize": 16,
      "editor.fontLigatures": true,
      "editor.fontFamily": "Lucida Console, 'Cascadia Code', 'Consolas', 'Courier New', monospace",
      "editor.rulers": [80, 120],
      "editor.renderWhitespace": "trailing",
      "terminal.integrated.fontSize": 16,

      // Configurações do Editor
      "editor.suggestSelection": "first",
      "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
      "editor.defaultFormatter": "esbenp.prettier-vscode",
      "editor.formatOnSave": true,
      "editor.tabSize": 2,
      "editor.detectIndentation": false,

      // Git
      "git.enableSmartCommit": true,
      "git.enabled": true,
      "git.confirmSync": false,
      "git.defaultCloneDirectory": "",

      // Segurança
      "security.workspace.trust.startupPrompt": "never",
      "security.workspace.trust.enabled": false,
      "security.workspace.trust.emptyWindow": false,

      // Prettier Configurações
      "prettier.tabWidth": 2,
      "prettier.semi": false,
      "prettier.singleQuote": true,
      "prettier.trailingComma": "none",
      "prettier.arrowParens": "avoid",
      "prettier.endOfLine": "auto",

      // Formatação específica por linguagem
      "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode",
        "editor.formatOnSave": true,
        "editor.formatOnType": true
      },
      "[javascriptreact]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode",
        "editor.formatOnSave": true,
        "editor.formatOnType": true
      },
      "[html]": {
        "editor.defaultFormatter": "vscode.html-language-features"
      },
      "[erb]": {
        "editor.defaultFormatter": "aliariff.vscode-erb-beautify",
        "editor.formatOnSave": true
      },
      "[ruby]": {
        "editor.defaultFormatter": "Shopify.ruby-lsp",
        "editor.formatOnSave": true,
        "editor.formatOnType": true,
        "editor.insertSpaces": true,
        "editor.semanticHighlighting.enabled": true,
        "files.trimTrailingWhitespace": true,
        "files.insertFinalNewline": true,
        "files.trimFinalNewlines": true,
        "editor.rulers": [120],
        "ruby.useBundler": true,
        "ruby.useLanguageServer": true,
        "ruby.intellisense": true,
        "ruby.codeCompletion": true,
        "rubyLsp.formatter": "auto",
        "lspServer.enabled": true,
        "rubyLsp.featuresConfiguration": {},
        "rubyLsp.rubyExecutablePath": "/home/vulcan/.asdf/shims/ruby",
        "rubyLsp.customRubyCommand": "asdf",
        "rubyLsp.rubyVersionManager.identifier": "asdf",
        "rubyLsp.linters": ["rubocop", "standard", "brakeman"],
        "rubyLsp.enableExperimentalFeatures": true,
        "rubyLsp.enabledFeatures": {
          "codeActions": true,
          "diagnostics": true,
          "documentHighlights": true,
          "documentLink": true,
          "documentSymbols": true,
          "foldingRanges": true,
          "formatting": true,
          "hover": true,
          "inlayHint": true,
          "onTypeFormatting": true,
          "selectionRanges": true,
          "semanticHighlighting": true,
          "completion": true,
          "codeLens": true,
          "definition": true,
          "workspaceSymbol": true,
          "signatureHelp": true
        }
      },
      "[jsonc]": {
        "editor.quickSuggestions": {
          "strings": true
        },
        "editor.suggest.insertMode": "replace"
      },

      // Terminal
      "terminal.integrated.automationShell.osx": "",
      "terminal.integrated.splitCwd": "workspaceRoot",
      "terminal.integrated.automationShell.linux": "",
      "profiles": {
        "defaults": {},
        "list": [
          {
            "guid": "{07b52e3e-de2c-5db4-bd2d-ba144ed6c273}",
            "name": "Windows PowerShell",
            "commandline": "powershell.exe",
            "hidden": false,
            "fontSize": 16,
            "startingDirectory": "D:\\",
            "colorScheme": "One Half Dark",
            "fontFace": "Cascadia Code PL",
            "tabTitle": "balta.io",
            "tabColor": "#8625d2"
          }
        ]
      },

      // Outras Configurações
      "diffEditor.ignoreTrimWhitespace": false,
      "workbench.editor.enablePreview": false,
      "liveServer.settings.donotShowInfoMsg": true,
      "liveServer.settings.donotVerifyTags": true,
      "files.associations": {
        "*.html.erb": "erb"
      },
      "indentRainbow.ignoreErrorLanguages": ["markdown"],
      "json.schemas": [],
      "launch": {
        "configurations": [],
        "compounds": []
      },
      "workbench.editorAssociations": {
        "*.svg": "default"
      },
      "vsicons.dontShowNewVersionMessage": true,
      "guides.enabled": false,

      // Emmet Configurações
      "emmet.includeLanguages": {
        "html": "html",
        "javascript": "javascript",
        "erb": "html",
        "ruby": "html",
        "ejs": "html"
      },
      // Configurações do Solargraph (integrado via ruby-lsp da Shopify)
      "solargraph.diagnostics": true,
      "solargraph.useBundler": false, // Altere para true se desejar usar o Bundler
      "solargraph.bundlerPath": "/home/vulcan/.asdf/shims/bundle", // Caminho para o Bundler se useBundler for true
      "solargraph.formatting": true,
      "solargraph.completion": true,
      "solargraph.hover": true,
      "solargraph.references": true,
      "solargraph.rename": true,
      "solargraph.symbols": true,
      "solargraph.checkGemVersion": true,

      "rails.workspaceSymbols": true, // Habilita símbolos de espaço de trabalho para Ruby on Rails
      "rails.fileWatcher": true, // Habilita o monitoramento de arquivos para projetos Rails

      "files.watcherExclude": {
        "**/log/**": true,
        "**/tmp/**": true,
        "**/node_modules/**": true,
        "**/public/assets/**": true,
        "**/public/packs/**": true
      }
    }
