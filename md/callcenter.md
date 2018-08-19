# Python no CallCenter

## Objetivo da Apresenta��o
Muito tem se falado nas v�rias funcionalidades do Python como linguagem de programa��o e de seus potenciais, 
mas, sinto a necessidade de demonstrar a versatilidade inerente do Python em termos de resolu��o de problemas
reais numa empresa real de Callcenter, a qual tem diversas necessidades de escalabilidade, fluxo de dados e confiabilidade nos 
seus processos internos.

Ou seja, nessa apresenta��o eu irei falar sobre como aplicamos as t�cnicas do python em problemas reais e n�o nas t�cnicas em si

## Quem sou Eu?
Meu nome � Guilherme Bencke, e sou formado em Ci�ncia da Computa��o pela ULBRA em 2003, programo desde 1986 e profissionalmente
desde 1998. 

J� trabalhei com dezenas de linguagens e tecnologias em projetos tanto para o Brasil, quanto EUA e Fran�a.

Atualmente (Dependendo do Dia) sou Desenvolvedor / L�der T�cnico e Gerente de Desenvolvimento de Software.

## Funciona um CallCenter
Um CallCenter, ou Contact Center, � uma empresa especializada em prestar o servi�o de receber um conjunto de dados sobre pessoas
a serem contactadas e realizar uma s�rie de a��es de contato com essas pessoas. 

A Zanc � uma empresa de CallCenter de Cobran�a em que o objetivo do contato � o pagamento de uma d�vida que um cliente tem com 
alguma empresa conveniada a Zanc para a cobran�a dessa d�vida. O Fluxo dos dados na empresa � basicamente o abaixo:

## Desafios nos Fluxos de Dados
Basicamente um CallCenter enriquece, filtra, segmenta, gera listas de contato e executa esses contatos. Atualmente existem
diversos desafios no dia a dia da empresa, principalmente relacionado com:
* Recep��o de Dados: A Zanc atende em torno de 40 conv�nios atrav�s de 4 CRMs e usando 2 Discadores, cada um desses conv�nios
disponibiliza diariamente dados atualizados para contato para cada um dos clientes a serem acionados. Em geral, esses dados vem 
em diversos formatos de texto, que podem ser mudados de uma hora para outra pela empresa conveniada, e muitas vezes sem nenhum
aviso, e os nossos CRMs dependem de um tamanho de formato de importa��o relativamente fixo. Essa atividade de recep��o de dados
� realizada por pessoas sem forma��o t�cnica em programa��o ou processamento de dados.

## Desafios nos Fluxos de Dados (2)
* Analise de Dados: Telefonia � o segundo maior gasto de uma empresa de callcenter, ent�o na realidade o lucro da empresa � minimizar
o custo com telefonia, ou seja, apenas ligar para pessoas em que realmente esse contato possa surtir efeito. Para tanto, existe um setor 
de Analise de Dados que prioriza os clientes a serem acionados e os que n�o ser�o acionados. As pessoas que executam essa an�lise n�o tem
forma��o em processsamento de dados ou programa��o.
* Localizacao de Clientes: Como utilizamos diversas ferramentas de CRM e discadores, existe uma dificuldade imensa de consolidar os dados
sobre cada um dos CPFs na base de dados, uma vez que um cliente pode estar devendo para v�rias empresas conveniadas ao mesmo tempo, e a 
informa��o de acionamento de um CRM pode e deve ser usada por outro CRM de outro conv�nio.

## Porque Python?
Podemos ver que a maior parte dos fluxos de dados dentro da empresa tem a necessidade de pequenos ajustes de programa��o di�rios e que
devem ser feitos no momento em que o problema � detectado.

A Empresa sempre usou bastante .NET e PHP nos seus processos internos, mas, existe a necessidade de treinar pessoas sem forma��o em 
programa��o para que programassem pequenos programas para pequenos tratamentos de arquivos e de ajustes em dados ou analises.

Nesse quesito de ser uma linguagem de facil aprendizado, versatil tanto na parte de analise de dados, como tratamento deles, al�m de 
possibilidade de servir web e rodar em qualquer plataforma, fez com que selecionassemos o python como "lingua franca" da empresa.

Atualmente todos os futuros desenvolvimentos de sofware da empresa s�o feitos em python.

## Python na Recepcao de Dados
A Vasta maioria dos dados � recepcionado por arquivos de texto, esses arquivos de texto s�o recepcionados por FTP em diversos formatos como
CSV, delimitado, campo fixo entre outros. Esses arquivos tem em geral centenas de campos que podem mudar de uma hora para outra. Tamb�m existe
muitas vezes a necessidade de se cruzar dados com os que est�o no banco de dados do CRM pois algumas empresas conveniadas mandam dados duplicados
ou em ordem errada, oque � necess�rio fazer uma valida��o interna antes da carga.

Antes de 2017 diversas pessoas importavam esses arquivos em excel, e gastavam dias para processa-los e valida-los.  
Decidimos criar um treinamento interno de python para treinar pessoas, que n�o conheciam programa��o para que possam abrir os arquivos de texto
e realizar as valida��es necess�rias, inclusive acessando os dados no banco de dados do CRM. E atualmente mesmo quando a necessidade de ajustes
no tratamento dos arquivos, essa opera��o leva algumas horas em vez de alguns dias.

Esse treinamento est� dispon�vel no github: 
https://github.com/gbencke/PythonFlatFilesProcessingCourse

Importante Salientar que as pessoas que realizaram esse curso jamais tinham programado antes.

## Python na Analise dos Dados
Uma vez carregado os dados para dentro do CRM, � necess�rio que se fa�a a an�lise de quais clientes ser�o acionados ou n�o, oque gera o arquivo
de mailing que � carregado no discador que efetua as liga��es, uma vez o cliente atendendo, essa liga��o � passada para um atendente que efetua o contato.

Essa � uma �rea rica para machine learning, pois � necess�rio encontrar os padr�es que melhor definem os clientes potenciais e gerar um score.

Para isso, o Python tem nos ajudado no sentido de usar a biblioteca XGBoost que cria arvores de decis�o que geram um score de diversas vari�veis com a 
probrabilidade do cliente atender o telefone, a probabilidade dele honrar os pagamentos, entre outros. Antes usavamos R para isso, mas, nosso conhecimento
com R era limitado a poucas pessoas.

Temos 2 projetos piloto utilizando python para machine learning nessa area:
Herval Deep Mailing - https://github.com/gbencke/HervalDeepMailing - Para c�lculo de propens�o de pagamentos da carteira Herval (Usando XGBoost)
Deep Mailing - https://github.com/gbencke/DeepMailing - Para c�lculo de probabilidade de atendimento de liga��o da carteira ITAUCARD (Usando XGBoost)

## Python na Localizacao
Como falamos anteriormente, um cliente pode estar em diversos convenios ao mesmo tempo, ent�o � fundamental que as ocorrencias entre os CRMs sejam compartilhados.
Isso � extremamente cr�tico no caso da localiza��o de telefones onde um cliente pode ter 5 telefones num CRM que atende uma empresa, mas, o mesmo cliente pode
estar cadastrado em outro CRM de outro Conv�nio com outros telefones. E existe uma oportunidade de economia se n�o discamos os telefones de um cliente num CRM, se
sabemos que esse cliente j� foi discado por outro CRM em outro conv�nio

Para resolver isso temos uma base de localiza��o com todas as liga��es efetuadas por todos os CRMs e para todos os telefones de todos os clientes. Atualmente essa
base tem em torno de 500 milhoes de ligacoes com milhoes de telefones cadastrados.

A Solu��o original era acesso direto ao banco por stored procedures em postgres, oque era pesado, n�o era escal�vel e tinha diversos problemas com a modelagem de dados
feito.

Essa aplica��o est� sendo rescrita usando banco de dados postgresql, mas, com um web server tornado usando o async do python 3.6, uma vez que todas as liga��es de toda
a empresa s�o cadastradas nessa base � poss�vel ter milhares de conex�es e atualiza��es simult�neas, oque o async nos pareceu a melhor solu��o.

## Discador
Mas, o principal impacto que a utiliza��o do python na nossa empresa trouxe foi no discador, que � o software que realiza a liga��o ao cliente final, que identifica se
ocorreu o al� dele, e passa para um operador para realizar a liga��o. 

Nossa solu��o atual foi feita em 2005, em .NET, mas, infelizmente com o tempo se mostrou inadequada e estamos trocando a arquitetura da discagem em si de .NET para python, oque 
veremos nos pr�ximos slides.

## Aqui vai o Multcall
