---
name: Lote em Dia Design System
colors:
  surface: '#f8f9ff'
  surface-dim: '#cbdbf5'
  surface-bright: '#f8f9ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#eff4ff'
  surface-container: '#e5eeff'
  surface-container-high: '#dce9ff'
  surface-container-highest: '#d3e4fe'
  on-surface: '#0b1c30'
  on-surface-variant: '#3e4a3d'
  inverse-surface: '#213145'
  inverse-on-surface: '#eaf1ff'
  outline: '#6e7b6c'
  outline-variant: '#bdcaba'
  surface-tint: '#006e2d'
  primary: '#006b2c'
  on-primary: '#ffffff'
  primary-container: '#00873a'
  on-primary-container: '#f7fff2'
  inverse-primary: '#62df7d'
  secondary: '#565e74'
  on-secondary: '#ffffff'
  secondary-container: '#dae2fd'
  on-secondary-container: '#5c647a'
  tertiary: '#a33900'
  on-tertiary: '#ffffff'
  tertiary-container: '#cc4900'
  on-tertiary-container: '#fffbff'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#7ffc97'
  primary-fixed-dim: '#62df7d'
  on-primary-fixed: '#002109'
  on-primary-fixed-variant: '#005320'
  secondary-fixed: '#dae2fd'
  secondary-fixed-dim: '#bec6e0'
  on-secondary-fixed: '#131b2e'
  on-secondary-fixed-variant: '#3f465c'
  tertiary-fixed: '#ffdbce'
  tertiary-fixed-dim: '#ffb599'
  on-tertiary-fixed: '#370e00'
  on-tertiary-fixed-variant: '#7f2b00'
  background: '#f8f9ff'
  on-background: '#0b1c30'
  surface-variant: '#d3e4fe'
typography:
  display-lg:
    fontFamily: Plus Jakarta Sans
    fontSize: 32px
    fontWeight: '700'
    lineHeight: 40px
    letterSpacing: -0.02em
  headline-lg:
    fontFamily: Plus Jakarta Sans
    fontSize: 24px
    fontWeight: '700'
    lineHeight: 32px
    letterSpacing: -0.015em
  headline-md:
    fontFamily: Plus Jakarta Sans
    fontSize: 20px
    fontWeight: '600'
    lineHeight: 28px
    letterSpacing: -0.01em
  headline-sm:
    fontFamily: Plus Jakarta Sans
    fontSize: 18px
    fontWeight: '600'
    lineHeight: 24px
  body-lg:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  body-md:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  body-sm:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '400'
    lineHeight: 16px
  label-lg:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '600'
    lineHeight: 20px
  label-md:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '600'
    lineHeight: 16px
    letterSpacing: 0.01em
  label-sm:
    fontFamily: Inter
    fontSize: 11px
    fontWeight: '700'
    lineHeight: 14px
    letterSpacing: 0.02em
  numeric-metric:
    fontFamily: Plus Jakarta Sans
    fontSize: 28px
    fontWeight: '700'
    lineHeight: 32px
    letterSpacing: -0.02em
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  gutter: 1rem
  margin: 1rem
  space-xs: 0.25rem
  space-sm: 0.5rem
  space-md: 1rem
  space-lg: 1.5rem
  space-xl: 2rem
---

## Brand & Style

O design system estabelece uma experiência utilitária, ágil e acolhedora voltada à operação diária de varejo físico (mercearias, empórios e lojas de produtos naturais). A estética combina **Modern Utilitarian** com ergonomia física de balcão: foco implacável na rápida escaneabilidade visual, redução da sobrecarga cognitiva e garantia de decisões corretas em frações de segundo.

O tom visual equilibra frescor orgânico e disciplina operacional. Transmite a segurança de um estoque auditado sem a frieza de softwares legados de ERP. Elementos táteis possuem áreas de toque generosas para uso com apenas uma mão no corredor ou atrás do caixa, eliminando ambiguidades por meio de alto contraste e convenções de status padronizadas.

## Colors

A hierarquia cromática é calibrada para priorizar alertas operacionais e prevenir perdas financeiras por expiração de produtos.

### Cores Fundamentais
- **Primary (`#16A34A`):** Verde fresco e confiável que ancora a identidade, ações primárias de sucesso e estados regulares.
- **Secondary (`#0F172A`):** Ardósia profundo utilizado para máxima legibilidade de títulos, valores numéricos e contraste com a base.
- **Tertiary (`#EA580C`):** Laranja vivo reservado para urgência intermediária operacional.
- **Neutral (`#64748B`):** Cinza neutro balanceado para legendas, metadados secundários e contornos estruturais.

### Superfícies & Fundo
- **App Canvas:** `#F8FAFC`
- **Surface Elevation 01 (Cards, Sheets):** `#FFFFFF`
- **Surface Muted / Dividers:** `#E2E8F0` / `#F1F5F9`

### Matriz Semântica de Validade (Obrigatória)
Cada status combina cor de primeiro plano e container de fundo de alto contraste:
- **Vencido (Crítico):** Texto/Ícone `#DC2626` sobre container `#FEE2E2`
- **Até 7 dias (Urgência Alta):** Texto/Ícone `#EA580C` sobre container `#FFEDD5`
- **Até 30 dias (Atenção Preventiva):** Texto/Ícone `#D97706` sobre container `#FEF3C7`
- **Em dia (Regular):** Texto/Ícone `#16A34A` sobre container `#DCFCE7`
- **Sem estoque / Arquivado:** Texto/Ícone `#64748B` sobre container `#F1F5F9`

## Typography

A tipografia utiliza **Plus Jakarta Sans** nos cabeçalhos e números de impacto operacional para imprimir clareza humana e moderna, enquanto **Inter** sustenta corpos de texto, formulários e metadados densos com precisão sistemática.

### Regras de Aplicação
- Números de dias restantes, códigos de lote e quantidades utilizam pesos `600` ou `700` para leitura imediata em movimento.
- Em dispositivos móveis compactos, métricas numéricas não ultrapassam 32px para evitar quebras de layout em cards de listagem.
- Rótulos de status empregam `label-sm` com caixa alta ou semi-bold estrito para diferenciação imediata de texto descritivo comum.

## Layout & Spacing

O layout é desenhado a partir de uma filosofia mobile-first de coluna única com ritmo vertical estrito de 8px (submúltiplo de 4px). 

### Dimensões do Canvas
- **Gutter:** `1rem` (16px) entre cartões agrupados e divisões de lista.
- **Margin:** `1rem` (16px) nas bordas laterais em telas padrão móveis, expandindo para `1.5rem` (24px) em tablets.
- **Target Touch Mínimo:** Todos os elementos acionáveis possuem altura mínima de `48px` para operação sem falhas de toque.

### Adaptação de Tela
- **Mobile (< 640px):** Lista vertical estrita, ações primárias fixadas no rodapé acessível pelo polegar, Bottom Navigationbar permanente.
- **Tablet / Balcão (≥ 640px):** Layout dividido em painel mestre-detalhe (2 colunas: 40% lista de lotes, 60% detalhes da inspeção/cadastro).

## Elevation & Depth

A profundidade é expressa prioritariamente através de **camadas tonais combinadas com contornos sutis de baixo contraste**, evitando sombras escuras que poluem a tela sob luz solar ou iluminação fluorescente de loja.

### Níveis de Elevação
- **Level 0 (Base Canvas):** Fundo plano `#F8FAFC`, sem relevo.
- **Level 1 (Cards, Itens de Lista):** Superfície `#FFFFFF` com borda de 1px em `#E2E8F0` e sombra ambiente ultra suave (`0 1px 3px rgba(15, 23, 42, 0.04)`).
- **Level 2 (Modais Inferiores, Bottom Sheet, Alertas Flutuantes):** Fundo `#FFFFFF`, sombra difusa (`0 8px 24px -4px rgba(15, 23, 42, 0.10)`), sem bordas pesadas.
- **Level 3 (Bottom Navigation & Sticky CTAs):** Superfície `#FFFFFF` com borda superior sólida de 1px em `#E2E8F0` e desfoque sutil quando sobreposto.

## Shapes

O sistema adota o nível de arredondamento **2 (Rounded)**:
- **Base UI (Botões, Inputs, Badges):** Raio de `0.5rem` (8px).
- **Cards e Painéis:** Raio de `1rem` (16px), conferindo suavidade ergonômica sem perda de aproveitamento de tela.
- **Modais e Bottom Sheets:** Raio superior de `1.5rem` (24px).
- **Tags e Badges de Status:** Pílula completa (`9999px`) ou raio de `0.5rem` (8px) para encaixe perfeito em cantos de cards.

## Components

### 1. Badges de Validade (Status Chips)
- **Construção:** Ícone correspondente à esquerda (16px), rótulo em `label-sm` em peso 700.
- **Estilo:** Padding horizontal de `8px`, vertical de `4px`, cantos com `8px`.
- **Regra de cor:** Aplica a matriz de status (fundo claro + tipografia escura saturada na respectiva cor semântica). Nunca utilizar texto branco sobre fundo saturado em chips de listagem para preservar legibilidade de balcão.

### 2. Cards de Lote & Produto
- **Estrutura:** Cabeçalho com nome do produto e quantidade disponível; corpo com código do lote e data formal (DD/MM/AAAA); rodapé com badge de validade e contagem regressiva em destaque (ex.: "Vence em 4 dias").
- **Barra lateral de acento:** Borda esquerda de 4px na cor do status para leitura periférica instantânea durante a rolagem.

### 3. Botões (Buttons)
- **Primary:** Fundo `#16A34A`, texto branco, altura de `48px`, raio de `8px`.
- **Secondary:** Fundo `#FFFFFF`, contorno de 1.5px em `#E2E8F0`, texto `#0F172A`.
- **Destructive:** Fundo `#FEE2E2`, texto `#DC2626` para descarte de lote vencido.

### 4. Inputs & Campos de Formulário
- Altura mínima de `48px`, preenchimento `#FFFFFF`, contorno `#CBD5E1`.
- Foco ativo destacado com anel de 2px em `#16A34A`.
- Labels posicionadas acima do campo em `label-md` com texto `#334155`. Suporte a máscaras dedicadas para datas e códigos de barra (EAN-13).

### 5. Navegação Inferior (Bottom Navigation)
- Altura de `64px`, fixada na base com proteção para safe-area.
- 4 destinos obrigatórios:
  1. **Visão geral** (Ícone dashboard/home)
  2. **Lotes** (Ícone camadas/caixa com alerta)
  3. **Produtos** (Ícone tags/cesta)
  4. **Configurações** (Ícone engrenagem/ajustes)
- Item ativo: Ícone e texto preenchidos em `#16A34A` com indicador de ponto sutil. Itens inativos em `#64748B`.