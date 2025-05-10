
# 📘 Introdução à Modelagem de Dados

**Modelagem de Dados** é a técnica usada para representar de forma lógica e estruturada os dados de um sistema, definindo entidades, atributos e relacionamentos.

---

## 🔶 Conceitos Básicos

| Termo        | Definição                                                                 |
|--------------|--------------------------------------------------------------------------|
| **Dado**     | Elemento bruto, sem contexto (ex: “João”, “23”).                         |
| **Informação** | Conjunto organizado de dados que tem significado (ex: Boletim escolar). |
| **Conhecimento** | Aplicação de informações organizadas para tomada de decisões.           |

---

## 🛠️ Etapas da Modelagem

1. **Modelo Conceitual (DER)**  
   Visão geral do sistema, sem detalhes técnicos.  
   👉 Ferramenta: Diagrama Entidade-Relacionamento.

2. **Modelo Lógico**  
   Define tabelas, chaves primárias/estrangeiras, restrições, normalização.

3. **Modelo Físico**  
   Gera o script SQL, adaptado ao SGBD (ex: MySQL, PostgreSQL).

---

## 🧩 Elementos do Modelo ER

- **Entidade**: Representa um objeto real.  
  Ex: `Aluno`, `Livro`, `Pessoa`.

- **Atributo**: Característica da entidade.  
  Ex: `nome`, `CPF`, `título`.

- **Relacionamento**: Associação entre entidades.  
  Ex: `Aluno` ⟶ `Entrega` ⟵ `Trabalho`.

---

## 🔄 Cardinalidade

| Tipo           | Exemplo                           | Interpretação                                  |
|----------------|-----------------------------------|------------------------------------------------|
| **1:1**        | Pessoa — CNH                      | Uma pessoa possui no máx. uma CNH               |
| **1:N**        | Estado — País                     | Um país tem vários estados                     |
| **N:M**        | Aluno — Trabalho                  | Alunos entregam vários trabalhos e vice-versa  |

---

## 📐 Exemplos Clássicos

- **1:N – Jogador × Time**  
  Um time possui vários jogadores, mas cada jogador pertence a um único time.

- **1:N – Estado × País**  
  Um país tem vários estados, e cada estado pertence a um único país.

- **N:M – Livro × Autor**  
  Um livro pode ter vários autores, e um autor pode escrever vários livros.

- **N:M – Aluno × Trabalho**  
  Um aluno entrega vários trabalhos, e um trabalho pode ser feito por vários alunos.

- **1:1 – Pessoa × CNH**  
  Uma pessoa tem, no máximo, uma CNH. Uma CNH pertence a uma única pessoa.

---

## 🔧 Normalização de Dados

**Objetivo:** Eliminar redundâncias e dependências desnecessárias.

### 🔹 Primeira Forma Normal (1FN)
- **Regra:** Eliminar atributos multivalorados ou compostos.
- ✅ Atributos devem ser atômicos (ex: telefone separado, endereço dividido).

**Exemplo incorreto:**  
| Cliente | Telefone           |
|---------|--------------------|
| Ana     | 9999-9999, 8888-8888 |

**Correção:**  
Separar em outra tabela `Telefone(ClienteID, Telefone)`

---

### 🔹 Segunda Forma Normal (2FN)
- **Regra:** Eliminar dependência parcial da chave primária.
- ✅ Todos os atributos devem depender da **chave completa**.

**Exemplo antes da 2FN:**  
| ID_Pedido | ID_Produto | Nome_Produto | Nome_Fabricante |
|-----------|------------|--------------|-----------------|

**Correção:**  
Separar em `Produto(ID_Produto, Nome_Produto, ID_Fabricante)` e `Fabricante(ID_Fabricante, Nome_Fabricante)`

---

### 🔹 Terceira Forma Normal (3FN)
- **Regra:** Eliminar dependência **transitiva**.
- ✅ Nenhum atributo não-chave depende de outro atributo não-chave.

**Exemplo antes da 3FN:**  
| Nº Pedido | Cod_Produto | Preço       |
|-----------|-------------|-------------|

**Correção:**  
Separar em `Produto(Cod_Produto, Preço)` e manter `Pedido(Cod_Produto)`.

---

## 🧠 Regras de Chaves

- **Chave Primária (PK)**: Identifica unicamente uma linha.
- **Chave Estrangeira (FK)**: Referência uma PK de outra tabela.
- **Chave Candidata**: Possui potencial para ser PK.
- **Chave Alternativa**: Candidata que não foi escolhida como PK.

---

## 🛡️ Vantagens do SGBD

- Eliminação de redundâncias  
- Integridade e segurança dos dados  
- Compartilhamento e controle de acesso  
- Backup, recuperação e consistência

---

## 💻 Ferramentas recomendadas

- **Excalidraw**:  
  [https://excalidraw.com/](Excelidraw)

---