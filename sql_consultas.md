# 🧠 Guia Prático de Consultas em SQL

Este guia é focado no aprendizado de **consultas SQL**, ou seja, como extrair informações de um banco de dados.  
Você vai encontrar exemplos de como buscar, filtrar, ordenar e combinar dados de diferentes tabelas, além de explicações simples sobre `JOINs` e o uso de `alias`.

Tudo com base em tabelas realistas como **Alunos**, **Paciente/Prontuário**, **Jogadores/Times** e **Livros/Autores**.

---

## 📋 Tabelas utilizadas nos exemplos

### 🧑‍🎓 Tabela: Alunos

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

### 🏥 Tabela: Paciente e Prontuario (1:1)

```sql
CREATE TABLE Paciente (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    data_nascimento DATE
);

CREATE TABLE Prontuario (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    id_paciente INTEGER UNIQUE,
    historico TEXT,
    FOREIGN KEY (id_paciente) REFERENCES Paciente(id)
);
```

### ⚽ Tabela: Times e Jogadores (1:N)

```sql
CREATE TABLE Time (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL,
    cidade VARCHAR(50)
);

CREATE TABLE Jogador (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL,
    posicao VARCHAR(30),
    idade INTEGER,
    id_time INTEGER,
    FOREIGN KEY (id_time) REFERENCES Time(id)
);
```

### 📚 Tabela: Livros e Autores (N:N)

```sql
CREATE TABLE Autor (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL
);

CREATE TABLE Livro (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(100) NOT NULL,
    ano_publicacao INTEGER
);

CREATE TABLE LivroAutor (
    id_livro INTEGER,
    id_autor INTEGER,
    PRIMARY KEY (id_livro, id_autor),
    FOREIGN KEY (id_livro) REFERENCES Livro(id),
    FOREIGN KEY (id_autor) REFERENCES Autor(id)
);
```

---

# 🗄️ Introdução a Banco de Dados com SQL

Este guia apresenta os fundamentos dos bancos de dados relacionais com foco em SQL. Vamos aprender os tipos de dados básicos, como criar tabelas, usar restrições (`PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, etc.), e realizar todas as operações do CRUD.

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

### Consulta com Condições Compostas:
```sql
SELECT * FROM Alunos
WHERE curso = 'Computação' AND idade >= 22;
```

### Consulta com Condição IN:
```sql
SELECT * FROM Alunos
WHERE id IN (1, 14, 2);
```

## 🔗 JOINs em SQL: INNER, LEFT e RIGHT

### 🧩 INNER JOIN (Junção Interna)
Retorna apenas os registros que têm correspondência nas duas tabelas.

```sql
SELECT j.nome AS Jogador, t.nome AS Time
FROM Jogadores AS j
INNER JOIN Times AS t ON j.time_id = t.id;
```

---

## 📘 Explicando INNER JOIN e Alias de Forma Simples

### 🔍 O que é `INNER JOIN`?

Imagine que você tem **duas tabelas**:

- Uma tabela com **alunos**
- Outra tabela com os **cursos** que esses alunos fazem

Mas... o nome do curso **não está diretamente** na tabela de alunos, e sim só o **ID do curso**. Para descobrir o nome do curso de cada aluno, precisamos **juntar** as duas tabelas.  
É aí que entra o `JOIN`.

#### 💡 `INNER JOIN` significa:
> “Me mostre apenas os dados que existem nas duas tabelas, que se conectam por algum campo em comum”.

#### 👇 Exemplo simples:

```sql
SELECT a.nome, c.nome
FROM Alunos AS a
INNER JOIN Cursos AS c ON a.id_curso = c.id;
```

#### O que está acontecendo aqui?
- `Alunos AS a`: estamos dando o apelido **`a`** para a tabela `Alunos`
- `Cursos AS c`: damos o apelido **`c`** para a tabela `Cursos`
- `a.nome`: quer dizer "o nome que está na tabela dos alunos"
- `c.nome`: quer dizer "o nome que está na tabela dos cursos"
- `ON a.id_curso = c.id`: estamos dizendo **como essas tabelas se conectam**

### 🏷️ O que são `alias` (apelidos)?

Alias são **apelidos temporários** para facilitar a leitura das consultas.

#### Sem alias (um pouco mais confuso):
```sql
SELECT Alunos.nome, Cursos.nome
FROM Alunos
JOIN Cursos ON Alunos.id_curso = Cursos.id;
```

#### Com alias (mais claro e mais curto):
```sql
SELECT a.nome AS NomeAluno, c.nome AS NomeCurso
FROM Alunos AS a
JOIN Cursos AS c ON a.id_curso = c.id;
```

> 📌 Você pode escolher qualquer letra ou nome curto para o alias, como `a`, `alu`, `c`, `cur`, etc.

### 🧠 Dica Final

Pense no `JOIN` como **ligar peças de LEGO**. Se duas peças têm um encaixe compatível, elas se juntam. O `INNER JOIN` **só mostra as peças que encaixam de verdade** nas duas tabelas.
