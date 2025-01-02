# MAS

Um ativador do Windows e do Office usando métodos de ativação HWID / Ohook / KMS38 / Online KMS, com foco em código-fonte aberto e menos detecções de antivírus.

### Ativando o Windows / Office

!!! info "**Método 1 - PowerShell**"
    - Clique com o botão direito no menu iniciar do Windows e selecione PowerShell ou Terminal (Não CMD).
    - Copie e cole o código abaixo e pressione Enter:
     ```
     irm https://get.activated.win | iex
     ```
    ??? note "Mais opções"
        - Em versões mais antigas do Windows (17134 e anteriores), você precisará executar o comando abaixo antes de seguir as etapas acima:
        ```
        [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
        ```
    - Você verá as opções de ativação. Siga as instruções na tela.
    - Isso é tudo.

!!! info "**Método 2 - Tradicional**"
    - Baixe o arquivo sob o botão de código do [GitHub](https://github.com/massgravel/Microsoft-Activation-Scripts) ou do [Bitbucket](https://bitbucket.org/WindowsAddict/microsoft-activation-scripts)
    - Clique com o botão direito no arquivo zip baixado e extraia
    - Na pasta extraída, encontre a pasta chamada `All-In-One-Version`
    - Execute o arquivo chamado `MAS_AIO-CRC32_XXXXXXXX.cmd`
    - Você verá as opções de ativação, siga as instruções na tela.
    - Isso é tudo.

Para executar os scripts no modo não interativo, verifique: [Command Line Switches](https://massgrave.dev/command_line_switches)

### Resumo das Ativações

| Tipo de Ativação | Produto Suportado   | Período de Ativação                         |
|:-----------------|:--------------------|:--------------------------------------------|
| HWID             | Windows 10-11       | Permanente                                  |
| Ohook            | Office              | Permanente                                  |
| KMS38            | Windows 10-11-Server| Até o ano de 2038                           |
| Online KMS       | Windows / Office    | 180 dias. Vitalício com Tarefa de Renovação |

Para ativar produtos não suportados, como o Office no Mac, verifique: [Office For Mac](https://massgrave.dev/office_for_mac).