---
title: Um comparativo entre implementações de RISC-V
date: 2023-06-26
draft: false
author: "Junior Santos"
authorLink: "https://jr-santos98.github.io/about/"
description: "Uma comparação entre as implementações para a ISA RISC-V."

tags: ["Tutorial", "Minikube", "Kubernetes"]
categories: ["Tutoriais"]
---

Este tutorial mostra como criar um cluster para processadores da arquitetura Power (ppc64/ppc64le) utilizando o Minikube.

<!--more-->

## Introdução

RISC-V é uma nova arquitetura de conjunto de instruções
(ISA) que foi criada na Universidade da Califórnia em Berkeley
como um projeto de pesquisa e educação em arquitetura
de computadores, atualmente vem ganhando cada vez
mais implementações por parte da indústria. Ela foi desenvolvida
com o objetivo de ser aberta, livre e acessível,
de forma a permitir que qualquer pessoa possa usar, modificar
e implementar a arquitetura sem restrições ou custos
adicionais. A ISA foi projetada para suportar espaços de endereçamento
de 32 bits, 64 bits e 128 bits, visando aumentar a
sua adoção. Essa flexibilidade permite que a arquitetura RISCV
seja utilizada em uma ampla variedade de aplicações, desde
dispositivos de baixo consumo de energia até sistemas de alto
desempenho. Ao suportar diferentes tamanhos de palavra,
a ISA RISC-V oferece maior versatilidade para atender às
necessidades específicas de cada projeto, permitindo um uso
eficiente dos recursos disponíveis. Essa abordagem modular
contribui para a popularidade e a crescente aceitação da
arquitetura RISC-V em diversas indústrias e setores.

RISC-V é uma arquitetura que permite que qualquer pessoa
ou organização crie suas próprias implementações. Devido
a esse fato, este blog tem como objetivo apresentar e
comparar as principais implementações.

## Implementações

Para a escolha das implementações a serem apresentadas,
foram pesquisadas implementações robustas e avançadas, que fossem
capazes de executar um SO (Sistema Operacional) em uma FPGA.
Para este cenário foram escolhidas:
Ariane (CVA6)[4], Boomv3[5], Rocket[1] e Shakti[2].

### Rocket Chip

É uma implementação de processador escalar em ordem de 5 estágios.
Foi desenvolvido na Universidade da Califórnia (UC) em Berkeley.
Sua implementação é a primeira, e serve como referência, biblioteca
e plataforma de testes para o conjunto de instruções (ISA) RISCV.

#### Pipeline

![Pipeline do Rocket Chip](caminho_da_imagem.jpg "Pipeline do Rocket Chip")

Possui um pipeline clássico de 5 estágios, sem muitas
alterações ou modificações aparente.
Possui uma cache de dados que pode ser bloqueante ou não,
as caches L1 e L2 são configuraveis,
a previsão de branch é configurável 
e fornecida por um buffer de destino de ramificação (BTB),
tabela de histórico de ramificação (BHT)
e uma pilha de endereços de retorno (RAS).
Ainda possui Buffer de Pesquisa de Tradução (TLB) de dados e de
instruções, para melhorar o desempenho geral do sistema.

### BOOMv3 (SonicBOOM)

É um projeto aberto desenvolvido pela UC em Berkeley.
Trata-se de um processador superescalar fora de ordem de
alto desempenho. 
Possui um pipeline de 10 estágios com uma penalidade de 12 ciclos
para misprediction.
Trata-se de um projeto ambicioso dedicado a computação de alto
desempenho, voltado para o mercado de clusters e servidores.

#### Pipeline

![Pipeline do BOOM](caminho_da_imagem.jpg "Pipeline do BOOM")

Possui um pipeline complexo e robosto, configurável
e personalizável.
Possui TLB para instruções, 
preditores complexos de dois níveis baseados em vetores de histórico
global (chamados de GShare ou TAGE, dependendo de sua versão). 
O BOOM oferece suporte à especulação de ramificação completa usando
um BTB, TLB e RAS.
O uBTB (às vezes chamado de "next-line-predictor" ou "L0 BTB"),
uma versão simplificado do BTB,
redireciona o PC em um único ciclo de um pequeno buffer totalmente
associativo de destinos de ramificação, melhorando drasticamente
a taxa de transferência em pequenos loops.

### Ariane (CVA6)

Implementação desenvolvida pelo grupo HW, uma organização global
dedicada a criação de hardwares livres.
O CVA6 trata-se de um processador escalar fora de ordem com
um pipeline de 6 estágios.
Pode ser comparado ao pipeline Rocket de 5 estágios
com um estágio adicional para o Program Counter (PC).
Ou melhor, ele trata o processo de PC como uma fase do
pipeline.

#### Pipeline

![Pipeline do Ariane - CVA6](caminho_da_imagem.jpg "Pipeline do Ariane - CVA6")

Ele possui tamanho configurável e TLBs separados.
Implementa um PTW (Caminhador da Tabela de Páginas)
em nível de hardware, que é acionado sempre que um endereço
não é encontrado na TBL, seu papel é consultar a memória principal,
realizar a tradução do endereço e adicionar na TBL.
o Ariane contém três meios diferentes de prever o próximo PC,
ou seja, uma tabela de histórico de ramificação (BHT),
buffer de destino de ramificação (BTB)
e pilha de endereço de retorno (RAS).

### Shakti Classe C

SHAKTI é uma iniciativa open-source do Instituto Indiano
de Tecnologia de Madras.
Classe C é um membro da família de processadores SHAKTI.
O processador escalar apresenta um pipeline de 5 estágios em ordem,
sendo o mais avançado da linha de processadores.

#### Pipeline

![Pipeline do Shakti Classe C](caminho_da_imagem.jpg "Pipeline do Shakti Classe C")

Com base nas implementações anteriores, esta apresenta as
caracteristicas mais básicas entre as citadas.
Pipeline simples, e estruturas clássicas aplicadas.
Possui predição de branch através de BTB, BHT e RAS,
apresenta caches L1 separados, assim como TLB associativas separadas.
Assim como as anteriores, configurável e com parametros ajustáveis.

## Comparação

tabela

Utilizando como parametro a quantidade de MIPS relatada,
a literatura considera que BOOM lidera o critério de desempenho
por MHz e ultrapassa todos os outros em mais de um fator de 2.
Seguido por Rocket, SHAKTI e CVA6 seguem na ordem mencionada.

BOOM também se destaca como sendo a implementação mais complexa,
com maior área e consumo. Tudo isso deve-se ao fato, da sua
estrutura superescalar, paralelismo e capacidade de execução.

Ao olhar para para

## Conclusão

Todas as implementações têm suas vantagens e desvantagens,
elas atendem a públicos diferentes com necessidades diferentes.

A implementação Rocket se destaca pelo pionerismo, simplicidade e
eficiência. Foi a primeira implementação, serve como debugguer da ISA,
molde e referência no surgimento de novas placas.
Assim como, queridinha das publicações e da academia.

BOOM, se destaca por ser a implementação mais robosta e eficiente.
Voltada para a computação de alto desempenho e suas necessidades.

Ariane por sua vez, se destaca pelo tamanho e consumo.
Projetada para atender a requisitos de
desempenho e eficiência energética.

Por fim, o núcleo Shakti é projetado para sistemas de computação
de médio porte e possui características adequadas para essa finalidade.
Ela é simples e eficiente.

## Referências

[1] Krste Asanović et al.2016.The Rocket Chip Generator. TechnicalReport UCB/EECS-2016-17. Department of Electrical Engineering &Computer Sciences, University of California, Berkeley, CA, USA.

[2] Gurajala Bhavitha Chowdary. 2022.Set Associative Data TLB for ShaktiC-Class Processor. Ph. D. Dissertation. Indian Institute of TechnologyMadras.

[3] Alexander Dörflinger, Mark Albers, Benedikt Kleinbeck, Yejun Guan,Harald Michalik, Raphael Klink, Christopher Blochwitz, Anouar Nechi,and Mladen Berekovic. 2021.  A comparative survey of open-sourceapplication-class RISC-V processor implementations. InProceedings ofthe 18th ACM International Conference on Computing Frontiers. ACM. https://doi.org/10.1145/3457388.3458657

[4] Florian Zaruba and Luca Benini. 2019. The Cost of Application-ClassProcessing: Energy and Performance Analysis of a Linux-Ready 1.7-GHz 64-Bit RISC-V Core in 22-nm FDSOI Technology.IEEE Transac-tions on Very Large Scale Integration (VLSI) Systems27, 11 (nov 2019),2629–2640. https://doi.org/10.1109/tvlsi.2019.2926114

[5] Jerry Zhao, Ben Korpan, Abraham Gonzalez, and Krste Asanovic. 2020.SonicBOOM: The 3rd Generation Berkeley Out-of-Order Machine.Fourth Workshop on Computer Architecture Research with RISC-V(May2020).
