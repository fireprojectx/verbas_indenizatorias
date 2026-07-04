# Verbas Indenizatórias — ALMG · 20ª Legislatura

Painel web para consultar e comparar a verba indenizatória dos deputados estaduais da
Assembleia Legislativa de Minas Gerais (ALMG), com dados públicos direto da
[API de Dados Abertos da ALMG](https://dadosabertos.almg.gov.br/).

## Objetivo

A verba indenizatória é um valor pago mensalmente a cada deputado para custear despesas
do exercício do mandato (correio, combustível, hospedagem, publicidade, material de
escritório etc.). Os dados já são públicos, mas estão espalhados em centenas de páginas
individuais no portal da ALMG, o que dificulta comparar deputados entre si ou acompanhar
a evolução ao longo do tempo.

Este projeto existe para dar **mais transparência** a esse gasto público, reunindo os
dados oficiais em um único lugar e facilitando três perguntas simples que qualquer
cidadão deveria conseguir responder rapidamente:

- Quanto cada deputado(a) recebeu de verba indenizatória, em que período e em quais categorias?
- Como os deputados e os partidos se comparam entre si (ranking)?
- Quem está usando, na média mensal, mais do que o teto legal permite?

Nenhum dado é armazenado ou alterado — o site apenas consulta a API oficial da ALMG em
tempo real e apresenta o resultado de forma visual.

## O limite legal (teto mensal)

Cada deputado tem direito a reembolso de despesas indenizatórias até um **teto mensal**,
fixado pela Deliberação da Mesa da ALMG nº 2.446/2009. Esse teto foi reajustado em 16,6%
em fevereiro de 2023, passando de R$ 27.000 para R$ 31.500 por mês. A partir daí, o
cálculo passou a ser feito com base na **UFEMG** (Unidade Fiscal do Estado de Minas
Gerais): como a Secretaria de Fazenda de MG reajusta a UFEMG todo início de ano, o valor
em reais do teto sobe junto, sem depender de uma nova deliberação a cada vez.

| Ano  | UFEMG do ano | Teto mensal (aprox.) |
| ---- | -----------: | --------------------: |
| 2023 |     R$ 5,0369 |          R$ 31.500,00 |
| 2024 |     R$ 5,2797 |          R$ 33.098,53 |
| 2025 |     R$ 5,5310 |          R$ 34.587,96 |
| 2026 |     R$ 5,7899 |      **R$ 36.209,15** |

Confira o valor vigente no [portal de transparência da ALMG](https://www.almg.gov.br/transparencia/prestacao-de-contas/deputados/verba-indenizatoria/)
e as [resoluções da UFEMG (SEF/MG)](https://www.fazenda.mg.gov.br/empresas/legislacao_tributaria/resolucoes/ufemg.html)
antes de tirar conclusões — novas deliberações da Mesa podem reajustar o teto além do que
consta nesta tabela.

Um ponto importante: a norma permite que o saldo não utilizado em um mês seja acumulado
e reembolsado em meses seguintes, dentro do mesmo exercício financeiro. Por isso, a
aba **"Acima do teto"** deste painel não aponta uma irregularidade quando a média mensal
de um deputado ultrapassa o teto do ano — é apenas um indicador de acompanhamento, já
que esse acúmulo de saldo é previsto em lei.

**Não confunda com o subsídio (salário).** O subsídio dos deputados é uma rubrica
separada da verba indenizatória, com reajuste escalonado e datas próprias: R$ 25.300
até dez/2022, R$ 29.400 em jan/2023, R$ 31.200 em abr/2023, R$ 33.000 em fev/2024 e
R$ 34.700 em fev/2025. Esse escalonamento é do salário, e não se aplica ao teto da
verba indenizatória tratado neste painel, que segue a tabela acima (reajustada pela
UFEMG, não pelo mesmo cronograma do subsídio).

## Funcionalidades (abas)

- **Deputados** — busca e filtro por nome/partido; ao selecionar um deputado, mostra o
  total gasto por ano, evolução mês a mês e as categorias de despesa mais relevantes.
- **Ranking** — compara todos os deputados (e partidos) em um ou mais períodos
  escolhidos, com uma "corrida de barras" animada conforme as respostas da API chegam.
- **Acima do teto** — reaproveita o período carregado no Ranking e compara a média
  mensal de cada deputado(a) com o teto vigente no(s) ano(s) do período, destacando
  quem está acima.

Também é possível exportar em CSV tudo o que já foi consultado na sessão (botão
"Exportar CSV"), útil para análises no Excel/Power BI.

## Como usar

Este é um projeto de página única, sem build nem dependências de servidor:

1. Abra o arquivo `index.html` diretamente no navegador (ou publique-o em qualquer
   servidor estático).
2. A lista de deputados carrega automaticamente da API; se a consulta falhar, o painel
   usa uma lista local (semente) como reserva.

## Sobre a API e os limites de uso

- Fonte oficial: `https://dadosabertos.almg.gov.br/api/v2`.
- A API impõe um limite de **1 requisição por segundo**, respeitado pelo painel através
  de uma fila interna. Por isso, carregar um ano completo de um deputado leva alguns
  segundos, e um ranking de mandato completo (77 gabinetes × vários meses) pode levar
  dezenas de minutos.
- Os dados já consultados ficam em cache durante a sessão do navegador, então repetir ou
  ampliar uma consulta é instantâneo.
- Para análises longitudinais em massa (todos os meses de todos os anos de uma vez), a
  ALMG também publica arquivos CSV consolidados em
  [dadosabertos.almg.gov.br → Arquivos](https://dadosabertos.almg.gov.br/documentacao/arquivos).

## Limitações

- O painel depende inteiramente da disponibilidade e do formato de resposta da API
  pública da ALMG; instabilidades na API afetam a exibição dos dados.
- Os valores refletem apenas meses já fechados/publicados pela ALMG.
- Este projeto é independente e não possui vínculo oficial com a Assembleia Legislativa
  de Minas Gerais.
