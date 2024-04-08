# Dia da Ira

Patch com a tradução em português da visual novel Dies Irae ~ Amantes Amentes ~. 
Compatível com a versão inglesa DX package. Possivelmente funcional com a versão Steam e também com a versão japonesa em HD -Animation Anniversary-. Embora a japonesa permita jogar em resolução 16:9 e 4:3, ela não é recomendada porque pode apresentar problemas.

Além de adicionar a tradução, este patch restaura o **cursor original**, a **música original de menu**, a **cor original** de texto lido, o **título original** dos capítulos **III e VI**, algumas **CGs sem censura** e  **arquivos de voz faltantes ou censurados**.

# Progresso
- Introdução - 1/1 legenda
- Prólogo - 1/1 capítulo
- Rota comum - 6/6 capítulos
- Rota da Kasumi - 7/7 capítulos
- Rota da Kei - 2/7 capítulos
- Rota da Marie - 5/7 capítulos
- Rota da Rea - 7/7 capítulos
- Other Story - 5/5  capítulos
- Total - 33/40 capítulos

Ao todo são 59812 linhas de texto em si, sendo 53851 linhas únicas (5.7MB)

# Instalação Final - futuramente

- Baixe o patch disponível no Github.
- Extraia o conteúdo e coloque a pasta da ```data```, juntamente dos arquivos ```data.5``` e ```malie.ini``` na pasta raiz do jogo.

Se e o jogo abrir com outro ícone, cursor em forma de espada e vídeo introdutório traduzido, a instalação está concluída.

# Explicação de como o Patch funciona.

Dentro do arquivo ```.ini``` estão instruções para a restauração da música de menu e cor do texto lido, em conformidade com a versão original japonesa.
Dentro da pasta ```data``` está o cursor e o ícone, os quais o jogo só reconhecem se não estiverem compilados.
Dentro do arquivo ```data5.dat``` estão todos os demais arquivos referentes ao patch. A engine sempre dá prioridade para buscá-los no ```.dat``` de numeração mais alta.


# Tradução

Em 2017, eu traduzi algumas cenas aleatórias, mas diversos problemas no jogo e a falta de ferramentas para criar um patch completo impediam de iniciar um projeto de tradução na época.
Em 2023, eu decidi inserir o que tinha traduzido no jogo e, logo em seguida, encontrei ferramentas recentes que permitiriam fazer um patch e contornei quase todos os problemas. 
Assim, resolvi terminar o que havia começado e embarcar na lamentável loucura de traduzir o jogo inteiro sozinho. Portanto, pode haver uma variação de qualidade nas cenas antigas em relação ao restante.
Talvez eu desista e nunca termine a rota da Kei...

Para traduzir, é necessário extrair o arquivo ```exec.dat``` de dentro do ```data3.dat```, localizado na pasta ```system```, utilizando o GARbro.
Tendo extraído, utilize o programa StringTool, criado por [marcussacana](https://github.com/marcussacana/SacanaWrapper), para converter o script em ```exec.txt```.
Para compilar, utilize novamente o programa StringTool.exe.
É importante que tanto o ```exec.dat``` quanto o ```exec.txt``` **tenham o mesmo número de linhas e estejam na mesma pasta**.
Caso o número de linhas não seja igual, o programa não irá compilar.

Para traduzir as escolhas e nomes na caixa de texto, utilize Malie_Script_Tool, criado por [Crsky](https://github.com/crskycode/Malie_Script_Tool), para converter o script em ```exec.msg.txt``` e ```exec.str.txt```
Para usá-lo, é necessário compilá-lo com o Visual Studio. O programa possui um bug, então é necessário compilá-lo duas vezes. Primeiro para criar uma versão específica para decompilar. Em seguida, delete as linhas 19 e 22 em ```Program.cs``` e compile novamente para criar uma versão de compilação.

O script de Dies Irae, da forma como é extraído pelo StringTool, possuí uma peculiaridade: cada palavra em itálico ou sobrescrita (ruby) obrigatoriamente exige estar separada em uma nova linha. 
Devido a diferença no número de linhas, não é recomendado para se trabalhar com o script japonês (embora não seja impossível).
Por causa da limitação do número de linhas, você não pode remover itálicos e rubys (embora possa ignorar), tampouco pode adicionar novos itálicos ou ruby, fazendo com que seja refém do texto.

Extraindo com o Malie_Script_Tool, o problema de itálicos e rubys é corrigido. No entanto, o programa extrai o texto duplicado (apenas a segunda linha importa). O ideal é utilizá-lo apenas para traduções do japonês ou para fazer edições, adicionando itálicos, rubys e quebras de linha.

A tradução inglesa de Dies Irae, embora oficial, é de procedência duvidosa. Muitas linhas “americanizadas” e apagamento de referências culturais. Infinitos palavrões desnecessários, frases incompletas, linhas reescritas ao ponto de parecer uma fanfic, inconsistências narrativas entre 1º e 3º pessoa e diversos erros de tradução. A rota da Kei é facilmente uma das piores coisas que já vi. Faz as demais parecerem maravilhosas.  **Por isso, trabalhar conjuntamente ao script japonês lado a lado torna-se imprescindível.**

# Compilação

A compilação do patch será feita automaticamente através do GitHub Actions. Para rodar localmente, use o comando ```python dependencies\compile_pc.py```

Para compilar manualmente todos os arquivos do jogo dentro do ```data5.dat``` é necessário utilizar o programa [Malie's packer](https://github.com/satan53x/SExtractor/tree/main/tools/Malie).
Basta colocar os arquivos relacionados à tradução dentro de uma pasta ```data``` com as mesmas subpastas que compõem o jogo original, e então rodar o programa em pyhton, selecionando o caminho onde a sua pasta ```data``` está localizada, não a pasta ```data``` em si. Neste caso, é a pasta ```patch``` que deve ser selecionada.
Para cada jogo que utilize a engine Malie, é necessário o indicar os bytes do offset 0x10~0x17 do ```data1.dat``` , [desta forma](https://github.com/Akaruzi/dies_aitrans/issues/4#issuecomment-1913515911)

Para a substituição das imagens sem censura, é necessário ter os ```.dzi``` e todos os relacionados a elas, localizados na pasta ```tex```, caso contrário a resolução é exibida errado. É possível substituir por arquivos ```.png```, mas o processo é mais complicado, uma vez que você precisa editar os nomes de cada arquivo no ```exec.str.txt```, além de que a resolução também é exibida erroneamente. Fazendo dessa forma, as imagens são substituídas dentro do jogo, mas não na galeria.

# Censura

Como você deve saber, a versão japonesa de Amantes Amantes, lançada para computador, é baseada na versão de PSP. Todo eroge lançado para console sofre censura, tanto visual quanto textual, muito além de meramente remover as cenas de sexo.
Sendo assim, acaba por ser **obrigatório usar o script inglês como base para a tradução**, isso porque ele **restaurou** grande parte das linhas originais da versão Acta Est Fabula, tanto as linhas reescrita quanto as linhas que foram removidas.
Contudo, a versão inglesa não restaurou 100% dessas linhas. 

Tudo o que eu pude restaurar em conformidade ao jogo original, eu restaurei, incluído no patch os respectivos arquivos de voz originais. Infelizmente duas linhas (v_vi0267 e v_sy2162) não podem ser restauradas porque foram removidas. Adicionar qualquer linha extra quebra o atual processo de compilação. Assim sendo, é impossível fazer uma versão 2 em 1, com todo o conteúdo do Amantes e as cenas H do Acta.

A versão inglesa também optou por restaurar **apenas algumas** artes sem censura e **manter outras** censuradas. Neste patch, eu as **restaurei**.

# Observações
- Infelizmente não é possível corrigir os nomes que aparecem entre os capítulos. Eles foram alterados na versão inglesa e só é possível encontrar os arquivos originais em ```.dzi``` na versão de Nintendo Switch, a qual não consegui extrair todo o conteúdo. Embora seja possível substituir por arquivos ```.png```, é muito trabalhoso e a maneira mais prática envolveria extrair todo o conteúdo do jogo e substituir manualmente. Se você souber como extrair os ```.dat``` do console, entre em contato.
- Dies Irae é intraduzível, não por causa de seu vocabulário, mas pelo seu estilo narrativo em uma 3º pessoa que simula 1º pessoa. Preservar fielmente esse estilo geraria estranhezas, entretanto a reescrita faz da tradução puramente interpretativa. Não importa se você ler em português, inglês, russo ou qualquer outro idioma (talvez o chinês seja exceção), você não estará lendo Dies Irae, mas uma fanfic. Nesta tradução, a narração simulada de 1º pessoa foi reescrita em 3º pessoa, similar ao que foi feito na versão inglês, mas preservando o tom narrativo original de 1º pessoa em cenas específicas, sempre indicando com aspas ou travessão. 