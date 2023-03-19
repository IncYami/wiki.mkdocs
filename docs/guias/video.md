# Video players

## **PC**

- [MPV](https://mpv.io/) - [Tutorial de instalação e configuração]() (recomendado)
- [MPC-HC](https://github.com/clsid2/mpc-hc/releases) / [Potplayer](https://potplayer.daum.net/)

!!! danger "Não use o VLC!"
    O VLC não é recomendado porque geralmente exibe cores erradas, apresenta artefatos visuais e quebra legendas intensivas. Aqui estão algumas comparações mostrando esses problemas:

    - [Comparação 1](https://slow.pics/c/XhbmrYgU)

    - [Comparação 2](https://slow.pics/c/vH560pvp)

## **Android**

- [mpv-android](https://play.google.com/store/apps/details?id=is.xyz.mpv)
- [MX player](https://play.google.com/store/apps/details?id=com.mxtech.videoplayer.ad)

## **iOS**

- [MX player](https://apps.apple.com/in/app/mx-player/id1429703801)
- [Outplayer](https://apps.apple.com/br/app/outplayer/id1449923287)

## **TV**

Apenas use um cabo HDMI 👍

***

## Servidor de mídia

A configuração consiste em duas partes - o servidor e o cliente. Um cliente é simplesmente um reprodutor de mídia que acessará o conteúdo de um servidor. O servidor é executado no dispositivo que armazena seu conteúdo. Ambos podem ser instalados no mesmo sistema, mas são aplicativos separados. Normalmente, você teria o servidor em um computador conectado a outros dispositivos em sua rede doméstica e um cliente instalado em todos esses dispositivos. Todos os três populares vêm com seu próprio cliente/jogador, bem como suporte para usar o kodi como cliente (recomendado para anime).

- [Plex](https://www.plex.tv/) - [Guia para Anime](https://docs.google.com/document/d/1sXKZDYzbBDDWS8eqJ3IcaxSWhYKIPDdtChm74CBJ6ig)
- [Emby](https://emby.media/)
- [Jellyfin](https://jellyfin.org/)

### Escaneando anime sem renomear

- [Scanning files without renaming them](https://kodi.wiki/view/Anime#Scanning_files_without_renaming_them)
- [Absolute Series Scanner Plex](https://github.com/ZeroQI/Hama.bundle)

***

## Scaling

1. Qualidade não é o mesmo que resolução.
2. Sempre que algo com uma resolução diferente da sua tela estiver sendo reproduzido no modo de tela cheia, algo está sendo dimensionado para a resolução da tela.

Esse algo geralmente é o reprodutor de vídeo. Por exemplo, reproduzir um vídeo de 1080p em um monitor de 2160p significa que ele deve ser ampliado para preencher a tela, caso contrário, ele simplesmente seria reproduzido em 1/4 da tela. O upscaling não é uma opção que você pode habilitar ou desabilitar em tela cheia, a única coisa que pode ser alterada é o método de escala. Consequentemente, o upscaling não é algo que você possa usar para "aprimorar" o vídeo ao reproduzi-lo na mesma resolução. Não é uma maneira de melhorar de alguma forma a reprodução de vídeo 1080p em uma tela 1080p. Os shaders são ativados apenas quando a resolução do vídeo não corresponde à resolução da tela e o dimensionamento é necessário.

A escala padrão na maioria dos players é ruim. MPV foi construído em um perfil de alta qualidade chamado gpu-hq que permite melhores algoritmos de upscaling (scale=spline36, cscale=spline36, dscale=mitchell). Essa opção é necessária mesmo se você usar shaders externos para atuar como um fallback. Quaisquer opções de dimensionamento explicitamente especificadas depois disso irão substituí-lo. Para aqueles com GPUs poderosos, shaders externos de qualidade ainda mais alta estão disponíveis - FSRCNNX, NNEDI etc. O arquivo deve ser colocado em %appdata%/mpv/shaders e na linha `glsl-shader="~~/FSRCNNX_x2_8-0-4 -1.glsl"` deve ser adicionado à configuração. Pressione shift+I seguido de 2 para confirmar que o shader está funcionando. Quadros perdidos ou tempos de quadro altos (acima de 25 ms) são um sinal de que sua GPU não consegue acompanhar e você deve mudar para um shader menos exigente.

Os shaders mencionados acima são 2x scalers, o que significa que eles sempre são dimensionados em 2x. Para 720p a 1080p, o vídeo será primeiro dimensionado para 1440p por FSRCNNX e depois reduzido para 1080p por dscale=mitchell. Para 720p a 2160p, FSRCNNX fará de 720p a 1440p e, em seguida, scale=spline36 escalará o restante até 2160p. Quando é necessário dimensionar abaixo de um determinado limite, FSRCNNX não será ativado e MPV retornará para spline36. Também existem escaladores como ravu-zoom que podem aumentar para proporções arbitrárias, ao custo de desempenho lento devido à renderização direta para a resolução de destino.

- [Ravu e NNEDI](https://github.com/bjin/mpv-prescalers)
- [FSRCNNX](https://github.com/igv/FSRCNN-TensorFlow/releases)

## Filtragem

O mesmo tipo de filtragem usado pelos encoders, mas em tempo real. Não é uma alternativa para uma bom encode, mas sim uma correção temporária para fontes da web. Debanding é o mais comumente usado e o único necessário. Aprimoramento de detalhes, redução de ruído, nitidez etc. não são recomendados. Todas essas opções estão disponíveis com MPV e madvr. Mais informações sobre qualidade, artefatos de vídeo e codificação no [Guia de Qualidade](/guias/qualidade).

## Reprodução Suave

**O problema:** Quase todos os animes são reproduzidos a 23,976 fps (tecnicamente 24000/1001), mas vamos arredondar para 24 fps por conveniência. No entanto, os monitores geralmente são executados em taxas de atualização que não correspondem a essa taxa de quadros, levando a um efeito conhecido como Judder.

O Judder é mais comumente visto em laptops/desktops com monitores de 60 hz, porque a taxa de atualização não é um múltiplo inteiro da taxa de quadros do conteúdo. 60hz/24fps é 2,5 e, como você não pode atualizar 2,5 vezes por quadro, deve ser calculada a média ao longo do tempo. Nesse caso, o primeiro quadro será mantido por 2 atualizações, o segundo quadro por 3 atualizações, o terceiro por 2 e assim por diante, levando à média de 2,5. Por causa disso, cada quadro é mostrado por um período de tempo diferente (33,3 ms para quadros pares, 50 ms para ímpares), o que faz com que o movimento pareça vago/lento, isso é especialmente perceptível durante as cenas panorâmicas.
Embora quase todos os animes sejam 24fps, você também pode assistir a outros conteúdos, como ação ao vivo (às vezes 25fps) e YouTube (principalmente 30/60fps, às vezes 25/50fps) e, se o fizer, é importante poder reproduzir essas taxas de quadros de volta apropriadamente.

**A solução:** combinar a taxa de atualização da tela com a taxa de quadros do conteúdo, para a qual existem muitos métodos

**Sincronização adaptável:** Compatível com G-Sync/G-Sync (Certificado)/Freesync Premium é de longe a melhor solução, mas requer a GPU e o monitor corretos para usar. A exibição corresponderá perfeitamente ao conteúdo, independentemente da taxa de quadros. O Freesync normal pode funcionar, mas somente se o monitor for compatível com LFC.
Certifique-se de usar um player que ativará a sincronização adaptativa, como MPV.

**Ajuste da taxa de atualização automática:** Muitos dispositivos de streaming (Apple TV, Shield, Fire stick, etc.) software de reprodução (Kodi, Plex etc). O conteúdo 24/30/60fps deve funcionar perfeitamente, no entanto, o conteúdo 25fps requer suporte 25/50hz, que algumas TVs em [regiões NTSC](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0d/PAL-NTSC-SECAM.svg/2560px-PAL-NTSC-SECAM.svg.png) pode não suportar.

**Exibições de alta taxa de atualização:** 120hz, 144hz, 240hz e 360hz são todos múltiplos de 24 e, como tal, corresponderão perfeitamente, pois cada quadro pode ser repetido para várias atualizações. No entanto, 144 hz não exibirá conteúdo de 30/60 fps corretamente e nenhum dos itens acima irá lidar com conteúdo de 25 fps corretamente.

## Compatibilidade

Decodificação é o processo de reproduzir o arquivo de vídeo. Existem dois tipos - hardware e software. Tudo pode ser decodificado, a diferença está na quantidade de trabalho necessária para fazer isso. Quando é acelerado por hardware, não sobrecarrega a CPU do seu dispositivo.

A maioria dos players de PC irá decodificar tudo com swdecode como uma opção alternativa. O problema é quando essa decodificação não é rápida o suficiente para reproduzir seu vídeo em tempo real. Isso nunca será um problema, pois o hwdecode é compatível com esse codec.

Se estiver assistindo em um TV/+Android Box, você verá uma lista de codecs suportados em suas especificações. O Plex e outros servidores de mídia reconhecerão um formato como não suportado e iniciarão a transcodificação para H264 de 8 bits. O Kodi player é a melhor opção para decodificação de software como em um PC, oferecendo a opção de sempre transmitir diretamente ou executar sem um servidor. No entanto, como a CPU da sua TV/Box é muito mais fraca em comparação com um PC, haverá casos de atraso horrível ao tentar forçar o swdecode. Observe que a decodificação do software utiliza sua CPU, portanto, a causa do atraso não se limita à decodificação. É qualquer coisa que possa estar usando sua CPU no momento. Como quando há muito typesetting complicada em uma legenda .ass que precisa ser renderizada, que ficará atrasada com uma CPU fraca, não importa qual seja o codec de vídeo. Geralmente:

- H264 8 bits funciona em qualquer lugar
- H264 10 bits raramente funciona sem uma CPU decente. O suporte de decodificação de hardware para isso é inexistente.
- H265 8 bits e 10 bits funcionam quando existe suporte de hardware. A maioria dos dispositivos mais recentes nos últimos 5 anos oferece suporte a ele.

### Typesetting 

Anime geralmente tem estilo de legenda .ass, enquanto os subs aparecerão na maioria das TVs e players (plex, emby, jellyfin etc.), o typesetting ou o diálogo sobreposto às vezes é interrompido. Isso é especialmente um problema se você estiver assistindo fansubs. **Kodi** é um dos poucos players que suporta a renderização adequada. Observe que o player é separado do servidor de mídia kodi e pode até ser usado com o Plex.