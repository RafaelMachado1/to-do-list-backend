# Passo-a-passo Express

## Vídeo tutorial

[to-do-list-configuracao-express](https://drive.google.com/file/d/1-LD9ECyKBvkZpQST5h8Du2VNSWcnpcpG/view?usp=share_link)

## Iniciando o npm

Criação do arquivo de configuração package.json.

```bash
npm init -y
```

### package.json

Definição dos scripts.

```json
{
    "name": "to-do-list-backend",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    **"scripts": {
        "start": "node ./build/index.js",
        "build": "tsc",
        "dev": "ts-node-dev ./src/index.ts"
    },**
    "keywords": [],
    "author": "",
    "license": "ISC"
}
```

## Instalando o typescript

E também as tipagens do node e o ts-node-dev para facilitar o desenvolvimento do código. São todas dependências de desenvolvimento, por isso o -D.

```bash
npm i -D typescript @types/node ts-node-dev
```

## Configurando o typescript

Criação do arquivo de configuração tsconfig.json.

```bash
npx tsc --init
```

### tsconfig.json

Definição das flags.

```json
{
    "compilerOptions": {
        "target": "ES6",
        "module": "commonjs",   
        "sourceMap": true,       
        "outDir": "./build",      
        "rootDir": "./src",       
        "removeComments": true,   
        "noImplicitAny": true,      
        "esModuleInterop": true,
        "noEmitOnError": true,
        "strict": true
    }
}
```

## Instalando o express e o cors

São dependências de produção.

- Express = framework para criar o servidor (será a API)
- Cors = biblioteca para liberar acesso externo ao servidor

```bash
npm i express cors
```

## Instalando as tipagens do express e do cors

São dependências de desenvolvimento.

```bash
npm i -D @types/express @types/cors
```

## Criando o servidor

Fica no arquivo `**src/index.ts**`.

```tsx
import express, { Request, Response } from 'express'
import cors from 'cors'

const app = express()

app.use(cors())
app.use(express.json())

app.listen(3003, () => {
    console.log(`Servidor rodando na porta ${3003}`)
})

app.get("/ping", async (req: Request, res: Response) => {
    try {
        res.status(200).send({ message: "Pong!" })
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

## Testando o servidor

Agora é só executá-lo com o script dev e testá-lo no Postman via o endpoint **GET /ping**.