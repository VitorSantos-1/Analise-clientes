# Inteligência de Receita & Perfil de Clientes

Relatório desenvolvido em **Power BI** para a análise de receita e do comportamento de clientes de
uma rede varejista. O painel dá visibilidade ao ticket médio, ao faturamento por segmento, aos
hábitos de consumo e à recompra, apoiando decisões de relacionamento, retenção e expansão de receita.

---

## Visão Geral

A solução estrutura o histórico transacional e o cadastro de clientes em um modelo dimensional e
entrega uma leitura clara de quem compra, quanto compra e com que frequência. O objetivo é sair da
visão puramente agregada de faturamento e enxergar a receita pela ótica do cliente — base para
qualquer estratégia de retenção e crescimento.

> **Nota de confidencialidade:** todos os dados exibidos no arquivo `.pbix` são fictícios e
> anonimizados, criados exclusivamente para demonstração de portfólio.

---

## Contexto de Negócio

No varejo, é comum acompanhar o faturamento total e ignorar sua composição por cliente. Isso esconde
riscos e oportunidades: uma parcela pequena da base costuma sustentar a maior parte da receita
(curva ABC), e quedas de frequência de compra sinalizam evasão antes que ela apareça no faturamento.
Sem essa leitura, ações de retenção e de aumento de ticket ficam no escuro.

Este painel torna visível o perfil de consumo da base — ticket médio, recorrência, segmentação por
volume e distribuição geográfica — permitindo focar esforço onde ele gera mais retorno.

## O Problema que Resolve

- **Receita analisada só no agregado**, sem enxergar a contribuição por cliente.
- **Clientes de alto valor não identificados** (ausência de curva ABC de clientes).
- **Evasão silenciosa:** queda de frequência não percebida a tempo.
- **Ações de retenção genéricas**, sem segmentação por comportamento.

## Público e Decisões Apoiadas

- **Comercial / Relacionamento:** prioriza retenção dos clientes que sustentam o faturamento.
- **Marketing:** segmenta campanhas por comportamento e volume de compra.
- **Diretoria:** acompanha ticket médio e a saúde da base de clientes.

## Impacto e Valor Gerado

Revelou ticket médio, recompra e curva ABC de clientes, permitindo focar a retenção nos clientes
que sustentam o faturamento e agir cedo sobre quedas de frequência — protegendo receita recorrente
e orientando o esforço comercial.

---

## Arquitetura de Dados e Abordagem Técnica

### Fontes de dados
- **Histórico de transações** (vendas por cliente e período).
- Cadastro de **clientes** (atributos de segmentação).

### Transformação (Power Query / M)
Limpeza e estruturação do histórico transacional, padronização de cadastros de clientes, cálculo de
intervalos entre compras e criação das faixas de segmentação por volume. O tratamento é feito na
camada de consulta para manter o modelo coeso.

### Modelagem dimensional (Star Schema)
- **Fato Transações** — grão de venda por cliente / data.
- **Dimensão Cliente** — atributos e segmento.
- **Dimensão Calendário** — base das análises de frequência e recorrência.

### Principais medidas (DAX) — lógica implementada

```DAX
Faturamento Total = SUM( FatoTransacoes[Valor] )
Clientes Ativos   = DISTINCTCOUNT( FatoTransacoes[ClienteID] )
Ticket Medio      = DIVIDE( [Faturamento Total], [Clientes Ativos] )
Frequencia Media  = DIVIDE( COUNTROWS( FatoTransacoes ), [Clientes Ativos] )
% Recompra        = DIVIDE( [Clientes com 2+ Compras], [Clientes Ativos] )
```

> As fórmulas descrevem a lógica de cálculo do relatório e servem como referência de leitura do modelo.

---

## Indicadores e Análises (KPIs)

- **Faturamento Total & Ticket Médio:** gasto médio por cliente e volume bruto de vendas.
- **Distribuição por Categoria de Cliente:** segmentação da base pelo volume financeiro de compras.
- **Frequência & Recorrência:** intervalo médio entre compras e retenção da base.
- **Vendas por Região & Canal:** distribuição geográfica da receita e performance de canais.

## Estrutura de Páginas do Relatório

1. **Visão de Receita** — faturamento, ticket médio e clientes ativos.
2. **Perfil de Clientes** — curva ABC e segmentação por volume.
3. **Frequência & Recompra** — recorrência e retenção da base.

## Como Visualizar

O relatório é apresentado pelas imagens da seção **Prints** abaixo, que reproduzem as páginas
principais do painel. O arquivo-fonte (`.pbix`) não é versionado neste repositório por conter o
modelo de dados; pode ser disponibilizado sob solicitação para avaliação técnica.

## Estrutura de Arquivos

```text
README.md    -> Documentacao do projeto (contexto de negocio + arquitetura tecnica)
docs/        -> Prints das paginas do relatorio
.gitignore   -> Exclui binarios (.pbix) e planilhas de trabalho do versionamento
```

## Prints

As imagens abaixo apresentam as páginas principais do relatório — a imagem é o que comunica o
projeto de forma imediata. Os prints serão adicionados na pasta `docs/`.

<!-- Descomente ao adicionar a imagem:
![Visao de receita e perfil de clientes](docs/print-1.png)
-->

## Autor

Vitor Santos — Análise de Dados e Inteligência Comercial (Varejo).
