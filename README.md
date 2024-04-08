# Projeto_Integrador_AutoPecas

Projeto final de curso - ADM Banco de Dados
Professor Hudson Neves
Alunos: Ana Cristina Oliveira da Silva
        Audeane de Lucena Santana
        Luiz Felipe Pereira da Silva
        
SENAC - Tallal Abu Allan

CREATE TABLE Cliente (
    IDCliente INT PRIMARY KEY,
    Nome VARCHAR(100) NOT NULL,
    Data_Nasc DATE NOT NULL,
    Contato_idcontato INT,
    FOREIGN KEY (Contato_idcontato) REFERENCES Contato(IDcontato)
);

CREATE TABLE Pessoa_Fisica (
    IDPessoa INT PRIMARY KEY,
    Nome VARCHAR(100) NOT NULL,
    RG VARCHAR(20) NOT NULL,
    CPF CHAR(14) NOT NULL,
    Data_Nasc DATE NOT NULL,
    Contato_idcontato INT,
    FOREIGN KEY (Contato_idcontato) REFERENCES Contato(IDcontato)
);

CREATE TABLE Pessoa_Juridica (
    IDPessoa INT PRIMARY KEY,
    Nome_fantasia VARCHAR(50) NOT NULL,
    Razao_social VARCHAR(50) NOT NULL,
    CNPJ CHAR(18) NOT NULL,
    IE VARCHAR(20),
    Contato_idcontato INT,
    FOREIGN KEY (Contato_idcontato) REFERENCES Contato(IDcontato)
);

CREATE TABLE Contato (
    IDcontato INT PRIMARY KEY,
    Telefone CHAR(15),
    Endereco VARCHAR(100) NOT NULL,
    CEP CHAR(9),
    Email VARCHAR(60) NOT NULL
);

CREATE TABLE Veiculo (
    IDVeiculo INT PRIMARY KEY,
    Marca_veic CHAR(50) NOT NULL,
    Modelo_veic CHAR(22) NOT NULL,
    Placa_veic VARCHAR(15) NOT NULL
);

CREATE TABLE Fornecedor (
    IDFornecedor INT PRIMARY KEY,
    Nome_fantasia VARCHAR(50) NOT NULL,
    Razao_social VARCHAR(50) NOT NULL,
    CNPJ CHAR(18) NOT NULL,
    IE VARCHAR(20),
    Contato_idcontato INT,
    FOREIGN KEY (Contato_idcontato) REFERENCES Contato(IDcontato)
);

CREATE TABLE Produto (
    IDProduto INT PRIMARY KEY,
    Nome VARCHAR(50) NOT NULL,
    Preco DECIMAL(10,2) NOT NULL,
    Descricao VARCHAR(255) NOT NULL,
    Qtde_estoque INT NOT NULL,
    Qtde_min INT NOT NULL,
    Modelo_idmod INT,
    FOREIGN KEY (Modelo_idmod) REFERENCES Modelo(IDmod)
);

CREATE TABLE Marca (
    IDmarca INT PRIMARY KEY,
    Descricao VARCHAR(100) NOT NULL
);

CREATE TABLE Modelo (
    IDmod INT PRIMARY KEY,
    Descricao VARCHAR(100) NOT NULL,
    Marca_idmarca INT,
    FOREIGN KEY (Marca_idmarca) REFERENCES Marca(IDmarca)
);

CREATE TABLE Venda (
    IDvenda INT PRIMARY KEY,
    DTVenda DATE,
    Cliente_idcliente INT,
    FOREIGN KEY (Cliente_idcliente) REFERENCES Cliente(IDCliente)
);

CREATE TABLE Itens_venda (
    IDvenda INT,
    IDproduto INT,
    Preco DECIMAL(10,2) NOT NULL,
    Qtde INT NOT NULL,
    PRIMARY KEY (IDvenda, IDproduto),
    FOREIGN KEY (IDvenda) REFERENCES Venda(IDvenda),
    FOREIGN KEY (IDproduto) REFERENCES Produto(IDProduto)
);


ALTER TABLE Veiculo
ADD Cliente_idcliente INT NOT NULL;

SP_HELP Veiculo;
ALTER TABLE Veiculo
ADD CONSTRAINT fk_cliente
    FOREIGN KEY (Cliente_idcliente)
    REFERENCES Cliente(IDCliente);

