# Python no CallCenter

## Objetivo da Apresentação
Muito tem se falado nas várias funcionalidades do Python como linguagem de programação e de seus potenciais, 
mas, sinto a necessidade de demonstrar a versatilidade inerente do Python em termos de resolução de problemas
reais numa empresa real de Callcenter, a qual tem diversas necessidades de escalabilidade, fluxo de dados e confiabilidade nos 
seus processos internos.

Ou seja, nessa apresentação eu irei falar sobre como aplicamos as técnicas do python em problemas reais e não nas técnicas em si

## Quem sou Eu?
Meu nome é Guilherme Bencke, e sou formado em Ciência da Computação pela ULBRA em 2003, programo desde 1986 e profissionalmente
desde 1998. 

Já trabalhei com dezenas de linguagens e tecnologias em projetos tanto para o Brasil, quanto EUA e França.

Atualmente (Dependendo do Dia) sou Desenvolvedor / Líder Técnico e Gerente de Desenvolvimento de Software.

## Funciona um CallCenter
Um CallCenter, ou Contact Center, é uma empresa especializada em prestar o serviço de receber um conjunto de dados sobre pessoas
a serem contactadas e realizar uma série de ações de contato com essas pessoas. 

A Zanc é uma empresa de CallCenter de Cobrança em que o objetivo do contato é o pagamento de uma dívida que um cliente tem com 
alguma empresa conveniada a Zanc para a cobrança dessa dívida. O Fluxo dos dados na empresa é basicamente o abaixo:

## Desafios nos Fluxos de Dados
Basicamente um CallCenter enriquece, filtra, segmenta, gera listas de contato e executa esses contatos. Atualmente existem
diversos desafios no dia a dia da empresa, principalmente relacionado com:
* Recepção de Dados: A Zanc atende em torno de 40 convênios através de 4 CRMs e usando 2 Discadores, cada um desses convênios
disponibiliza diariamente dados atualizados para contato para cada um dos clientes a serem acionados. Em geral, esses dados vem 
em diversos formatos de texto, que podem ser mudados de uma hora para outra pela empresa conveniada, e muitas vezes sem nenhum
aviso, e os nossos CRMs dependem de um tamanho de formato de importação relativamente fixo. Essa atividade de recepção de dados
é realizada por pessoas sem formação técnica em programação ou processamento de dados.

## Desafios nos Fluxos de Dados (2)
* Analise de Dados: Telefonia é o segundo maior gasto de uma empresa de callcenter, então na realidade o lucro da empresa é minimizar
o custo com telefonia, ou seja, apenas ligar para pessoas em que realmente esse contato possa surtir efeito. Para tanto, existe um setor 
de Analise de Dados que prioriza os clientes a serem acionados e os que não serão acionados. As pessoas que executam essa análise não tem
formação em processsamento de dados ou programação.
* Localizacao de Clientes: Como utilizamos diversas ferramentas de CRM e discadores, existe uma dificuldade imensa de consolidar os dados
sobre cada um dos CPFs na base de dados, uma vez que um cliente pode estar devendo para várias empresas conveniadas ao mesmo tempo, e a 
informação de acionamento de um CRM pode e deve ser usada por outro CRM de outro convênio.

## Porque Python?
Podemos ver que a maior parte dos fluxos de dados dentro da empresa tem a necessidade de pequenos ajustes de programação diários e que
devem ser feitos no momento em que o problema é detectado.

A Empresa sempre usou bastante .NET e PHP nos seus processos internos, mas, existe a necessidade de treinar pessoas sem formação em 
programação para que programassem pequenos programas para pequenos tratamentos de arquivos e de ajustes em dados ou analises.

Nesse quesito de ser uma linguagem de facil aprendizado, versatil tanto na parte de analise de dados, como tratamento deles, além de 
possibilidade de servir web e rodar em qualquer plataforma, fez com que selecionassemos o python como "lingua franca" da empresa.

Atualmente todos os futuros desenvolvimentos de sofware da empresa são feitos em python.

## Python na Recepcao de Dados
A Vasta maioria dos dados é recepcionado por arquivos de texto, esses arquivos de texto são recepcionados por FTP em diversos formatos como
CSV, delimitado, campo fixo entre outros. Esses arquivos tem em geral centenas de campos que podem mudar de uma hora para outra. Também existe
muitas vezes a necessidade de se cruzar dados com os que estão no banco de dados do CRM pois algumas empresas conveniadas mandam dados duplicados
ou em ordem errada, oque é necessário fazer uma validação interna antes da carga.

Antes de 2017 diversas pessoas importavam esses arquivos em excel, e gastavam dias para processa-los e valida-los.  
Decidimos criar um treinamento interno de python para treinar pessoas, que não conheciam programação para que possam abrir os arquivos de texto
e realizar as validações necessárias, inclusive acessando os dados no banco de dados do CRM. E atualmente mesmo quando a necessidade de ajustes
no tratamento dos arquivos, essa operação leva algumas horas em vez de alguns dias.

Esse treinamento está disponível no github: 
https://github.com/gbencke/PythonFlatFilesProcessingCourse

Importante Salientar que as pessoas que realizaram esse curso jamais tinham programado antes.

## Python na Analise dos Dados
Uma vez carregado os dados para dentro do CRM, é necessário que se faça a análise de quais clientes serão acionados ou não, oque gera o arquivo
de mailing que é carregado no discador que efetua as ligações, uma vez o cliente atendendo, essa ligação é passada para um atendente que efetua o contato.

Essa é uma área rica para machine learning, pois é necessário encontrar os padrões que melhor definem os clientes potenciais e gerar um score.

Para isso, o Python tem nos ajudado no sentido de usar a biblioteca XGBoost que cria arvores de decisão que geram um score de diversas variáveis com a 
probrabilidade do cliente atender o telefone, a probabilidade dele honrar os pagamentos, entre outros. Antes usavamos R para isso, mas, nosso conhecimento
com R era limitado a poucas pessoas.

Temos 2 projetos piloto utilizando python para machine learning nessa area:
Herval Deep Mailing - https://github.com/gbencke/HervalDeepMailing - Para cálculo de propensão de pagamentos da carteira Herval (Usando XGBoost)
Deep Mailing - https://github.com/gbencke/DeepMailing - Para cálculo de probabilidade de atendimento de ligação da carteira ITAUCARD (Usando XGBoost)

## Python na Localizacao
Como falamos anteriormente, um cliente pode estar em diversos convenios ao mesmo tempo, então é fundamental que as ocorrencias entre os CRMs sejam compartilhados.
Isso é extremamente crítico no caso da localização de telefones onde um cliente pode ter 5 telefones num CRM que atende uma empresa, mas, o mesmo cliente pode
estar cadastrado em outro CRM de outro Convênio com outros telefones. E existe uma oportunidade de economia se não discamos os telefones de um cliente num CRM, se
sabemos que esse cliente já foi discado por outro CRM em outro convênio

Para resolver isso temos uma base de localização com todas as ligações efetuadas por todos os CRMs e para todos os telefones de todos os clientes. Atualmente essa
base tem em torno de 500 milhoes de ligacoes com milhoes de telefones cadastrados.

A Solução original era acesso direto ao banco por stored procedures em postgres, oque era pesado, não era escalável e tinha diversos problemas com a modelagem de dados
feito.

Essa aplicação está sendo rescrita usando banco de dados postgresql, mas, com um web server tornado usando o async do python 3.6, uma vez que todas as ligações de toda
a empresa são cadastradas nessa base é possível ter milhares de conexões e atualizações simultâneas, oque o async nos pareceu a melhor solução.

## Discador
Mas, o principal impacto que a utilização do python na nossa empresa trouxe foi no discador, que é o software que realiza a ligação ao cliente final, que identifica se
ocorreu o alô dele, e passa para um operador para realizar a ligação. 

Nossa solução atual foi feita em 2005, em .NET, mas, infelizmente com o tempo se mostrou inadequada e estamos trocando a arquitetura da discagem em si de .NET para python, oque 
veremos nos próximos slides.

## Aqui vai o Multcall
