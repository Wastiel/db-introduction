# 🗄️ Introdução a Banco de Dados com SQL

Este guia apresenta os fundamentos dos bancos de dados relacionais com foco em SQL. Você aprenderá os tipos de dados básicos, como criar tabelas, usar restrições (`PRIMARY KEY`, `NOT NULL`, etc.), e realizar todas as operações do CRUD.

---

## 🔠 Tipos de Dados Básicos em SQL

| Tipo       | Descrição                            | Exemplo           |
|------------|---------------------------------------|-------------------|
| `INTEGER`  | Número inteiro                        | `1`, `100`, `-5`  |
| `REAL`     | Número decimal (ponto flutuante)      | `3.14`, `-0.5`    |
| `VARCHAR`     | Texto (cadeia de caracteres)          | `'Maria'`         |
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

## 🏗️ Criação de Tabela (CREATE)

```sql
CREATE TABLE Alunos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome VARCHAR(45) NOT NULL,
    idade INTEGER,
    curso VARCHAR(45) NOT NULL,
    ativo BOOLEAN DEFAULT 1
);
```

- `id`: identificador único, gerado automaticamente  
- `nome`: obrigatório  
- `idade`: opcional  
- `curso`: obrigatório  
- `ativo`: por padrão, `1` (ativo)

---

## 🧾 Inserção de Dados (INSERT)

### Inserir um único registro:

```sql
INSERT INTO Alunos (nome, idade, curso)
VALUES ('João Silva', 22, 'Engenharia');
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

## 📌 Recomendações

- Teste os comandos em ferramentas como:
  - [DB Browser for SQLite](https://sqlitebrowser.org/)
  - [DBeaver](https://dbeaver.io/)
  - [SQL Fiddle](https://sqlfiddle.com/)
- Use `SELECT *` com cuidado em bancos grandes — prefira selecionar apenas as colunas necessárias.
- Combine `WHERE`, `ORDER BY`, `LIMIT`, `AND` e `OR` para criar consultas eficientes.

---

## 🔗 Recursos Complementares

- [Repositório de estudo (db-introduction)](https://github.com/Wastiel/db-introduction)
- [W3Schools – SQL Tutorial](https://www.w3schools.com/sql/)
- [SQLite Tutorial](https://www.sqlitetutorial.net/)
- [DIO – Curso de SQL Básico](https://www.dio.me/courses/introducao-ao-sql)

---

> ✍️ Sinta-se à vontade para adaptar este material, adicionar novas tabelas e praticar mais comandos como `JOIN`, `GROUP BY` e `HAVING` à medida que evolui.