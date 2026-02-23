# 🛒 E-commerce API — Python + Flask

API RESTful para e-commerce desenvolvida como projeto de um curso introdutório de Python e Flask. Utiliza SQLite como banco de dados e autenticação de sessão com Flask-Login.

---

## 🚀 Tecnologias Utilizadas

- **Python 3**
- **Flask 2.3** — framework web
- **Flask-SQLAlchemy** — ORM para banco de dados
- **Flask-Login** — gerenciamento de autenticação/sessão
- **Flask-CORS** — suporte a Cross-Origin Resource Sharing
- **SQLite** — banco de dados local
- **Postman** — ferramenta utilizada para testar os endpoints

---

## 📦 Instalação

```bash
# Clone o repositório
git clone <url-do-repositorio>
cd python-flask-introductory-main

# Crie e ative um ambiente virtual
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Instale as dependências
pip install -r requirements.txt
```

### Criando o banco de dados

Antes de rodar pela primeira vez, crie as tabelas no banco:

```bash
python
>>> from application import application, db
>>> with application.app_context():
...     db.create_all()
>>> exit()
```

### Rodando a aplicação

```bash
python application.py
```

A API estará disponível em `http://localhost:5000`.

---

## 🔐 Autenticação

A API usa autenticação baseada em sessão (cookie). Faça login antes de acessar os endpoints protegidos.

### Login
`POST /login`

```json
{
  "username": "seu_usuario",
  "password": "sua_senha"
}
```

### Logout
`POST /logout` *(requer autenticação)*

---

## 📌 Endpoints

### Produtos

| Método | Rota | Auth | Descrição |
|--------|------|------|-----------|
| `GET` | `/api/products` | ❌ | Lista todos os produtos |
| `GET` | `/api/products/<id>` | ❌ | Detalhes de um produto |
| `POST` | `/api/products/add` | ✅ | Adiciona um produto |
| `PUT` | `/api/products/update/<id>` | ✅ | Atualiza um produto |
| `DELETE` | `/api/products/delete/<id>` | ✅ | Remove um produto |

**Exemplo — Adicionar produto:**
```json
{
  "name": "Teclado Mecânico",
  "price": 349.90,
  "description": "Teclado com switches blue"
}
```

---

### Carrinho

| Método | Rota | Auth | Descrição |
|--------|------|------|-----------|
| `GET` | `/api/cart` | ✅ | Visualiza o carrinho |
| `POST` | `/api/cart/add/<product_id>` | ✅ | Adiciona item ao carrinho |
| `DELETE` | `/api/cart/remove/<product_id>` | ✅ | Remove item do carrinho |
| `POST` | `/api/cart/checkout` | ✅ | Finaliza compra (limpa carrinho) |

---

## 🗄️ Modelos de Dados

**User** — `id`, `username`, `password`

**Product** — `id`, `name`, `price`, `description`

**CartItem** — `id`, `user_id`, `product_id`

---

## 🧪 Testando com Postman

1. Importe as rotas acima no Postman
2. Faça uma requisição `POST /login` com suas credenciais
3. O Postman salvará o cookie de sessão automaticamente — use nas demais requisições
4. Para rotas que enviam dados, defina o `Content-Type` como `application/json` no header

---

## ⚠️ Observações

- A `SECRET_KEY` está exposta no código — em produção, use variáveis de ambiente
- As senhas são armazenadas em texto puro — em produção, utilize hashing (ex: `bcrypt`)
- O banco SQLite é ideal para desenvolvimento; em produção, considere PostgreSQL ou MySQL

---

## 👨‍💻 Sobre o Projeto

Projeto desenvolvido como parte de um curso introdutório de Python e Flask, explorando conceitos de criação de APIs REST, modelagem de banco de dados com SQLAlchemy e autenticação de usuários.
