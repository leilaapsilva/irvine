## 1.1 Boas vindas a Linguagem Assembly

Este livro, intitulado Linguagem Assembly para Computadores "Intel-Based", foca na programação de microprocessadores Intel, especificamente em membros da 
família de processadores Intel IA-32. A família IA-32começou com o Intel 80386, e continua(?) atuamente no Pentium 4. A linguagem assembly é a linguagem de 
programação mais antiga, e de todas as linguagens, é a mais próxima da linguagem nativa de um computador. Isso proporciona acesso direto ao hardware 
de um computador, tornando necessário que você entenda bastante sobre sua 
arquitetura de computadores e sistema operacional.

*Valor educacional - Porque você tem que ler este livro?* Talvez você esteja em um curso similar a um dos seguintes:

- Linguagem assembly para microcomputadores 
- Linguagem de programação assembly
- Introdução a arquitetura de computadores
- Fundamentos de Sistemas de computação
- Programação de sistemas embarcados

De fato, esses são nomes de cursos em colégios e universidades que usam a 
décima terceira edição deste livro. Você provavelmente escontrará que este 
livro contém mais técnicas de linguagem assembly, referencia de informação e 
exemplos do que você pode digerir em um único semestre.
	Se você está em um curso cujo nome inclui as palavras arquitetura ou 

fundamentos, este livro dará a você alguns princípios básicos sobre arquitetura 

de computadores, linguagem de máquina e programação em baixo nível que 

permanecerão com você por anos. Você aprenderá linguagem assembly suficiente 

para testar seu conhecimento na maioria das famílias de microprocessadores 

utilizadas atualmente. Você não estará aprendendo a programar um computador "de 

brinquedo" usando um assembler simulado; está é a coisa real, a mesma usada 

pelos profissionais. Você irá aprender a arquitetural da família de 

processadores IA-32 do ponto de vista do programador.
	Se você está em dúvida sobre o valor de gastar horas estudando os 

detalhes de baixo nível de software e hardware, talvez você possa encontrar 

inspiração na seguinte citação de uma carta(?) mandada por um dos maiores 

cientistas da computação do nosso tempo, Donald Knuth:
	"Algumas pessoas [dizem] que tendo linguagem de máquina, (at all), foi 

o maior erro que eu cometi. Eu realmente não penso que você pode escrever um 

livro para programadores sérios se você não estiver ábil para discutir detalhes 

de baixo nível."

Site Antes (you go any farther), visite o site web do livro para ver suporte 

extra de informações e exercícios que você pode utilizar:
	http://www.nuvisionmiami.com/books/asm
Há sempre novos tutoriais, exemplos interessantes de programas, correções a 

erros no texto, e (so on). Se por alguma razão a URL fornecida nãoe stiver 

disponível, você pode encontrar o web site do livro pela URL da Prentice Hall 

(www.prenhall.com). Pesquise por "Kip Irvine".

#### 1.1.1 Algumas boas questões 

Talvez nós possamos responder algumas questões sobre este livro e como ele pode 

ser usado. 

Qual background eu devo ter? Antes de ler este livro, você deve ter completado 

um curso na faculdade ou o equivalente em programação de computadores. A 

maioria dos estudantes aprende C++, C#, Java, ou Visua Basic. Outras linguagens 

irão funcionar, devido a ter caracteristicas semelhantes.

O que é um assembler (montador)? Um assembler é um programa que converte 

código-fonte de programas em linguagem assembly para linguagem de máquina. O 

assembler pode opcionalmente gerar um arquivo fonte listado com números, 

endereços de memória, código fonte (statements), e uma referência-cruzada(?) 

listando os símbolos e variáveis usados em um programa. Um programa 

(companion), chamado linker, combina arquivos individuais criados por um 

assembler em um único programa executável. Um terceiro programa, chamado de 

debugger provê uma forma para o programador (to trace) a execução de um 

programa e examinar os (contents) de memória. Dois dos mais populares 

assemblers para a família Intel são MASM (Microsoft Assembler) e TASM (Borland 

Turbo Assembler). 

De quais hardware e software eu preciso? Você precisa de um computador com 

Intel386, Intel486, ou um dos processadores Pentium. Todos esses pertencem a 

família de processadores IA-32, como Intel os denomina. Seu sistema operacional 

deve ser alguma versão do Microsoft Windows, MS-DOS ou algum Linux rodando um 

emulador DOS. Os seguintes itens também são requeridos ou recomendados:

- Editor: Você precisa de um simples editor que possa criar arquivos fonte na 

linguagem assembly. Você pode usar TextPad por Helios Software, que é fornecido 

com o CD-ROM deste livro. Ou você pode usar o Bloco de Notas (grátis no 

Windows), ou o editor do Microsoft Visual Studio (usado com Visual C++). 

Qualquer outro editor que produz arquivos de texto ASCII também podem ser 

usados.


...


Como linguagem assembly (relate to machine language)? Primeiro, linguagem de 

máquina é uma linguagem numérica que é especificamente entendida pelo 

processador de um computador (a CPU). Processadores Intel, por exemplo, têm uma 

linguagem de máquina que é automaticamente entendia por outros processadores 

intel. Linguagem de máquina consiste puramente de números.
	Linguagem assembly consiste de (statements) que usam mneomônicos curtos 

como ADD, MOV, SUB, e CALL. Linguagem assembly tem uma relação um-para-um com 

linguagem de máquina, significando que uma instrução em linguagem assembly 

corresponde a uma instrução de linguagem de máquina. 

Como C++ e Java são traduzidos para linguagem assembly? Linguagens alto nível 

como C++ e Java tem uma relação um-para-vários tanto com linguagem assembly 

quanto com linguagem de máquina. Uma simples declaração em C++, por exemplo, é 

expandida para múltiplas instruções em linguagem assembly ou instruções de 

máquina.
	Vamos (find out firt-hand) como declarações C++ são expandidas em 

código de máquina. A maioria das pessoas não é capaz de ler código de máquina, 

então nós mostraremos relativamente de perto linguagem assembly, (instead). O 

seguinte trecho em C++ (carries out) duas operações aritméticas e armazena o 

resultado em uma variável. Assuma que X e Y são inteiros:
	X = (Y + 4) * 3;

A seguir está a tradução desse trecho para linguagem assembly. Note que a 

tradução requer múltiplas declarações porque a linguagem assembly trabalha em 

um nível detalhado:

	mov eax, Y		; move Y para o registrador EAX
	add eax, 4		; adiciona 4 ao registrador EAX
	mov ebx, 3		; move 3 para o registrador EBX
	imul ebx		; multiplica EAX por EBX
	mov X, eax		; move EAX para X

(Registradores são nomeados locais de armazenamento dentro da CPU que são 

usados em resultados intermediários de operações)

	O ponto neste exemplo não é mostrar que C++ é "melhor" ou mais poderosa 

que linguagem assembly, mas mostrar como assembly implementa uma declaração em 

linguagem de alto-nível. As declarações em assembly tem uma correspondência 

um-para-um com a linguagem de máquina nativa do computador, que é uma série de 

números codificados com significado especial para o processador.

	Nós? Nós quem? Durante este livro, você verá constantes referências a 

nós. Autores de livros-texto e artigos acadêmicos costumam usar nós como uma 

referência formal a si mesmos. Se isso ajudar, pense que nós é uma referência 

ao autor, seus revisores (que realmente o ajudaram muito), seu publicador 

(Prentice-Hall), e seus estudantes (milhares).

Linguagem assembly é portátil? Uma distinção imortante entre linguagens de 

auto-nível e assembly deve ser feita sobre portabilidade. Uma linguagem cujos 

programas podem ser compilados e rodados em uma grande variedade de sistemas 

computacionais é dita portátil. Um programa em C++, por exemplo, deve compilar 

e rodar em praticamente quaquer computador, a menos que faça referências 

específicas a funções de bibliotecas que existem somente em um único sistema 

operacional. Uma característica da linguagem Java é que programas compilados 

rodam em quase todos os sistemas de computador. 
	Linguagem assembly, por outro lado, não "tenta" ser portátil. É 

amarrada a uma família específica de processadores, então há um número de 

diferentes linguagens assembly amplamente utilizadas atualmente. Cada uma é 

baseada em cada família de processadores ou um computador específico, com nomes 

como Motorola 68x00, Intel IA-32, SUN Sparc, Vax, e IBM-370; As instruções em 

assembly correspondem à arquitetura do conjunto de instruções do computador. 

Por exemplo, a linguagem assembly ensinada neste livro funciona somente em 

processadores pertencentes a família Intel IA-32.

Por que aprender linuagem assembly? Por que não apenas ler um bom livro de 

hardware de computadores e arquitetura, e evitar ter que aprender a linguagem 

de programação assembly?

- Você deve estar trabalhando para obter uma formação em engenharia de 

computação. Se sim, há uma grande probabilidade de que você irá escrever 

programas para sistemas embarcados. Tal como programas são escritos em C, Java, 

ou linguagem assembly, e baixados em chips de computador e instalados em 

dispositivos dedicados. Alguns exemplos são sistemas de combustível e ignição 

para automóveis, sistemas de controle de ar-condicionado, sistemas de 

segurança, sistemas de voo, sistemas portáteis, modems, impressoras, e outros 

periféricos. 

...

1.1.2 Aplicações de linguagem assembly

Nos primeiros dias de programação, muitos programas eram escritos parcialmente 

ou inteiramente em linguagem assembly porque programas precisavam ocupar uma 

pequena área de memória e tinha que rodar da forma mais eficiente possível. 

Conforme computadores se tornaram mais poderosos, programas se tornaram mais 

longos e mais complexos; isso demandou o uso de linguagens de alto-nível tal 

como C, FORTRAN, e COBOL que continham uma certa capacidade de estruturação 

para auxiliar o programador. Mais recentemente, linguagens orientadas a objetos 

como C++, C#, Visual Basic e Java tem tornado possível escrever programas 

complexos contendo milhões de linhas de código. 
   É raro ver uma larga aplicação de programas escritos completamente em 

linguagem assembly porque eles podem tomar muito tempo para serem escritos e 

mantidos. (Instead), assembly é usada para otimizar certas seções de programas 

para velocidade e acesso ao hardware do computador. Assembly também é usada ao 

escrever programas para sistemas embarcados e drivers de dispositivos. A tabela 

1-1 compara a adaptabilidade da linguagem assembly e linguagens de alto-nível 

em relação a vários tipos de programas de computador. 

...

## ------------ 			Capítulo 2			--------------

#### 2.1 Conceitos gerais

Este capítulo descreve a arquitetura da família de processadores Intel IA-32 e 

seu sistema do ponto de vista de um programador. Como dissemos no primeiro 

capítulo, assembly é uma ótima ferramenta para aprender como um computador 

funciona. Este capítulo é uma parte essencial do processo de apredizado, porque 

você precisa aprender o básico do sistema da arquitetura antes da linguagem 

assembly poder ser útil.
    Nós tentamos (strike) uma balança entre conceitos que se aplicam a todos os 

sistemas de microcomputadores e informação específica sobre a família IA-32. É 

impossível saber qual tipo de sistema de computação você usará no futuro, então 

seria um erro para você aprender apenas sobre a IA-32. Por outro lado, um 

generalizado, superficial conhecimento de processadores deixaria você com um 

sentimento de vazio, sem ter uma experiência suficiente com uma única CPU e 

assembly para fazer algo útil. Para usar uma analogia imperfeita, pessoas não 

se tornam grandes cozinheiras lendo livros de receitas. Elas aprendem a 

cozinhar um pouco e então constrõem suas próprias experiências.

	Depois de ler este capítulo, você deve querer (delve further) no design 

da IA-32. Você pode começar lendo o manual da Intel: Manual para 

desenvolvedores de software para IA-32: Arquitetura Básica. Você pode baixar 

isso frátis do site da Intel (www.intel.com). ... este manual pode manter sua 

atenção por dias ou semanas. Mas não se esqueça sobre o livro que você está 

segurando em suas mãos - ele ainda tem muito a oferecer a você.

2.1.1 Design Básico de Microcomputadores

A figura 2-1 mostra o design básico de um computador hipotético. A unidade 

central de processamento (CPU) é onde os cálculos e operações lógicas tomam 

lugar. Contém um número limitado de locais de armazenamento chamados 

registradores, um clock de alta-frequência, uma unidade de controle e uma 

unidade lógica aritmética. 

    - O clock sincroniza as operações internas da cpu com outros componentes do 

sistema.
    - A unidade de controle coordena a sequência de passos envolvida em 

executar instruções de máquina.
    - A unidade lógica aritmética processa operações aritméticas tais como 

adição ou subtração, e operações lógicas como AND, OR e NOT.

    A CPU é ligada ao resto do computador via pins ligados ao socket da CPU. 

Muitos destes pins conectam ao barramento de dados, o barramento de controle e 

o barramento de endereço.
    A unidade de armazenamento de memória é onde instruções e dados são 

mantidos enquanto um programa de computador está rodando. A unidade de 

armazenamento recebe requisições por dados da CPU, transfere dados da memória 

de acesso randômico (RAM) à CPU, e transfere dados da CPU para memória.
    Um barramento é um grupo de fios paralelos que transferem dados de uma 

parte do computador para outra. O sistema de barramento de um computador 

usualmente consiste de três diferentes barramentos: o de dados, o de controle e 

o de endereço. O barramento de dados transfere instruções e dados entre a CPU e 

a memória. O barramento de controle usa sinais binários para sincronizar as 

ações entre todos os dispositivos ligados ao sistema de barramento. O 

barramento de endereço (holds) os endereços das instruções e daos quando a 

instrução sendo executada atualmente transfere dado entre a CPU e a memória.

Clock    Cada operação envolvemtno a CPU e o sistema de barramentos é 

sincronizada por um clock interno que repetidamente pulsa a uma taxa constante. 

A unidade de temo mais básica para instruções de máquina é chamada o clico de 

máquina (ou tempo de ciclo de clock), que é o tempo requerido para um pulso 

completo de clock. Na figura a seguir, um pulso de clock é (depicted) como o 

tempo entre uma descida e a próxima.

    A duração de um ciclo de clock é recíproca à velocidade do clock, medida em 

oscilações por segundo. Um clock que oscila 1 bilhão de vezes por segundo (1 

GHz), por exemplo, produz um ciclo de clock com duração de um bilionésimo de 

segundo (1 nanossegundo). 
    Uma instrução de máquina requer ao menos um ciclo de clock para ser 

executada, e algumas requirem (em excesso) de 50 clocks (a instroção de 

multiplicação no processador 8088, por exemplo). Instruções requerendo acesso 

de memória que tem  ciclos de clock vazios são chamadas estados de espera por 

causa da diferença entre a velocidade da CPU, o sistema de barramento, e 

circuitos de memória. (Pesquisa recente sugere que em um futuro próximo nós 

devemos abandonar o modelo de computação síncrona em favor de um tipo de 

operação assíncrona que não requirirá um sistema de clock.)

2.1.2 - Ciclo de execução de instrução

--- A execução de uma única instrução de máquina pode ser dividida em uma 

sequência de operações individuais chamadas o ciclo de execução de instrução. 

Quando a CPU executa uma instrução usando um operando da memória, deve calcular 

o endereço do operador, colocar o endereço no barramento de endereço, aguardar 

obter o operando da memória e "so on". ---- 

Uma única instrução de máquina não simplesmente é executada "all at once". A 

CPU tem que seguir uma sequência predefinida de etapas para executar uma 

instrução de máquina, chamada o ciclo de execução de instrução. Vamos assumir 

que o ponteiro do registrador contém o endereço da instrução que nós queremos 

executar. Aqui estão todas as etapas para executar:

1. Primeiro, a CPU tem que buscar a instrução de uma área de memória chamada 

fila de instruções. Logo após fazer isso, incrementar o ponteiro de instrução.
2. Em seguida, a CPU decodifica a instrução olhando para o seu "binary bit 

pattern". Este bit pattern deve revelar que a instrução tem operandos (valores 

de entrada). 
3. Se operandos estão envolvidos, a CPU busca os operadores dos registradores e 

da memória. Às vezes, isso envolve cálculos de endereço.
4. Depois, a CPU executa a instrução, usando o valor de operando que foi 

encontrado durante a etapa anterior. Ela também atualiza alguns status flags, 

como Zero, Carry e Overflow.
5. Finalmente, se um operando de saída faz parte da instrução, a CPU armazena o 

resultado desta execução no operando.

    Nós usualmente simplificamos este processo complicado para três etapas 

básicas: Busca, Decodificação e Execução. Um operando é um valor que pode ser 

uma entrada ou uma saída para uma operação. Por exemplo, a expressão Z = X + Y 

tem dois operadores de entrada (X e Y) e um único operador de saída (Z).
    Um diagrama de blocos mostrando um fluxo de dados de uma CPU típica é 

ilustrado na Figura 2-2. O diagrama ajuda a mostrar relações entre componentes 

que interagem durante o ciclo de execução da instrução. Para ler instruções do 

programa da memória, um endereço é colocado no barramento de endereço. Em 

seguida, o controlador de memória coloca o código requisitado no barramento de 

dados, fazendo o código disponível dentro do "code cache". O valor do ponteiro 

de instrução determina qual instrução será executada em seguida. A instrução é 

analisada pelo decodificador de instrução, causando os sinais digitais 

apropriados para serem enviados à unidade de controle, que coordena a ALU (ULA) 

e unidade de ponto-flutuante. (Although) o barramento de controle não é 

mostrado nesa figura, ele carrega sinais que usam o clock do sistema para 

coordenar a transferencia de dados entre diferentes componentes da CPU.

2.1.3 Lendo dados da memória

Como regra, computadores leem dados da memória muito mais lentamente do que 

eles acessam registradores internos. Isto ocorre porque ler um único valor da 

memória envolve quatro etapas separadas:

1. Colocar o endereço do valor que você quer ler no barramento de endereço.
2. Setar (mudar o valor do) pino de leitura do processador.
3. Esperar um ciclo de clock para os chips de memória responderem. 
4. Copiar os dados do barramento de dados para o operador de destino.

Cada uma dessas etapas geralmente requer um único ciclo de clock, uma medida de 

tempo baseada no clock que pulsa dentro do processador a uma taxa regular. CPUs 

de computadores são descritas em termo de suas velocidades de clock. Uma 

velocidade de 1.2 GHz, por exemplo, significa que o clock pulsa, ou oscila, 1.2 

bilhões de vezes por segundo. Entao, 4 ciclos de clock são muito rápidos, 

considerando cada um dos outros por apenas 1/1.200.000.000º de um segundo. 

Ainda assim, é muito lento para os registradores da CPU, que são usualmente 

acessados em apenas um ciclo de clock.
    Felizmente, designers de CPUs notaram há um bom tempo que memória de 

computadores criam um gargalo de velocidade porque a maioria dos programas tem 

que acessar variáveis. Eles começaram com uma maneira (clever) de reduzir a 

quantidade de tempo gasto lendo e escrevendo na memória - eles armazenam as 

instruções e dados mais recentemente usados em memória de alta-velocidade 

chamada cache. A ideia é que um programa é mais propenso a querer acessar a 

mesma memória e instruções repetidamente, então cache mantém esses valores onde 

eles podem ser acessados facilmente. Além disso, quando a CPU começa a executar 

um programa, ela pode ver e carregar as próximas mil instruções (por exemplo) 

na cache, assumindo que estas instruções serão necessárias em breve. Se ocorre 

de ser um loop no block de código, as mesmas instruções estarão na cache. 

Quando o processador está ábil para encontrar dados na memória cache, nós 

chamamos isso de um cache hit. Por outro lado, se a CPU tenta encontrar algo na 

cache e isso não está lá, nós chamamos isso de cache miss.
    Memória cache para a família x86 é dividida em dois tipos. Cache level-1 

(ou cache primária) é armazenada na CPU. Cache level-2 (ou cache secundária) é 

um pouco mais lenta, e conectada à CPU por barramento de alta-velocidade. O 

dois tipos de cache trabalham juntos de uma forma otimizada. 
    Há uma razão pela qual memória cache é mais rápida que a convencional RAM - 

é porque memória cache é construida de um tipo especial de memória chamado RAM 

estática. É cara, mas não tem que ser constantemente atualizada para manter o 

conteúdo. Por outro lado, memória convencional, conhecida como RAM dinâmica, 

deve ser atualizada constantemente. É muito lenta, mas barata.

2.1.4 Carregando e executando um programa

Antes de um programa poder rodar, ele deve ser carregado da memória por um 

utilitário conhecido como um carregador de programa. Após carregado, o sistema 

operacional deve apontar a CPU para o ponto de entrada do programa, que é o 

endereço onde o programa começa a ser executado. As seguinte etapas explicam 

este processo com mais detalhes:

- O sistema operacional (SO) procura pelo nome do arquivo do programa no atual 

diretório do disco. Se ele não conseguir encontrar o nome ali, procura em uma 

lista predeterminada de diretórios (chamados "paths") pelo nome do arquivo. Se 

o SO falhar na busca pelo arquivo do programa, é mostrada uma mensagem de erro.
- Se o arquivo do programa é encontrado, o SO retém informações básicas sobre o 

arquivo do programa do diretório do disco, incluindo o tamanho do arquivo e o 

endereço físico no drive de disco.
- O SO determina o próximo local disponível na memória e carrega o arquivo do 

programa na memória. Ele aloca um bloco de memória para o prorama e insere 

informação sobre o tamanho do programa e localização em um "table" (às vezes 

chamado de descriptor table). Adicionalmente, o SO deve ajustar os valores dos 

ponteiros com o programa para que eles contenham endereços de dados do 

programa.
- O SO inicia a execução da primeira instrução de máquina do programa (é um 

ponteiro de entrada). Logo que um programa começa a rodar, é chamado um 

processo. O SO associa ao processo um número de idenfificação (ID do processo), 

que é usado para mantê-lo enquanto estiver rodando.
- O processo roda por si próprio. É trabalho do SO "to track" a execução do 

processo e responder a requisições de recursos do sistema. Exemplos de recursos 

são memória, arquivos de disco, e dispositivos de entrada-saída.
- Quando o processo termina, é removido da memória.

Dica: Se você está usando alguma versão do Microsoft Windows, pressione Ctrl-

Alt-Delete e selecione o Gerenciador de Tarefas. A janela do Gerenciador de 

Tarefas mostrará a você listas das aplicações e processos. Aplicações são os 

nomes de programas completos atualmente rodando, como Windows Explorer ou 

Microsoft Visual C++. Quando você clicak na aba Processos, você vê uma longa 

lista de nomes de processos. Cada um destes processos é um pequeno programa 

rodando independentemente de todos os outros. Você pode continuamente observar 

a quantidade de tempo de CPU e memória usados por cada processo. Em alguns 

casos, você pode parar um processo selecionando seu nome e pressonando a tecla 

Delete. 

2.1.5 Seção de Revisão

1. A Unidade Central de Processamento (CPU) contem registradores e quais outros 

elementos básicos?
2. A CPU é conectada ao resto do sistema do computador usando quais três 

barramentos?
3. Por que acesso à memória leva mais ciclos de máquina do que acesso a 

registradores?
4. Quais são as três etapas básicas no ciclo de execução de instrução?
5. Quais são as duas etapas adicionais requiridas no ciclo de execução de 

instrução quando um operando da memória é utilizado?

2.2 Processadores x86 de 32 Bits

Nesta seção, nós focamos nas características básicas da arquitetura de todos os 

precessadores x86. Isso inclui membros da família Intel IA-32 e todos os 

processadores AMD de 32 bits.

2.2.1 Modos de operação

Processadores x86 possuem trêsm modos primários de operação: modo protegido, 

modo de endereçamento real (?) e modo de administração do sistema. Um sub-modo, 

chamado virtual-8086, é um caso especial do modo protegido. Aqui está uma curta 

descrição de cada um:

Modo protegido - Modo protegido é o estado nativo do processador, no qual todas 

as instruções e recursos estão disponíveis. Progamas possuem áreas separadas de 

memória chamada segmentos, e o processador previne programas de referenciar 

memória sem seus segmentos associados.

Modo Virtual-8086 - Enquanto está em modo protegido, o processador pode 

diretamente executar o software do modo de endereçamento real como programas do 

MS-DOS em um ambiente seguro. Em outras palavras, se um programa quebra ou 

(attemps) a escrever dados na área de memória do sistema, isso não afetará 

outros programas rodando ao mesmo tempo. Um sistema operacional moderno pode 

executar seções múltiplas de virtual-9086 separadas ao mesmo tempo.

Modo de endereçamento real - Modo de endereçamento real implementa o ambiente 

de programação de um processador intel com alguns recursos extras, como a 

abilidade de alternar entre outros modos. Este modo é utilizado se um programa 

requer acesso direto à memória do sistema e dispositivos de hardware.

Modo de gerenciamento de sistema - O modo de gerenciamento de sistema (em 

inglês, SMM) provê um sistema operacional com um mecanismo para funções 

implementadas com poder de gerenciamento e segurança do sistema. Estas funções 

são usualmente implementadas pelos fabricantes de computadores que customizam o 

processador para um sistema particular.

2.2.2 Ambiente básico de execução

Espaço de endereço

No modo protegido de 32 bits, uma tarefa ou programa pode endereçar um endereço 

linear com espaço de 4GBytes. Começando com o processador P6, uma técnica 

chamada extensão de endereçamento físico aceita um total de 64 GBytes de 

memória física para ser endereçado. Programas do modo de endereçamento real, 

por outro lado, podem apenas endereçar um intervalo de 1 MByte. Se o 

processador está no modo protegido e rodando múltiplos programas no modo 

virtual-8086, cada programa tem sua própria área de memória de 1-MByte.

Figura 2-3 Registradores básicos de execução de programas

Registradores básicos de execução de programas

Registradores são locais de armazenamento de alta-velocidade diretamente 

inseridos na CPU, projetados para serem acessados a uma velocidade muito mais 

alta do que a memória convencional. Quando um processo em loop é otimizado para 

velocidade, por exemplo, contadores de loop são armazenados em registradores 

(rather than) variáveis. A figura 2-3 mostra os registradores básicos de 

execução de programa. Existem oito registradores de propósito geral, seis 

registradores de segmento, um registrador de (status flags) do processador 

(EFLAGS), e um ponteiro de instrução (EIP).

Registradores de Propósito Geral - Os registradores de propósito geral são 

primeiramente usados para aritmética e movimentação de dados. Como mostrado na 

figura 2-4, os 16 bits menos significantes do registrador EAX podem ser 

referenciados usando o nome AX.

Porções de alguns registradores podem ser endereçados como valores de 8 bits. 

Por exemplo, o registrador AX tem um (upper half named) AH e um outro nome 

chamado AL. A mesma relação de (overlapping) existe para os registradores EAX, 

EBX, ECX e EDX.

[tabela]

Os registradores de propósito geral restantes podem ser acessados apenas usando 

nomes de 32 ou 16 bits, como mostra a seguinte tabela:

[Tabela]

Usos especializados - Alguns registradores de propósito geral tem usos 

específicos:

- EAX é automaticamente usado por instruções de multiplicação e divisão. Ele é 

chamado de registrador (extended accumulator).
- A CPU usa automaticamente o ECX como um contador de loop.
