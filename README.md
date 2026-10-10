# Limpeza de dados: preços de combustíveis no RS﻿

Projeto de limpeza e padronização de dados públicos da ANP, feito em Python com pandas. O objetivo foi pegar um arquivo nacional grande, recortar o Rio Grande do Sul e entregar tabelas prontas para análise.

## Fonte dos dados

Série Histórica de Preços de Combustíveis e de GLP, publicada pela ANP no Portal de Dados Abertos. Arquivo usado: Combustíveis Automotivos, 1º semestre de 2026 (atualizado em 03/07/2026).

Link: https://dados.gov.br/dados/conjuntos-dados/serie-historica-de-precos-de-combustiveis-e-de-glp

O arquivo original não está no repositório por causa do tamanho. Para rodar o notebook, baixe o CSV no link acima e coloque dentro de uma pasta chamada `dados-originais`.

## Problemas encontrados

- O arquivo tinha 422.418 linhas e 16 colunas, cobrindo o país inteiro. Recortei o RS, que ficou com 31.015 linhas.
- A coluna `Valor de Compra` estava 100% vazia.
- A coluna `Complemento` tinha 326.259 vazios no país (cerca de 77%), porque a maioria dos postos não tem complemento de endereço.
- O preço (`Valor de Venda`) vinha como texto, com vírgula decimal.
- A data da coleta vinha como texto.
- Havia 6 linhas duplicadas exatas (mesmo posto, produto, data e preço).
- O GNV é vendido em R$/m³ e os demais combustíveis em R$/litro, então misturá-los distorceria qualquer média de preço.

## O que foi feito

- Filtrei o estado do RS.
- Padronizei os nomes das colunas (minúsculas, sem espaços e sem traços).
- Removi a coluna `valor\_de\_compra`, sem nenhum valor.
- Converti `valor\_de\_venda` para número e `data\_da\_coleta` para data.
- Removi as 6 linhas duplicadas.
- Separei o GNV em um arquivo próprio, por causa da unidade de medida.
- Mantive `complemento` vazio onde não havia informação, sem preencher nada.
- Verifiquei maiúsculas, espaços e grafias em município, revenda, bandeira, produto e rua. O texto já vinha padronizado, então não alterei.
- Conferi os preços por produto e não encontrei valores impossíveis.

## O que mudou

| Item | Antes | Depois |

\|---|---|---|

| Linhas (RS) | 31.015 | 31.009 após remover duplicados |

| Linhas nos combustíveis líquidos | 31.009 | 30.513 (496 de GNV em arquivo separado) |

| Colunas | 16 | 15 |

| Duplicados exatos | 6 | 0 |

| Preço | texto com vírgula | número |

| Data | texto | data (02/01/2026 a 30/06/2026) |

## Arquivos

- `limpeza\_combustiveis\_rs.ipynb`: notebook com todo o processo, do diagnóstico à exportação.
- `dados-limpos/combustiveis\_liquidos\_rs\_2026\_01.csv` e `.xlsx`: gasolina, gasolina aditivada, etanol, diesel e diesel S10 no RS.
- `dados-limpos/gnv\_rs\_2026\_01.csv`: GNV no RS, em R$/m³.

## Como rodar

1. Baixe o CSV da fonte e coloque na pasta `dados-originais`.
1. Abra o notebook a partir da pasta do projeto.
1. Execute todas as células (Kernel, Restart Kernel and Run All Cells).

## Ferramentas

Python, pandas, Jupyter Notebook.
