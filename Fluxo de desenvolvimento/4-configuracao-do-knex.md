## Vídeo tutorial

[to-do-list-configuracao-knex](https://drive.google.com/file/d/1YAoaPy1ESUA02f-Z5RhmAXE614mtOjJK/view?usp=share_link)

## Instalação do knex

- Knex = biblioteca query builder para conectar com banco de dados
- SQLite3 = biblioteca do banco de dados SQLite

```bash
npm i knex sqlite3
```

## Instalação das tipagens

```bash
npm i -D @types/knex
```

## Criação da pasta database

Por enquanto todos os arquivos relacionados ao banco de dados estarão na pasta **`src/database`**.

## Criação do arquivo .db

O arquivo se chamará **`src/database/to-do-list.db`.**

## Criação do arquivo .sql

O arquivo se chamará `**src/database/to-do-list.sql**`.

## Criando tabelas e populando

Será feito no arquivo .sql.

Conecte a extensão do VSCode com o arquivo .db e crie as tabelas no formato planejado.

```sql
CREATE TABLE users (
    id TEXT PRIMARY KEY UNIQUE NOT NULL,
    name TEXT NOT NULL,
		email TEXT UNIQUE NOT NULL,
		password TEXT NOT NULL
);

CREATE TABLE tasks (
    id TEXT PRIMARY KEY UNIQUE NOT NULL,
    title TEXT NOT NULL,
		description TEXT NOT NULL,
		created_at TEXT DEFAULT (DATETIME()) NOT NULL,
		status INTEGER DEFAULT (0) NOT NULL
);

CREATE TABLE users_tasks (
		user_id TEXT NOT NULL,
		task_id TEXT NOT NULL,
		FOREIGN KEY (user_id) REFERENCES users (id),
		FOREIGN KEY (task_id) REFERENCES tasks (id)
);

INSERT INTO users (id, name, email, password)
VALUES
	("f001", "Fulano", "fulano@email.com", "fulano123"),
	("f002", "Beltrana", "beltrana@email.com", "beltrana00");

INSERT INTO tasks (id, title, description)
VALUES
	("t001", "Implementar o header", "Criar o componente Header do site"),
	("t002", "Implementar o footer", "Criar o componente Footer do site"),
	("t003", "Testar site", "Teste de usabilidade de todo o site"),
	("t004", "Deploy do site", "Subir o site no surge");

INSERT INTO users_tasks (user_id, task_id)
VALUES
	("f001", "t001"),
	("f002", "t002"),
	("f001", "t003"),
	("f002", "t003");

SELECT * FROM users;
SELECT * FROM tasks;
SELECT * FROM users_tasks;
```

## Configuração do knex

Fica no arquivo **`src/database/knex.ts`**.

```tsx
import knex from 'knex'

export const db = knex({
    client: "sqlite3",
    connection: {
        filename: "./src/database/to-do-list.db", //localização do seu arquivo .db
    },
    useNullAsDefault: true, // definirá NULL quando encontrar valores undefined
    pool: {
        min: 0, // número de conexões, esses valores são os recomendados para sqlite3
        max: 1,
				afterCreate: (conn: any, cb: any) => {
            conn.run("PRAGMA foreign_keys = ON", cb)
        } // configurando para o knex forçar o check das constrainst FK
					// para entender melhor, depois assista o vídeo de refatoração de DELETE users by id
    }
})
```

## Testando a conexão

Refatore o endpoint **GET /ping** para que ele retorne também uma propriedade users contendo o array de itens cadastrados na tabela de usuários.

```tsx
import { db } from './database/knex'

// ... configurações do express

app.get("/ping", async (req: Request, res: Response) => {
    try {
				const result = await db("users")
        res.status(200).send({ message: "Pong!", result })
    } catch (error) {
        console.log(error)

        if (req.statusCode === 200) {
            res.status(500)
        }

        if (error instanceof Error) {
            res.send(error.message)
        } else {
            res.send("Erro inesperado")
        }
    }
})
```

Terminando de confirmar que está tudo ok, pode desfazer as alterações no endpoint **GET /ping.**