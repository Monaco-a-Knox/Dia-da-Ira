# Traduzindo a engine MalieSystem

Dentro do arquivo ```.ini``` estão instruções sobre música de menu, cor de texto lido, tamanho da fonte e outras coisas.
Dentro da pasta ```data``` costuma-se encontrar o cursor e o ícone, os quais o jogo (Dies Irae) só reconhecem se não estiverem compilados.
Dentro do arquivo ```translation.csv```, quando houver, é possível traduzir alguns botões do jogo que são acessados pela janela. Infelizmente eles não suportam acentuação.

A engine MalieSystem sempre dá prioridade para puxar o script e demais conteúdos adicionais no ```.dat``` de numeração mais alta. Em Dies Irae, todo o conteúdo do patch está no ```data5.dat```.
É possível fazer mais de um arquivo, colocando coisas diferentes em cada. Neste patch, eu coloquei tudo num só arquivo, embora seja possível fazer um segundo somente com cenas sem censura, assim o jogador poderia optar por tê-las ou não.
Uma vez que sou conta a censura, não o fiz, mas você pode fazer sua própria versão caso tenha aversão a gore, calcinhas ou mamilos.

# Extração do script

O script está criptografado dentro do ```exec.dat```, que fica localizado dentro de um dos aquivos ```data.dat```, normalmente na pasta ```system```.

Utilize a versão modificada do [GARbro](https://github.com/crskycode/GARbro/commits/master/) para conseguir abrir os ```.dat``` da maioria dos jogos produzidos pela Light.
É possível utilizar dois programas para converter ```exec.dat``` em ```exec.txt```.

O primeiro é o StringTool, criado por [marcussacana](https://github.com/marcussacana/SacanaWrapper). Este programa é mais recomendado para extrair o script em inglês devido a maneira como as linhas são exibidas.

É importante que tanto o ```exec.dat``` quanto o ```exec.txt``` **tenham o mesmo número de linhas e estejam na mesma pasta**.
Caso o número de linhas não seja igual, o programa não irá compilar. Essa exigência vale também para o programa mencionado abaixo.

Infelizmente, o script extraído pelo StringTool não permite acesso às escolhas e nomes na caixa de texto, tampouco permite adicionar ou remover sobrescritos (rubys) e itálicos, embora possa ignorá-los.

Para isso, é necessário utilizar o programa Malie_Script_Tool, criado por [Crsky](https://github.com/crskycode/Malie_Script_Tool). Este programa é mais recomendado para extrair o script japonês.

O arquivo ```exec.msg.txt``` contém o texto duplicado, na qual somente a segunda linha importa para a tradução.

O arquivo ```exec.str.txt``` contém as escolhas e nomes dos personagens. Nele também é possível modificar a exibição do texto horizontal/vertical.

```msgframe type='enable' dir='normal'``` indica a direção do texto: normal/horizonta e vertical.
```msgframe src='normal_r'``` indica qual caixa de texto será utilizada. Aqui refere-se a caixa vertical direita de KKK, na qual as dimensões podem ser modificadas editando ```normal_r.svg```
```src='text01'``` refere-sem, em KKK, às imagens das cartas.

Para usá-lo, é necessário compilá-lo com o Visual Studio. O programa possui um bug, então é necessário compilá-lo duas vezes. Primeiro para criar uma versão específica para decompilar. Em seguida, delete as linhas 19 e 22 em ```Program.cs``` e compile novamente para criar uma versão de compilação.
Você encontre ele já compilado por mim neste [repositório](https://github.com/Monaco-a-Knox/Dia-da-Ira/blob/main/outros/malie%20tools.7z).

Infelizmente, nenhum desses métodos dá acesso ao script na íntegra, com toda sua programação. É por isso que modificar o número de linhas quebra a compilação.

Além disso, por vezes, um programa pode apresentar incompatibilidades com o outro. Ocorre de um ```.dat``` compilado pelo Malie_Script_Tool não ser aberto depois pelo StringTool — normalmente ao fazer mudanças no ```exec.str.txt```.

# Quebra de linha - line break/wordwarp

Com exceção da versão inglesa de Dies Irae, que corrige esse problema automaticamente, os demais jogos vão quebrar as palavras no meio caso não tenha espaço na linha.
Para corrigir isso, é necessário adicionar [n] para quebrar as linhas. Uma forma de fazer isso automaticamente é o script criado por [Cosetto](https://github.com/Akaruzi/dies_aitrans/issues/4#issuecomment-2076302302). É preciso modificá-lo para se ajustar ao seu jogo, indicando a codificação do seu script e quantos caracteres cabem por linha na sua caixa de texto.

# Códigos e comandos

- [n] — quebrar linha/adicionar nova linha
- [c] — quebrar linha/adicionar nova linha (aparentemente não há diferença)
- [z] — fim da linha/esperar pelo próximo clique
- [s] — fim da linha dublada/interromper áudio após o clique
- [r] — não lembro o que faz
- []() — adicionar sobrescrito (ruby) e.g [ 破壊 ](あい)
- [](、) — ênfase japonesa e.g [ 先 ]( 、)[ 達 ]( 、)
- v_sy0086 — indica o arquivo de voz
- Quando for utilizar o travessão duplo (——) opte pelo japonês (――) pois ele é exibido melhor dentro do jogo.
- Em Dies Irae, este código estranho adiciona itálico.

- Os comandos acima só podem ser utilizados extraindo o texto com o Malie_Script_Tool.
- As runas de DI/KKK aparecem como caracteres ilegíveis na extração do Malie_Script_Tool, já na extração do StringTool, a linha meramente fica vazia.
- Em KKK, é possível adicionar textos sobrescrito por cima das runas (神代文字), mas somente no modo NVL.

# Edição de imagens

O jogo sempre dará prioridade para os arquivos originais fracionados em ```.webp```, onde as informações de montagem encontram-se nos arquivos ```.dzi```.

Entretanto, você pode substituí-los por arquivos ```.png```. Para isso, é necessário modificar os arquivos ```.svg``` correspondentes de cada imagem individualmente, adicionando o link da sua imagem modificada e.g. ```xlink:href='./image01_pt.png'```.
Caso suas imagens editadas possuam outras dimensões, é preciso modificar também os valores ```width/height```. Se precisar modificar o posicionamento, altere também as coordenadas ```x/y```.

Se você extrair todo o conteúdo do jogo com o GARbro e remover os ```data.dat```, o jogo vai puxar todos os arquivos diretamente das pastas extraída.
Em alguns jogos, como KKK, onde textos verticais precisam ser reposicionados manualmente na direção horizontal, acertar as coordenadas é um desafio.
Sendo assim, este processo é recomendado para poder testar as modificações sem precisar compilar tudo dentro de um ```data.dat``` diversas vezes até dar certo.

Se você souber chinês, o usurário Akaruzi escreveu recentemente um [guia](https://github.com/Akaruzi/kkk_r18_patch/blob/master/README.md) mais detalhado e com imagens ilustrativas.

# Compilação

Para compilar todos os arquivos do jogo dentro de um novo ```data.dat``` é necessário utilizar o programa [Malie's packer](https://github.com/satan53x/SExtractor/tree/main/tools/Malie).

É importante observar a estrutura original do jogo. Em Dies Irae, todos os arquivos e subpastas ficam dentro da pasta ```data```, então indique o caminho onde a pasta está localizada, não a pasta em si. No caso deste patch, é indicado a pasta ```patch```, onde dentro encontra-se a ```data```.

Para cada jogo que utilize a engine MalieSystem, é necessário modificar o ```dat_pack.py```, indicando os bytes do offset 0x10~0x17 do ```data1.dat``` , [desta forma](https://github.com/Akaruzi/dies_aitrans/issues/4#issuecomment-1913515911)

Neste patch específico, todo o processo de compilação é feito automaticamente através do [GitHub Actions.](https://github.com/Monaco-a-Knox/Dia-da-Ira/blob/main/dependencies/compile_pc.py).
Para rodar localmente, use o comando ```python dependencies\compile_pc.py```

# Tipografia

As fontes usadas em jogos da Light aceitam praticamente todos os caracteres romanos, com exceção de caracteres romenos/poloneses/turcos específicos, tais quais: ś, ṇ, ṃ, ș etc.
Nem todos os kanjis chineses são suportados.

Caso sejam essências, você pode modificar a fonte ou substituí-la por qualquer outra fonte ```.otf```. A nova fonte pode ter o mesmo nome da antiga, ou atualizar o ```malie.ini``` com o nome da nova fonte.
No caso de KKK, o jogo já oferece diferentes fontes puxadas do sistema.

# Tradução e censura de Dies Irae

A tradução inglesa de Dies Irae, embora oficial, é de procedência duvidosa. Muitas linhas “americanizadas” e apagamento de referências culturais. Infinitos palavrões desnecessários, frases incompletas, linhas reescritas ao ponto de parecer uma fanfic, inconsistências narrativas entre 1º e 3º pessoa e diversos erros de tradução. A rota da Kei é facilmente uma das piores coisas que já vi. Faz as demais parecerem maravilhosas.  **Por isso, trabalhar conjuntamente ao script japonês lado a lado torna-se imprescindível.**

Como você deve saber, a versão japonesa de Amantes Amantes, lançada para computador, é baseada na versão de PSP. Todo eroge lançado para console sofre censura, tanto visual quanto textual, muito além de meramente remover as cenas de sexo. Há cerca de 300 linhas que foram editadas, corrigidas, modificadas censura ou removidas na versão japonesa de console.
Sendo assim, acaba por ser **obrigatório usar o script inglês como base para a tradução**, isso porque ele **restaurou** grande parte das linhas originais da versão Acta Est Fabula, tanto as linhas reescrita quanto as linhas que foram removidas.
Contudo, a versão inglesa não restaurou 100% dessas linhas — 95% eu diria.

Tudo o que eu pude restaurar em conformidade ao jogo original, eu restaurei, incluído no patch os respectivos arquivos de voz originais. Infelizmente duas linhas (v_vi0267 e v_sy2162) não podem ser restauradas porque foram removidas no japonês e o inglês não restaurou. 
A versão inglesa também optou por restaurar **apenas algumas** artes sem censura e **manter outras** censuradas. Neste patch, eu as **restaurei**.

Adicionar qualquer linha extra quebra o atual processo de compilação. Assim sendo, é impossível fazer uma versão 2 em 1, com todo o conteúdo do Amantes e as cenas H do Acta.

# Observações

- Os jogos japoneses precisam do crack chinês AlphaROMdiE, o qual você já deve conhecer bem.
- Em alguns jogos, como Senshinkan, você pode ter problemas para instalar. Meramente extrair o conteúdo do primeiro arquivo não vai extrair na sequência o conteúdo dos seguintes. É necessário extrair um por um, individualmente.
- Em Kajiri Kamui Kagura, você pode ter problemas com a caixa de texto se modificar o script com todos os arquivos extraídos. Jamais delete os ```.dat``` originais pois são necessários para restaurar a caixa que você quebrou.

