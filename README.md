# Ollama-SQLite-Chatbot

🚀 **Ollama-SQLite-Chatbot** é um projeto Java que permite fazer consultas a um banco de dados SQLite usando linguagem natural. Ele utiliza a API do **Ollama** para converter perguntas em SQL e executar automaticamente no banco.

## 📌 Funcionalidades

✅ Consulta de dados do banco SQLite usando perguntas em linguagem natural  
✅ Geração dinâmica de queries SQL pela IA do Ollama  
✅ Operações CRUD na tabela `sala`  
✅ Integração com **Maven** e **SQLite-JDBC**  

## 🛠 Tecnologias Utilizadas

- **Java 21**
- **SQLite (sqlite-jdbc)**
- **Ollama4J** (Cliente Java para a API do Ollama)
- **Maven** (Gerenciamento de dependências)

## 📂 Estrutura do Projeto

```
├── src/main/java/org/example
│   ├── Main.java        # Classe principal, inicializa banco e IA
│   ├── Sala.java        # Classe para operações no banco SQLite
│
├── src/main/resources
│   ├── database.db      # Arquivo SQLite (criado dinamicamente)
│
├── pom.xml             # Configuração do Maven e dependências
```

## 🏗 Instalação e Execução

### 🔹 Pré-requisitos

- Ter o [Java 21+](https://adoptium.net/) instalado
- Instalar o **Ollama** localmente ([Guia de instalação](https://ollama.ai/))
- Ter **Maven** instalado ([Download Maven](https://maven.apache.org/download.cgi))

### 🔹 Clonar o repositório

```sh
git clone https://github.com/seu-usuario/Ollama-SQLite-Chatbot.git
cd Ollama-SQLite-Chatbot
```

### 🔹 Compilar e executar

```sh
mvn clean install
mvn exec:java -Dexec.mainClass="org.example.Main"
```

## ⚙️ Como Funciona

### 🗂 Configuração do Banco de Dados

A tabela `sala` é criada automaticamente caso ainda não exista:

```sql
CREATE TABLE IF NOT EXISTS sala (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome VARCHAR(45) NOT NULL,
    RA VARCHAR(45) UNIQUE NOT NULL
);
```

### 🔍 Exemplo de Consulta

Na classe `Main.java`, há um método que faz perguntas ao banco de dados:

```java
String pergunta = "quantos registros tem na tabela sala?";
OllamaResult sqlResult = ollamaAPI.generate("qwen2.5:3b",
    "Converta essa pergunta para uma consulta SQL válida no SQLite: " + pergunta,
    true, new OptionsBuilder().build());
String consultaSQL = sqlResult.getResponse().trim();
String respostaDB = executarConsulta(consultaSQL);
```

💬 Se perguntarmos **"Quais são os registros da tabela sala?"**, a IA gerará a query:

```sql
SELECT * FROM sala;
```

E retornará o resultado do banco de dados.

## 🏗 Dependências (pom.xml)

```xml
<dependencies>
    <dependency>
        <groupId>org.xerial</groupId>
        <artifactId>sqlite-jdbc</artifactId>
        <version>3.49.1.0</version>
    </dependency>

    <dependency>
        <groupId>io.github.ollama4j</groupId>
        <artifactId>ollama4j</artifactId>
        <version>1.0.93</version>
    </dependency>
</dependencies>
```

## 🛠 Extensões e Melhorias Futuras

- 📌 Suporte para múltiplas tabelas  
- 🤖 Melhor interpretação de linguagem natural  
- 🔍 Histórico de consultas salvas  
- 📊 Integração com um painel de visualização dos dados  

## 📜 Licença

Este projeto está sob a licença MIT.

---

💡 **Dúvidas ou sugestões?** Abra uma issue ou contribua com melhorias! 🚀
