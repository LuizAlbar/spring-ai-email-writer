# Email Writer Assistant ✍️🤖

Assistente de respostas de e-mail com IA que se integra diretamente ao Gmail. Construído com **Spring Boot** (backend), **React** (interface de testes) e uma **extensão para Chrome** (injeção no Gmail). Utiliza a API Gemini do Google para gerar respostas contextuais com tom personalizável.

![Java](https://img.shields.io/badge/Java-21-blue.svg)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4-green.svg)
![React](https://img.shields.io/badge/React-19-61dafb.svg)
![Gemini API](https://img.shields.io/badge/Gemini-API-orange.svg)

---
## 🔍 Preview do funcionamento

https://github.com/user-attachments/assets/5aebe900-97ed-4c8f-8bde-30b6ec716276

---

## 🚀 Funcionalidades

- **Resposta com um clique** – Injeção direta na janela de composição do Gmail via extensão.
- **Controle de tom** – Opções para tons Profissional, Casual ou Amigável.
- **Detecção automática de idioma** – A IA responde no mesmo idioma do e-mail original.
- **Interface de Testes** – Web App em React para validar a API de forma isolada.
- **Arquitetura Escalável** – Backend robusto utilizando Spring WebFlux e Clean Architecture.

---

## 🧱 Tecnologias utilizadas

| Componente        | Tecnologia                                  |
|-------------------|---------------------------------------------|
| Backend           | Java 21, Spring Boot 3, WebClient (WebFlux) |
| API de IA         | Google Gemini API (1.5 Flash)               |
| Frontend (testes) | React 19, Material UI (MUI), Axios          |
| Extensão Chrome   | Manifest V3, JavaScript (DOM Observation)   |
| Build / Tooling   | Maven, Vite, Jackson, Lombok                |

---

## 📦 Estrutura do projeto

```text
email-writer-assistant/
├── src/                # API Spring Boot
│   ├── src/main/java/com/email/writer/
│   │   ├── EmailWriterApplication.java
│   │   └── app/
│   │       ├── EmailRequest.java
│   │       ├── EmailGeneratorService.java
│   │       └── EmailGeneratorController.java
│   └── src/main/resources/application.properties
├── frontend/          # Interface React (Vite)
│   └── src/
│       ├── App.jsx
│       └── main.jsx
└── web-extension/              # Extensão para Chrome
    ├── manifest.json
    ├── content.js
    └── content.css
```

## 🔧 Configuração

### Pré-requisitos

- Java 21+ e Maven.
- Node.js 18+ e npm.
- Google Gemini API Key.

### 1. Backend (Spring Boot)

```bash
cd src
```

#### Configure o arquivo src/main/resources/application.properties:
```bash Properties
gemini.api.url=[https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=](https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=)
gemini.api.key=SUA_CHAVE_AQUI
server.port=8080
```

#### Execute a aplicação:
```bash
mvn spring-boot:run
```
### 2. Frontend de testes (React)

```bash
cd frontend-test
npm install
npm run dev
```

#### Acesse http://localhost:5173 para testar a geração de e-mails manualmente.

### 3. Extensão para Chrome

1. Acesse chrome://extensions/ no seu navegador.
2. Ative o Modo do desenvolvedor no canto superior direito.
3. Clique em Carregar sem compactação e selecione a pasta extension/.
4. Vá ao Gmail, clique em "Responder" e localize o botão azul AI Reply.

## 🧪 Endpoint da API
### POST /api/email/generate
#### Corpo da requisição (JSON):

```json
{
  "emailContent": "Olá, gostaria de saber o status do meu pedido #123.",
  "tone": "professional"
}
```
### 🧠 Como funciona

1. Captura: A extensão monitora o DOM do Gmail. Quando uma janela de resposta abre, ela injeta um botão e extrai o conteúdo do e-mail anterior.
2. Processamento: O backend recebe o conteúdo, higieniza e monta um prompt estruturado para o Gemini.
3. IA: O Google Gemini analisa o contexto e gera uma resposta adequada ao tom solicitado.
4. Injeção: O script de conteúdo (Content Script) recebe a resposta e a insere via document.execCommand diretamente na caixa de texto do Gmail.

### 🛠️ Solução de problemas

| Problema        | Possível Solução                                  |
|-------------------|---------------------------------------------|
| Botão não aparece | Recarregue o Gmail ou verifique se a extensão está ativa em chrome://extensions. |
| Erro "Failed to generate" | Verifique se o backend está rodando na porta 8080 e se a API Key é válida.          |
| Texto não é colado   | Certifique-se de que a caixa de resposta do Gmail está em foco antes de clicar.          |
