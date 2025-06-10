
# 🗄️ Introdução a Banco de Dados com SQL

Este guia apresenta os fundamentos dos bancos de dados relacionais com foco em SQL. Vamos aprender os tipos de dados básicos, como criar tabelas, usar restrições (`PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, etc.), e realizar todas as operações do CRUD.

---

## 🔠 Tipos de Dados Básicos em SQL

| Tipo       | Descrição                            | Exemplo           |
|------------|---------------------------------------|-------------------|
| `INTEGER`  | Número inteiro                        | `1`, `100`, `-5`  |
| `REAL`     | Número decimal (ponto flutuante)      | `3.14`, `-0.5`    |
| `VARCHAR`  | Texto (cadeia de caracteres)          | `'Maria'`         |
| `DATE`     | Data (formato `YYYY-MM-DD`)           | `'2025-05-27'`    |
| `BOOLEAN`  | Verdadeiro ou falso (`1` ou `0`)      | `1` (true), `0` (false) |

---

## ⚙️ Restrições (Constraints) em Tabelas

| Palavra-chave    | Significado                                                                 |
|------------------|------------------------------------------------------------------------------|
| `PRIMARY KEY`    | Define uma coluna como identificador único da tabela                         |
| `AUTOINCREMENT`  | Faz a coluna numérica crescer automaticamente a cada novo registro           |
| `NOT NULL`       | Impede que a coluna receba valores nulos (vazios)                            |
| `UNIQUE`         | Garante que os valores em uma coluna sejam todos diferentes                  |
| `DEFAULT`        | Define um valor padrão se nenhum valor for fornecido                         |

---

## 🏗️ Criação de um Banco de dados (CREATE)

```sql
CREATE DATABASE escola;
```

---

## 🏗️ Criação de Tabela (CREATE)

```sql
CREATE TABLE Alunos (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(45) NOT NULL,
    idade INTEGER,
    curso VARCHAR(45) NOT NULL,
    ativo BOOLEAN DEFAULT 1,
    data_aniversario DATE
);
```

- `id`: identificador único, gerado automaticamente  
- `nome`: obrigatório  
- `idade`: opcional  
- `curso`: obrigatório  
- `ativo`: por padrão, `1` (ativo)
- `data_aniversario`: Data de inserção nao obrigatoria.

---

## 🧾 Inserção de Dados (INSERT)

### Inserir um único registro:

```sql
INSERT INTO Alunos (nome, idade, curso)
VALUES ('João Silva', 22, 'Engenharia');

INSERT INTO Alunos (nome, idade, curso, ativo, data_cadastro)
VALUES ('Maria Silva', 22, 'Engenharia', 1, '2025-05-29');
```

### Inserir múltiplos registros:

```sql
INSERT INTO Alunos (nome, idade, curso)
VALUES 
  ('Maria Souza', 20, 'Direito'),
  ('Carlos Lima', 25, 'Computação'),
  ('Ana Costa', 19, 'Design');
```

---

## 🔍 Consulta de Dados (SELECT)

### Buscar todos os registros:

```sql
SELECT * FROM Alunos;
```

### Buscar apenas nome e idade:

```sql
SELECT nome, idade FROM Alunos;
```

### Filtrar por curso:

```sql
SELECT * FROM Alunos WHERE curso = 'Computação';
```

### Filtrar por idade maior que 21:

```sql
SELECT * FROM Alunos WHERE idade > 21;
```

### Ordenar por nome (crescente):

```sql
SELECT * FROM Alunos ORDER BY nome ASC;
```

---

## 📝 Atualização de Dados (UPDATE)

### Atualizar a idade de um aluno:

```sql
UPDATE Alunos
SET idade = 23
WHERE nome = 'João Silva';
```

### Marcar um aluno como inativo:

```sql
UPDATE Alunos
SET ativo = 0
WHERE id = 3;
```

---

## 🗑️ Remoção de Dados (DELETE)

### Apagar um único registro:

```sql
DELETE FROM Alunos
WHERE id = 2;
```

### Apagar todos os registros (⚠️ perigoso!):

```sql
DELETE FROM Alunos;
```

---

## ✅ Consulta com Condições Compostas

```sql
SELECT * FROM Alunos
WHERE curso = 'Computação' AND idade >= 22;
```

---

## ✅ Consulta com Condição IN

```sql
SELECT * FROM Alunos
WHERE id in(1, 14, 2);
```

---

## 🏥 Relacionamento 1:1 — Paciente e Prontuário

### 📘 Conceito:
Cada **paciente** possui **apenas um prontuário**, e cada **prontuário** está associado a **apenas um paciente**. Isso representa uma relação **um para um (1:1)**.

### 🏗️ Criação das Tabelas

```sql
CREATE TABLE Paciente (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    data_nascimento DATE
);
```

```sql
CREATE TABLE Prontuario (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    id_paciente INTEGER UNIQUE,
    historico TEXT,
    FOREIGN KEY (id_paciente) REFERENCES Paciente(id)
);
```

> 🔒 A restrição `UNIQUE` em `id_paciente` garante que um prontuário esteja vinculado **exclusivamente a um único paciente**, implementando assim o relacionamento 1:1.

### 🧾 Exemplo de Inserção

```sql
INSERT INTO Paciente (nome, data_nascimento) VALUES 
('Ana Souza', '1990-04-15'),
('Carlos Lima', '1985-11-22');

INSERT INTO Prontuario (id_paciente, historico) VALUES 
(1, 'Paciente com histórico de alergias a medicamentos.'),
(2, 'Paciente hipertenso, faz uso de medicação contínua.');
```

### 🔍 Consultando pacientes com seus prontuários

```sql
SELECT p.nome AS paciente, p.data_nascimento, pr.historico
FROM Paciente p
JOIN Prontuario pr ON p.id = pr.id_paciente;
```
---

## ⚽ Relacionamento 1:N — Time e Jogadores

### 📘 Conceito:
Um **time** pode ter **vários jogadores**, mas **cada jogador** pertence a **apenas um time**. Isso representa uma relação **um para muitos (1:N)**.

### 🏗️ Criação das Tabelas

```sql
CREATE TABLE Time (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL,
    cidade VARCHAR(50)
);
```

```sql
CREATE TABLE Jogador (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL,
    posicao VARCHAR(30),
    idade INTEGER,
    id_time INTEGER,
    FOREIGN KEY (id_time) REFERENCES Time(id)
);
```

### 🧾 Exemplo de Inserção

```sql
INSERT INTO Time (nome, cidade) VALUES 
('Flamengo', 'Rio de Janeiro'),
('Corinthians', 'São Paulo');

INSERT INTO Jogador (nome, posicao, idade, id_time) VALUES 
('Pedro', 'Atacante', 26, 1),
('Gabigol', 'Atacante', 27, 1),
('Cássio', 'Goleiro', 36, 2);
```

### 🔍 Consultando jogadores com seus times

```sql
SELECT j.nome AS jogador, j.posicao, t.nome AS time
FROM Jogador j
JOIN Time t ON j.id_time = t.id;
```

---

## 📚 Relacionamento N:N — Livros e Autores

### 📘 Conceito:
Um **livro pode ter vários autores**, e um **autor pode escrever vários livros**.  
Essa relação é **muitos para muitos (N:N)**, e precisamos de uma **tabela intermediária**.

### 🏗️ Criação das Tabelas

```sql
CREATE TABLE Autor (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL
);
```

```sql
CREATE TABLE Livro (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(100) NOT NULL,
    ano_publicacao INTEGER
);
```

```sql
CREATE TABLE LivroAutor (
    id_livro INTEGER,
    id_autor INTEGER,
    PRIMARY KEY (id_livro, id_autor),
    FOREIGN KEY (id_livro) REFERENCES Livro(id),
    FOREIGN KEY (id_autor) REFERENCES Autor(id)
);
```

### 🧾 Exemplo de Inserção

```sql
INSERT INTO Autor (nome) VALUES 
('Machado de Assis'),
('Clarice Lispector');

INSERT INTO Livro (titulo, ano_publicacao) VALUES 
('Dom Casmurro', 1899),
('A Hora da Estrela', 1977);

INSERT INTO LivroAutor (id_livro, id_autor) VALUES 
(1, 1),
(2, 2);
```

### 🔍 Consultando livros com autores

```sql
SELECT l.titulo, a.nome AS autor
FROM Livro l
JOIN LivroAutor la ON l.id = la.id_livro
JOIN Autor a ON a.id = la.id_autor;
```

---

## 📌 Recomendações

- Teste os comandos em ferramentas como:
  - [DB Browser for SQLite](https://sqlitebrowser.org/)
  - [DBeaver](https://dbeaver.io/)
  - [SQL Fiddle](https://sqlfiddle.com/)
- Use `SELECT *` com cuidado em bancos grandes — prefira selecionar apenas as colunas necessárias.
- Combine `WHERE`, `ORDER BY`, `LIMIT`, `AND` e `OR` para criar consultas eficientes.
- Relacione suas tabelas corretamente com **chaves estrangeiras**
- Para relações muitos-para-muitos, **crie sempre uma tabela associativa**
- Em JOINs, use apelidos (`AS`) para deixar as consultas mais legíveis
- Evite repetir informações — normalize os dados para manter o banco organizado


---

## 🔗 Recursos Complementares

- [Repositório de estudo (db-introduction)](https://github.com/Wastiel/db-introduction)
- [W3Schools – SQL Tutorial](https://www.w3schools.com/sql/)
- [SQLite Tutorial](https://www.sqlitetutorial.net/)
- [DIO – Curso de SQL Básico](https://www.dio.me/courses/introducao-ao-sql)

---

## 🏷️ Uso de Alias (Apelidos)

Os **alias** (ou apelidos) em SQL são usados para renomear temporariamente tabelas ou colunas durante uma consulta. Eles tornam os resultados mais legíveis ou ajudam a evitar ambiguidades em consultas mais complexas, especialmente ao usar `JOIN`.

### ✅ Por que usar alias?

- Facilita a leitura dos resultados
- Reduz repetição de nomes longos
- Esclarece o papel de colunas em `JOIN`
- Melhora a clareza ao usar funções de agregação

### 🧪 Exemplo de alias em colunas:

```sql
SELECT nome AS NomeAluno, idade AS IdadeAluno
FROM Alunos;
```

- `AS NomeAluno`: mostra a coluna `nome` com o título `NomeAluno` no resultado

### 🔄 Exemplo de alias em tabelas:

```sql
SELECT a.nome, a.curso
FROM Alunos AS a
WHERE a.ativo = 1;
```

- `Alunos AS a`: cria o apelido `a` para a tabela `Alunos`

### 🧩 Em joins:

```sql
SELECT j.nome AS Jogador, t.nome AS Time
FROM Jogadores AS j
JOIN Times AS t ON j.time_id = t.id;
```

- Aqui, usamos alias para deixar claro que `j.nome` é o nome do jogador e `t.nome` é o nome do time.

---


---

## 🔗 JOINs em SQL: INNER, LEFT e RIGHT

Os **JOINs** permitem combinar dados de duas ou mais tabelas com base em uma coluna relacionada entre elas. Isso é essencial para bancos de dados relacionais, onde informações estão distribuídas em várias tabelas.

### 🧩 INNER JOIN (Junção Interna)

Retorna apenas os registros que têm correspondência nas duas tabelas.

```sql
SELECT j.nome AS Jogador, t.nome AS Time
FROM Jogadores AS j
INNER JOIN Times AS t ON j.time_id = t.id;
```

📌 Mostra apenas jogadores que têm time associado.

---

### 🧩 LEFT JOIN (Junção à Esquerda)

Retorna todos os registros da tabela da esquerda e os correspondentes da tabela da direita. Se não houver correspondência, os valores da tabela da direita serão `NULL`.

```sql
SELECT j.nome AS Jogador, t.nome AS Time
FROM Jogadores AS j
LEFT JOIN Times AS t ON j.time_id = t.id;
```

📌 Mostra todos os jogadores, mesmo os sem time (nesses casos, o campo `Time` será `NULL`).

---

### 🧩 RIGHT JOIN (Junção à Direita)

Retorna todos os registros da tabela da direita e os correspondentes da tabela da esquerda. Se não houver correspondência, os valores da tabela da esquerda serão `NULL`.

```sql
SELECT j.nome AS Jogador, t.nome AS Time
FROM Jogadores AS j
RIGHT JOIN Times AS t ON j.time_id = t.id;
```

📌 Mostra todos os times, mesmo aqueles que não têm jogadores.

---

### 🧠 Quando usar cada um?

| Tipo de JOIN | Quando usar? |
|--------------|--------------|
| `INNER JOIN` | Quando você só quer dados com correspondência em ambas as tabelas. |
| `LEFT JOIN`  | Quando você quer **todos os registros da tabela principal** e os relacionados se existirem. |
| `RIGHT JOIN` | Quando você quer **todos os registros da tabela secundária** e os relacionados se existirem. |

---
