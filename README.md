# 
Sistema de Controle de Inventário de Bens Corporativos

Este projeto é uma **aplicação web frontend** desenvolvida em HTML, CSS (com **Tailwind CSS**) e JavaScript puro, projetada para interagir com um **Google Apps Script Web App** como backend. Ele permite o **controle de inventário de bens corporativos**, como os da Fazenda Morro Alto, oferecendo funcionalidades para **adicionar novos itens** e **visualizar a lista completa de bens**, além de permitir o **download dos dados em formato CSV**.

---

## ✨ Visão Geral

O objetivo principal deste sistema é fornecer uma interface amigável para gerenciar o inventário de ativos. Ele simplifica o registro de bens, incluindo detalhes como categoria, valor, vida útil, dados de aquisição e histórico de manutenção. A integração com o Google Apps Script e o Google Sheets permite que os dados sejam armazenados de forma centralizada e acessível, sem a necessidade de um banco de dados tradicional.

---

## 🚀 Funcionalidades

* **Adição de Novos Bens:** Um formulário abrangente permite registrar novos itens com diversas informações detalhadas.
* **Cálculo Automático de Depreciação:** Calcula a depreciação anual (linear) com base no valor de aquisição, vida útil e valor residual.
* **Visualização do Inventário:** Exibe todos os bens registrados em uma tabela dinâmica e fácil de ler.
* **Download de Dados (CSV):** Permite exportar todo o inventário para um arquivo CSV, facilitando análises e relatórios offline.
* **Indicadores Visuais:** Possui um indicador de carregamento para feedback do usuário durante operações de rede e caixas de mensagem para alertas.

---

## 🛠️ Tecnologias Utilizadas

* **HTML5:** Estrutura da página web.
* **Tailwind CSS:** Framework CSS para estilização rápida e responsiva.
* **JavaScript (ES6+):** Lógica frontend para interação com o usuário, manipulação do DOM e comunicação com o backend.
* **Google Apps Script:** Backend sem servidor para interação com o Google Sheets, atuando como um "banco de dados" e API.
* **Google Sheets:** Armazenamento dos dados do inventário.

---

## ⚙️ Como Instalar e Rodar

Este projeto consiste em um frontend (este arquivo HTML/CSS/JS) e um backend (Google Apps Script).

### Pré-requisitos

1.  Uma conta Google.
2.  Acesso ao Google Sheets e Google Apps Script.

### Configuração do Google Apps Script (Backend)

1.  Crie uma nova **planilha Google Sheets** para o inventário (ex: "Inventário Morro Alto").
2.  Nomeie as colunas da primeira linha da sua planilha exatamente como as chaves dos objetos JavaScript (ex: `category`, `itemName`, `description`, `quantity`, `condition`, `usageCondition`, `supplier`, `value`, `usefulLife`, `residualValue`, `annualDepreciation`, `acquisitionDate`, `assetId`, `status`, `lastMaintenanceDate`, `nextMaintenanceDate`, `costCenter`, `invoiceNumber`, `warrantyExpirationDate`, `attachmentLink`, `movementHistory`, `notes`). A ordem não é crucial, mas os nomes devem ser idênticos.
3.  No Google Sheets, vá em `Extensões > Apps Script`.
4.  No editor do Apps Script, substitua o código existente pelo seu código do Apps Script que lida com as requisições `GET` e `POST` para ler e escrever na planilha.
    * **Função `doGet(e)`:** Deve retornar os dados da planilha em formato JSON.
    * **Função `doPost(e)`:** Deve receber os dados de um novo item em JSON e adicioná-los à planilha.
5.  **Implante o projeto como um aplicativo da web:**
    * No editor do Apps Script, clique em `Implantar > Nova implantação`.
    * Selecione o tipo de implantação como **"Aplicativo da web"**.
    * Configure a opção **"Executar como"** para **"Minha própria conta"**.
    * Configure a opção **"Quem tem acesso"** para **"Qualquer pessoa"**.
    * Clique em "Implantar". Copie o **"URL do aplicativo da web"** que será gerado.

### Configuração do Frontend (Este Arquivo HTML)

1.  Abra o arquivo `index.html` (o código que você forneceu).
2.  Localize a linha que define `APP_SCRIPT_WEB_APP_URL`:
    ```javascript
    const APP_SCRIPT_WEB_APP_URL = '[https://script.google.com/macros/s/AKfycbwSzGjXpgDdvxvyL2JwPCct9tZKPD-eBu5fz2Y9O2YVS8NTtQSsU9pZxh9pJY_nAP47fA/exec](https://script.google.com/macros/s/AKfycbwSzGjXpgDdvxvyL2JwPCct9tZKPD-eBu5fz2Y9O2YVS8NTtQSsU9pZxh9pJY_nAP47fA/exec)';
    ```
3.  **Substitua o URL** pelo URL do Google Apps Script Web App que você copiou no passo anterior.
4.  **Para executar localmente:** Devido a restrições de segurança do navegador (CORS), o navegador não permite que um arquivo HTML local (`file://`) faça requisições para URLs HTTPS externas.
    * A maneira mais fácil de contornar isso para desenvolvimento é usar um **servidor web local simples**. Se você tem Python instalado, pode navegar até o diretório onde `index.html` está e executar no terminal:
        ```bash
        python -m http.server 8000
        ```
        Então, acesse `http://localhost:8000/index.html` no seu navegador.
    * Alternativamente, você pode **hospedar o arquivo HTML** em um serviço como GitHub Pages, Netlify, Firebase Hosting, etc.

---

## 💡 Uso

1.  **Carregamento Inicial:** Ao abrir a página, o sistema tenta carregar os dados existentes do Google Sheet e exibi-los na tabela.
2.  **Adicionar Novo Bem:**
    * Preencha os campos do formulário "Adicionar Novo Bem".
    * Os campos "Valor (R$)", "Vida Útil (anos)" e "Valor Residual (R$)" são usados para calcular automaticamente a "Depreciação Anual (R$)".
    * Clique no botão "Adicionar Bem". Os dados serão enviados para o Google Sheet.
3.  **Visualizar e Pesquisar:** A tabela exibirá os itens do inventário. Atualmente, não há funcionalidade de pesquisa/filtro no frontend, mas você pode usar os recursos de pesquisa do seu navegador (`Ctrl+F` ou `Cmd+F`).
4.  **Baixar CSV:** Clique no botão "Baixar como CSV" para exportar os dados exibidos na tabela para um arquivo CSV.

---
