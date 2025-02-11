# Projeto: Banco de Dados para E-commerce

## Descrição
Este projeto consiste na modelagem e implementação de um banco de dados MySQL para um sistema de e-commerce. Ele inclui as principais entidades necessárias para gerenciar clientes, vendedores, fornecedores, produtos, pedidos, pagamentos e entregas.

![Image](https://github.com/user-attachments/assets/625c782e-b24b-44cd-9da1-7e0a39e2cc1d)


## Estrutura do Banco de Dados

### 1. Criação do Banco de Dados
```sql
CREATE DATABASE IF NOT EXISTS ecommerce;
USE ecommerce;
```

### 2. Tabelas

#### Clientes
```sql
CREATE TABLE clientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    tipo ENUM('PF', 'PJ') NOT NULL,
    cpf_cnpj VARCHAR(14) UNIQUE NOT NULL
);
```

#### Vendedores
```sql
CREATE TABLE vendedores (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);
```

#### Fornecedores
```sql
CREATE TABLE fornecedores (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);
```

#### Produtos
```sql
CREATE TABLE produtos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    fornecedor_id INT,
    estoque INT NOT NULL,
    preco DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (fornecedor_id) REFERENCES fornecedores(id)
);
```

#### Pedidos
```sql
CREATE TABLE pedidos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    data_pedido DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (cliente_id) REFERENCES clientes(id)
);
```

#### Itens do Pedido
```sql
CREATE TABLE itens_pedido (
    id INT AUTO_INCREMENT PRIMARY KEY,
    pedido_id INT,
    produto_id INT,
    quantidade INT NOT NULL,
    preco_unitario DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (pedido_id) REFERENCES pedidos(id),
    FOREIGN KEY (produto_id) REFERENCES produtos(id)
);
```

#### Pagamentos
```sql
CREATE TABLE pagamentos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    pedido_id INT,
    tipo_pagamento ENUM('Cartão', 'Boleto', 'Pix') NOT NULL,
    valor DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (pedido_id) REFERENCES pedidos(id)
);
```

#### Entregas
```sql
CREATE TABLE entregas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    pedido_id INT,
    status ENUM('Aguardando Envio', 'Em Transporte', 'Entregue') NOT NULL,
    codigo_rastreio VARCHAR(50) UNIQUE NOT NULL,
    FOREIGN KEY (pedido_id) REFERENCES pedidos(id)
);
```

## Inserção de Dados

```sql
INSERT INTO clientes (nome, tipo, cpf_cnpj) VALUES ('Bruno Souza', 'PF', '12345678901');
INSERT INTO clientes (nome, tipo, cpf_cnpj) VALUES ('Empresa XYZ', 'PJ', '98765432000199');
INSERT INTO fornecedores (nome) VALUES ('Fornecedor A');
INSERT INTO produtos (nome, fornecedor_id, estoque, preco) VALUES ('Notebook', 1, 10, 3500.00);
INSERT INTO pedidos (cliente_id) VALUES (1);
INSERT INTO itens_pedido (pedido_id, produto_id, quantidade, preco_unitario) VALUES (1, 1, 2, 3500.00);
INSERT INTO pagamentos (pedido_id, tipo_pagamento, valor) VALUES (1, 'Cartão', 7000.00);
INSERT INTO entregas (pedido_id, status, codigo_rastreio) VALUES (1, 'Em Transporte', 'ABC123XYZ');
```

## Queries de Teste

### Quantos pedidos foram feitos por cada cliente?
```sql
SELECT cliente_id, COUNT(*) AS total_pedidos FROM pedidos GROUP BY cliente_id;
```

### Algum vendedor também é fornecedor?
```sql
SELECT v.nome FROM vendedores v JOIN fornecedores f ON v.nome = f.nome;
```

### Relação de produtos, fornecedores e estoques
```sql
SELECT p.nome AS produto, f.nome AS fornecedor, p.estoque FROM produtos p JOIN fornecedores f ON p.fornecedor_id = f.id;
```

### Relação de nomes dos fornecedores e produtos oferecidos
```sql
SELECT f.nome AS fornecedor, p.nome AS produto FROM fornecedores f JOIN produtos p ON f.id = p.fornecedor_id;
```

## Como Usar
1. Execute os comandos SQL na sua instância do MySQL.
2. Insira os dados de teste conforme indicado.
3. Utilize as queries para validar a estrutura do banco de dados.

---

## Contato

Para dúvidas ou sugestões, entre em contato:

## 👨‍💻 Autor

Bruno Molina, Uma Pessoa com Deficiência Auditiva - PcD, curso de análise de dados,
estudante do curso superior de Tecnologia em Análise e Desenvolvimento de Sistemas. Unicesumar. 2024 - 2026
- [GitHub](https://github.com/brumab) | [LinkedIn](https://www.linkedin.com/in/brumab1122/) | [cv](https://brumab.github.io/cur/)


