# Gest-o-de-Pedidos
Sistema de gestão de pedidos para vendedores

Estrutura Inicial:
Sistema de Pedidos

1. Login
   - Administrador
   - Vendedor

2. Cadastro de pedido
   - Cliente
   - Telefone
   - Endereço
   - Produto
   - Quantidade
   - Valor
   - Pagamento
   - Vendedor
   - Status

3. Lista de pedidos
   - Todos os pedidos
   - Filtro por status
   - Filtro por vendedor
   - Botão para alterar status

4. Dashboard
   - Vendas do dia
   - Pedidos em aberto
   - Ranking de vendedores
   - Produtos mais vendidos

1. Objetivo do sistema

Centralizar os pedidos recebidos pelos vendedores no WhatsApp em uma lista única para você acompanhar, organizar entregas e controlar vendas.

2. Tipos de usuário
Administrador
Pode:

Ver todos os pedidos
Filtrar por vendedor
Alterar status
Ver dashboard
Cadastrar vendedores
Exportar relatórios
Vendedor

Quem recebe pedidos.

Pode:

Cadastrar pedido
Ver os próprios pedidos
Alterar observações
Acompanhar status
3. Telas principais
Tela 1 — Login

Campos:

E-mail
Senha
Tipo de usuário
Tela 2 — Cadastro de pedido

Campos:

Data do pedido
Nome do cliente
Telefone / WhatsApp
Endereço de entrega
Bairro
Produto
Quantidade
Valor unitário
Valor total
Forma de pagamento
Vendedor
Observação
Status do pedido

Formas de pagamento:

Pix
Dinheiro
Cartão
Boleto
Pendente

Status:

Novo pedido
Em separação
Saiu para entrega
Entregue
Cancelado
Pagamento pendente
Pago
Tela 3 — Lista de pedidos

Tabela com:

ID
Data
Cliente
Telefone
Produto
Quantidade
Valor total
Pagamento
Vendedor
Status
Endereço
Observação

Filtros:

Data
Vendedor
Status
Forma de pagamento
Cliente
Produto
Tela 4 — Gestão de entrega

Campos principais:

Pedido
Cliente
Endereço
Status
Entregador
Observação da entrega

Status de entrega:

Aguardando separação
Separado
Saiu para entrega
Entregue
Problema na entrega
Cancelado
Tela 5 — Dashboard

Indicadores:

Total vendido hoje
Total vendido no mês
Quantidade de pedidos hoje
Pedidos pendentes
Pedidos entregues
Pedidos cancelados
Ticket médio

Gráficos:

Vendas por vendedor
Produtos mais vendidos
Pedidos por status
Vendas por forma de pagamento
Vendas por dia

4. Estrutura do banco de dados
Tabela: usuarios
CREATE TABLE usuarios (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    senha VARCHAR(255) NOT NULL,
    tipo_usuario VARCHAR(20) NOT NULL,
    ativo BOOLEAN DEFAULT TRUE,
    data_cadastro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
Tabela: pedidos
CREATE TABLE pedidos (
    id SERIAL PRIMARY KEY,
    data_pedido DATE NOT NULL,
    nome_cliente VARCHAR(120) NOT NULL,
    telefone VARCHAR(30),
    endereco TEXT NOT NULL,
    bairro VARCHAR(80),
    produto VARCHAR(120) NOT NULL,
    quantidade INTEGER NOT NULL,
    valor_unitario NUMERIC(10,2) NOT NULL,
    valor_total NUMERIC(10,2) NOT NULL,
    forma_pagamento VARCHAR(50),
    vendedor VARCHAR(100),
    status_pedido VARCHAR(50) DEFAULT 'Novo pedido',
    observacao TEXT,
    data_cadastro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
Tabela: entregas
CREATE TABLE entregas (
    id SERIAL PRIMARY KEY,
    pedido_id INTEGER REFERENCES pedidos(id),
    entregador VARCHAR(100),
    status_entrega VARCHAR(50),
    observacao_entrega TEXT,
    data_saida TIMESTAMP,
    data_entrega TIMESTAMP
);

5. Fluxo de uso
1. Cliente manda pedido pelo WhatsApp para o vendedor

2. Vendedor abre o sistema no celular

3. Vendedor cadastra o pedido

4. Pedido aparece na lista geral

5. Administrador acompanha e organiza a entrega

6. Status é atualizado até "Entregue"

7. Dashboard mostra vendas e desempenho
6. Primeira versão recomendada

Para começar rápido, eu faria:

Streamlit + PostgreSQL/Supabase

Com 4 abas:

Cadastro de Pedido
Lista de Pedidos
Dashboard
Gestão
