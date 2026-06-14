# Configuração do Ambiente Local

Este projeto usa variáveis de ambiente para proteger as credenciais do banco de dados.
O arquivo `.env.example` na raiz do projeto lista todas as variáveis necessárias.

## Passo 1 — Criar seu `.env` local

Copie o arquivo de exemplo e preencha com as credenciais reais:

```bash
cp .env.example .env
```

Edite o `.env` com os valores fornecidos pelo responsável do projeto:

```
DB_URL=jdbc:postgresql://<host>:<porta>/<banco>?sslmode=require
DB_USERNAME=seu_usuario
DB_PASSWORD=sua_senha
```

> O arquivo `.env` está no `.gitignore` e nunca deve ser commitado.

---

## Configuração no IntelliJ IDEA

### Opção A — Inserir variáveis manualmente

1. Vá em **Run > Edit Configurations...**
2. Selecione a configuração `AcademiaApplication`
3. Clique no ícone de pasta ao lado de **Environment variables**
4. Adicione cada variável (`DB_URL`, `DB_USERNAME`, `DB_PASSWORD`) com seus valores
5. Clique **OK** e rode a aplicação normalmente

### Opção B — Usar o plugin EnvFile (lê o `.env` automaticamente)

1. Instale o plugin: **Settings > Plugins > buscar "EnvFile"**
2. Nas configurações de run da aplicação, vá na aba **EnvFile**
3. Ative a opção **Enable EnvFile**
4. Clique em **+** e aponte para o arquivo `.env` na raiz do projeto
5. Salve e rode normalmente

---

## Configuração no VSCode

1. Crie (ou edite) o arquivo `.vscode/launch.json` na raiz do projeto
2. Adicione a configuração abaixo:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "java",
      "name": "Spring Boot - Academia",
      "request": "launch",
      "mainClass": "br.edu.ifpb.academia.AcademiaApplication",
      "env": {
        "DB_URL": "jdbc:postgresql://<host>:<porta>/<banco>?sslmode=require",
        "DB_USERNAME": "seu_usuario",
        "DB_PASSWORD": "sua_senha"
      }
    }
  ]
}
```

3. Substitua os valores pelos fornecidos pelo responsável do projeto
4. Use **Run > Start Debugging** ou **F5** para iniciar

> O `.vscode/` está no `.gitignore`, então esse arquivo não vai para o repositório.

---

## Rodando pelo terminal

Se preferir rodar via terminal sem IDE, exporte as variáveis antes de iniciar:

### Linux / macOS

```bash
export DB_URL="jdbc:postgresql://..."
export DB_USERNAME="seu_usuario"
export DB_PASSWORD="sua_senha"
./mvnw spring-boot:run
```

Ou usando o arquivo `.env` diretamente:

```bash
export $(cat .env | xargs) && ./mvnw spring-boot:run
```

### Windows (PowerShell)

```powershell
$env:DB_URL="jdbc:postgresql://..."
$env:DB_USERNAME="seu_usuario"
$env:DB_PASSWORD="sua_senha"
./mvnw spring-boot:run
```

---

## Verificando se funcionou

Com a aplicação rodando, acesse:

- **Swagger UI:** http://localhost:8080/swagger-ui.html
- **API Docs (JSON):** http://localhost:8080/v3/api-docs

Se aparecer a interface do Swagger, a conexão com o banco está funcionando corretamente.
