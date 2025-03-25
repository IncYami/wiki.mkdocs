# VapourSynth

!!! info "Sistemas"
    - Windows 11 (Mais recente)

## **Instalação**

**Baixe os seguintes programas e siga as etapas para instalação e configuração**
!!! abstract ""
    ### [:fontawesome-brands-python: __Python__](https://www.python.org/ftp/python/3.12.9/python-3.12.9-amd64.exe)
    ![Python Version](https://img.shields.io/badge/python-3.12.9-blue?style=flat-square)
    ***

!!! abstract ""
    ### [:fontawesome-solid-microchip: __VapourSynth (x64)__](https://github.com/vapoursynth/vapoursynth/releases) 
    ![GitHub release (latest by date)](https://img.shields.io/github/v/release/vapoursynth/vapoursynth?color=%233fb950&style=flat-square)
    ***
    Baixe o arquivo ` VapourSynth-x64-RXX.exe ` da versão mais recente com a tag Latest

!!! abstract ""
    ### [:fontawesome-solid-code: __VS Code (System Installer)__](https://code.visualstudio.com/sha/download?build=stable&os=win32-x64)
    ![GitHub release (latest by date)](https://img.shields.io/github/v/release/microsoft/vscode?color=%233fb950&style=flat-square)
    ***
    - **Etapa: Selecione o Local de Destino**

    Certifique que o local de instalação seja: `C:\Program Files\Microsoft VS Code`

    <br>

    - **Etapa: Selecionar Tarefas Adicionais**

    Nas opções de "**Outros**" deixe marcado conforme abaixo:

    :material-checkbox-outline: Adicione a ação "Abrir com Code" ao menu de contexto de arquivos do Windows Explorer

    :material-checkbox-outline: Adicione a ação "Abrir com Code" ao menu de contexto de diretório do Windows Explorer

    :material-checkbox-blank-outline: Registre Code como um editor para tipos de arquivos suportados

    :material-checkbox-outline: Adicione em PATH (disponível após reiniciar)

## **Dependências (Python)**

!!! warning ""
    Abra `CMD` como Administrador

Execute os sequintes comandos:

!!! example ""
    **Jaded Encoding Thaumaturgy**

    - [Wiki](https://jaded-encoding-thaumaturgy.github.io/JET-guide)
    - [GitHub](https://github.com/Jaded-Encoding-Thaumaturgy)

    ```
    pip install vsjet
    ```
    ```
    py -m vsjet latest
    ```

!!! example ""
    **muxtools**

    - [Wiki](https://muxtools.vodes.pw)
    - [GitHub](https://github.com/Jaded-Encoding-Thaumaturgy/muxtools)

    ```
    pip install git+https://github.com/Jaded-Encoding-Thaumaturgy/muxtools.git
    ```
    ```
    pip install git+https://github.com/Jaded-Encoding-Thaumaturgy/vs-muxtools.git
    ```

## **Plugins**

Faça download dos plugins e extraia para a pasta `C:\Program Files\VapourSynth\plugins`:

{{ read_excel('assets/VapourSynth/plugins.xlsx', engine='openpyxl') }}