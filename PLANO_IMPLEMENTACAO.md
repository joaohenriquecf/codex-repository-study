# Plano de Implementação — Lote em Dia

## 1. Objetivo

Construir uma aplicação web responsiva para pequenos varejistas acompanharem produtos por lote e validade, identificarem perdas iminentes e registrarem ações sobre o estoque.

O projeto contém frontend Angular 21 com rotas ainda vazias, backend Spring Boot 4 / Java 21 com Spring MVC e Spring Data JPA, banco H2 para desenvolvimento e protótipos de visão geral, lista, detalhe/saída e cadastro de lote em `stitch_lote_em_dia/`. O design system está em `stitch_lote_em_dia/lote_em_dia_design_system/DESIGN.md`.

## 2. Escopo funcional do MVP

1. Cadastrar e consultar produtos.
2. Registrar lotes vinculados a produtos, com código, quantidade e validade.
3. Listar e filtrar lotes por produto, situação e proximidade do vencimento.
4. Consultar detalhes e registrar saídas ou descartes, mantendo histórico.
5. Exibir visão geral com indicadores de estoque e alertas de validade.
6. Classificar validade: vencido (data anterior à data local atual), urgente (0–7 dias), atenção (8–30 dias) e em dia (mais de 30 dias). “Sem estoque” é um indicador independente, pois pode coexistir com qualquer situação de validade.

## 3. Fases de implementação

### Fase 0 — Alinhamento e fundação

- Revisar protótipos e mapear navegação, componentes e campos.
- Confirmar regras de negócio, contratos da API, erros, filtros e paginação.
- Definir execução local, CORS/proxy, decisões arquiteturais e convenções.
- Registrar as decisões iniciais na seção **Decisões do MVP** abaixo.

**Saída:** regras e contratos iniciais registrados.

### Fase 1 — Domínio e persistência

Implementar Produto (nome, descrição opcional, código de barras opcional, unidade e situação), Lote (produto, código, validade, quantidade inicial/disponível e datas) e Movimentação (lote, tipo, quantidade, data/hora e observação).

Aplicar validação de quantidades, impedir saídas acima do saldo, manter saldo e histórico de forma transacional, validar duplicidade de código no escopo definido e criar índices necessários. Usar migrações versionadas; H2 permanece como banco local até definição do ambiente de produção.

### Fase 2 — API REST

Organizar controllers, serviços, repositórios, entidades e DTOs, sem expor entidades JPA diretamente.

- `GET/POST /api/produtos`, `GET/PUT /api/produtos/{id}`
- `GET/POST /api/lotes`, `GET /api/lotes/{id}`
- `POST /api/lotes/{id}/movimentacoes`
- `GET /api/dashboard`

Validar entradas, padronizar erros, paginar listas, ordenar lotes por validade ascendente e calcular validade no backend. Documentar exemplos e limitar CORS às origens configuradas.

### Fase 3 — Estrutura e identidade visual do frontend

Substituir a tela padrão do Angular, criar rotas para visão geral, lotes, produtos e configurações e implementar navegação responsiva. Aplicar tokens do design system e componentes reutilizáveis para status, cards, formulários, alertas, carregamento e estados vazios. Garantir foco visível, rótulos acessíveis e alvos de toque de pelo menos 48 px.

### Fase 4 — Fluxos de produtos e lotes

Implementar listagem/pesquisa e cadastro/edição de produtos; cadastro de lote; listagem com filtros, ordenação e paginação; detalhe e histórico; saída/descarte com confirmação. Integrar formulários à API e apresentar erros de campo e falhas de rede.

### Fase 5 — Visão geral e alertas

Exibir contagens de vencidos, vencendo em até 7 dias, vencendo em até 30 dias e sem estoque, além de lista priorizada de lotes. Garantir definições consistentes com a listagem e tratar carregamento, ausência de dados e falhas.

### Fase 6 — Qualidade e preparação para entrega

Revisar acessibilidade, responsividade, erros, configuração por ambiente e instruções de execução. Definir banco de produção, backup e observabilidade antes da implantação.

## 4. Decisões do MVP (item 1 concluído)

As decisões abaixo estabelecem o contrato inicial para orientar a implementação. São explícitas para o MVP e podem ser revistas se uma necessidade de negócio diferente surgir.

### Regras de negócio

- **Data e fuso:** validade é uma data civil, sem horário. A referência é a data atual em `America/Sao_Paulo`, calculada no backend; o dia do vencimento conta como “vence hoje”, portanto urgente (0 dias restantes).
- **Faixas:** vencido < 0 dias; urgente entre 0 e 7 dias inclusive; atenção entre 8 e 30 dias inclusive; em dia acima de 30 dias. Sem estoque (saldo zero) é sinal independente da validade.
- **Unidade:** cada produto possui uma unidade selecionada no cadastro. O catálogo inicial é unidade, pacote, caixa, quilograma, grama, litro e mililitro. Unidade, pacote e caixa aceitam apenas quantidades inteiras; unidades de massa e volume aceitam até três casas decimais. Não haverá conversão entre unidades.
- **Estoque:** quantidade inicial e movimentações são positivas; saldo não pode ficar negativo. Não se permite saída ou descarte acima do saldo. Saídas e descartes são movimentos distintos no histórico.
- **Movimentação:** toda saída/descarte exige quantidade; observação é opcional. Operação e atualização do saldo são atômicas. Não se apaga movimentação; correções futuras devem ser feitas por movimento compensatório.
- **Arquivamento:** produtos e lotes com histórico não são apagados fisicamente. Podem ser arquivados/inativados e deixam de aparecer nas listas padrão; histórico permanece consultável.
- **Código de lote:** único por produto; pode ser reutilizado em produtos diferentes. Código de barras do produto é opcional e único quando informado.
- **Autenticação/múltiplas lojas:** fora do MVP. O MVP opera com uma única loja lógica e sem contas de usuário; não tratar o protótipo com nomes fictícios como requisito de autenticação.

### Contrato inicial da API

- Prefixo: `/api`; JSON em UTF-8; datas civis em formato ISO `YYYY-MM-DD`; instantes de movimentação em ISO-8601 com offset.
- Coleções aceitam `page` (base zero), `size` (padrão 20, máximo 100) e `sort`; lotes ordenam por `validade,asc` por padrão.
- `GET /api/lotes` aceita `produtoId`, `status`, `validadeDe`, `validadeAte`, `page`, `size` e `sort`. Status aceita `VENCIDO`, `URGENTE`, `ATENCAO`, `EM_DIA` e `SEM_ESTOQUE`; filtro sem estoque refere-se ao saldo e pode ser combinado a apenas um status de validade por vez.
- Erros usam envelope estável: `{ "timestamp": "...", "status": 400, "code": "VALIDATION_ERROR", "message": "...", "fieldErrors": [{ "field": "...", "message": "..." }] }`. Erros sem campo retornam `fieldErrors: []`.
- Usar `400` para validação, `404` para recurso inexistente, `409` para conflito de unicidade/saldo concorrente, `201` para criação, `200` para consulta/atualização e `204` somente quando não houver corpo de resposta.

### Execução local

- Frontend Angular em `http://localhost:4200`; backend Spring em `http://localhost:8080`.
- O frontend acessa a API pelo prefixo `/api`; em desenvolvimento, configurar proxy Angular para o backend. CORS deve permitir somente origens explicitamente configuradas.
- H2 permanece para desenvolvimento; banco de produção e política de autenticação ficam fora desta decisão do MVP.

## 5. Critérios de aceite

- É possível cadastrar produto e lote válidos.
- Lotes podem ser filtrados e aparecem ordenados pela validade.
- Status é igual no painel, lista e detalhe, respeitando a data de São Paulo.
- Não é possível movimentar acima do saldo; cada movimento atualiza o saldo uma vez e aparece no histórico.
- Indicadores do painel correspondem às regras da listagem.
- Formulários apresentam erros e preservam os dados digitados após falha.
- Interface funciona em celular e desktop e trata carregamento, vazio e erro.
- Execução local está documentada.

## 6. Estratégia de validação

Cobrir regras de domínio e contratos no backend, componentes/formulários/serviços no frontend e fluxos críticos ponta a ponta. Priorizar fronteiras de datas (hoje, 7, 8, 30 e 31 dias), saldo zero, saída parcial e tentativa acima do saldo.

## 7. Dependências e riscos

- Banco de produção, backup e observabilidade precisam ser definidos antes de implantação.
- Movimentações concorrentes exigem transação e controle de concorrência.
- Autenticação, isolamento por loja, notificações, leitura de código de barras e relatórios não fazem parte do MVP atual.
- Alterações futuras nas decisões de negócio podem exigir ajustes no contrato da API.

## 8. Ordem sugerida de execução

1. ~~Confirmar regras pendentes e contratos.~~ **Implementado:** decisões iniciais e contrato da API registrados na seção 4.
2. Implementar domínio, persistência e serviços.
3. Expor e documentar a API.
4. Criar estrutura visual e navegação do Angular.
5. Implementar produtos e lotes.
6. Implementar movimentações e histórico.
7. Implementar painel.
8. Revisar acessibilidade, cenários críticos e instruções de execução.

