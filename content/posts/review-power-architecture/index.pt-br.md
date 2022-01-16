---
title: "IBM Power Systems - Power8, Power9 and Power10"
date: 2021-12-18
draft: false
author: "Junior Santos"
authorLink: "https://jr-santos98.github.io/about/"
description: "Uma revisão sobre IBM Power Systems."
resources:
- name: "featured-image"
  src: "blog-architecture-power.png"

tags: ["Power Systems", "Power8", "Power9", "Power10"]
categories: ["Power Systems"]
---

Este post faz uma revisão sobre os processadores que compoêm o IBM Power Systems.

<!--more-->

# Instrodução

Em uma comparação entre os processadores da IBM (arquitetura Power) e os da Intel/AMD (arquitetura x86),
pode-se afirmar que a melhor opções entre eles, dependerá do seu uso.
Os chips x86 são voltados para o uso geral, apresentam boa escabilidade e alto performace em quase todos os usos.
Por outro lado, os chips Power são focados para uso de alto desempenho e alta-performace para servidores.
Tem suporte para atender demandas emengentes, têm virtualização de forma nativa,
com diversos recursos em hardware focados em virtualização, sendo a melhor escolha possível para esse tipo de trabalho.

Além disso, a arquitetura Power é focado para o ramo de negócios, possuindo planos de suporte para as diferentes atividades de negócios.
Tendo foco principal em soluções de virtualização, para atender demandas massivas de trabalho.
Ademais, os chips possuem recursos para dividir trabalhos ou reunir recursos, fazendo vários servidores se comportarem como um.

Dessa forma, a IBM torna-se uma peça fundamental para o plano de negócios de qualquer empresa ligada a tecnologia ou que precise de uma grande escalabilidade de recursos para atender a uma demanda massiva de trabalho.
Assim como principalmente para a área de computação em nuvem.

## POWER8

Power8 foi lançado pela IBM em 2014. Nele a IBM realizou diversas melhorias em relação a sua versão anterior.
As máquinas que foram criadas com esse chip, tinham a disposição de 6 á 12 núcleos, além de um clock que vária de 2.5 GHz á 5 GHz.
Power8 possui 32 KB para instruções + 64 KB para dados no cache L1, 512 KB tipo SRAM no cache L2, 96 MB do tipo eDRAM no cache L3 e 128 MB do tipo eDRAM no cache L4.

|Core|CPU|cache L1|cache L2|cache L3|cache L4|
|---|---|---|---|---|---|
| 6 á 12 | 2.5 GHz á 5 GHz | 64 KB + 32 KB | 512 KB | 96 MB | 128 MB |

Quando se fala de processadores, memória é um recurso fundamental.
A memória cache ela é mais rápida do que a memória principal (memória RAM),
por conta disso, seu tamanho é fundamental para melhor desempenho do processador. Ao comparar com a versão anterior do chip, a memória cache L3 teve seu tamanho aumentado.
Isso resultou em parte para o maior desempenho do processador em relação ao seu antecessor.

Power8 posssui muito mais recursos que o seus concorrentes x86 e seu antecessor, sendo mais poderoso que os mesmos.
Além disso, ele possui suporte para multithreading simultâneo com oito núcleos por thread (SMT-8), possuindo um grau de paralelismo muito grande.

## POWER9

Power9 foi lançado pela IBM em 2017. Essa versão conta com aprimoramento no núcleo e no hardware, o chip é menor resultando em uma otimização no consumo de energia.
O número de núcleos dubrou indo para 24, o clock foi fixado em 4 GHz.
Power9 possui 32 KB para instruções + 32 KB para dados no cache L1, 512 KB tipo SRAM no cache L2, 128 MB do tipo eDRAM no cache L3.

|Core|CPU|cache L1|cache L2|cache L3|
|---|---|---|---|---|
| 24 | 4 GHz | 32 KB + 32 KB | 512 KB | 128 MB |

O aumento do número de núcleos, somado a redução do tamanho do chip, com o aumento do cache L3, otimiza e aumenta o poder de processamento.
Power9 possui 1,5x melhor performance e 2x mais memória que Power8.

Power9 possui uma aceleração maior que suas versões anteriores, teve otimizada a leitura de memórias do tipo DDR4.
Com base na aceleração, foi possível reduzir os processos dos ciclos, o custo dos hardwares e aumentar a eficiência.

O chip foi melhorado para ter uma largura de banda mais alta e interface de baixa latência.
Essa melhoria foi obtida através de uma interface criada pela NVIDIA, chamada de NVLink.
Além disso, a arquitetura também foi otimizada para cargas de trabalho emergentes.
Aperfeiçoando seu desempanho na realização de trabalhos para computação de alto desempenho.

Todas essas melhorias foram realizadas com a perspectica de criar um processador mais otimizado para desenvolver operações de alto desempenho, de computação em nuvem, para grandes centros de dados e pesquisa.

## POWER10

Power10 foi anunciado pela IBM em 2020, com lançamento em 2021. O chip foi aprimorado para ter maior velocidade de processamento e maior capacidade para cálculos intensivos.
A quantidade de núcleos podem variar de 15 á 30, com um clock que vária de 4,5 GHz á 4 GHz.
Power10 possui 32 KB para instruções + 32 KB para dados no cache L1, 2 MB tipo SRAM no cache L2, 128 MB do tipo eDRAM no cache L3.

|Core|CPU|cache L1|cache L2|cache L3|
|---|---|---|---|---|
| 15 á 30 | 3.5 GHz á 4 GHz | 32 KB + 32 KB | 2 MB | 128 MB |

Power10 foi projetado para atingir alto grau de desempenho em padrões de criptografia já existente e em padrões de criptografia futuros.
Power10 teve implementado em seus núcleos um acelerador matemático de matriz.
Isso teve como resultado uma inferência de IA 10x, 15x, 20x mais rápido para cálculos FP32, BFloat16 e INT8, respectivamente, que em comparação com Power9.

Diversas mudanças foram realizadas em comparação com o seu antecessor.
Power10 teve seu hardware de leitura otimizado, foi adicionado suporte para as memórias DDR5,
a memória cache L2 teve a sua capacidade aumentada, além do chip que teve seu tamanho reduzido.
Essas características significam que o chip Power10 teve aumento de performance e sua otimização prepara o chip para suportar as mais novas técnologias desenvolvidas.

A IBM implementou o PowerAXON no Power10.
Ele tem a capacidade de permitir compartilhar a memória principal de um servidor Power10 com outros servidores Power10.
Este recurso pode ser utilizado para permitir que um conjunto de máquinas pequenas, consigam se torna uma grande máquina com grande poder de processamento.

Com todos os recursos das versões anteriores otimizados, com a adição de recursos inovadores e com o aumento do poder e da capacidade de processamento,
tornam esse processador o mais poderoso que a IBM já criou.
Perfeito para trabalhos de análise de dados, computação em nuvem, programação de alto desempenho e entre outros trabalhos que necessitam de máquinas atualizas e poderosas.

> O [OpenPower Lab](https://openpower.ic.unicamp.br/) não conta com servidores Power10 dentro de seu acervo.
