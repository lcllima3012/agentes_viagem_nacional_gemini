# Sistema de Criação de Conteúdo de Viagem com Agentes Gemini

Este projeto utiliza o poder dos modelos Gemini do Google para automatizar a criação de conteúdo de viagem. Ele emprega uma arquitetura com múltiplos agentes, cada um especializado em uma etapa do processo: busca de informações sobre destinos, planejamento de viagens, redação de e-mails marketing e revisão de conteúdo.

## Visão Geral

O sistema funciona da seguinte maneira:

1.  **Busca de Destinos (Agente 1):** Coleta informações relevantes sobre um destino específico (pontos turísticos, restaurantes, atrações, acomodações, melhor época para visitar, etc.) utilizando a busca do Google. As informações priorizam avaliações positivas e atualidade.
2.  **Planejamento de Viagem (Agente 2):** Com base no destino e na cidade de origem, este agente planeja a viagem, buscando informações sobre passagens aéreas/terrestres (com valores em reais), acomodações, passeios e outros detalhes relevantes.
3.  **Redação de E-mail Marketing (Agente 3):** Utiliza as informações coletadas e o plano de viagem para redigir um rascunho de e-mail marketing cativante, com o objetivo de despertar o interesse do leitor em conhecer o destino.
4.  **Revisão de Qualidade (Agente 4):** Revisa o rascunho do e-mail, verificando clareza, concisão, correção e tom adequado para um público diversificado.

## Pré-requisitos

Antes de executar o código, você precisará:

* **Ter uma conta Google Cloud com acesso ao Gemini API.**
* **Configurar uma chave de API do Google Gemini.**
* **Ter o Python instalado em seu ambiente.**
* **Utilizar o Google Colab ou um ambiente Python com as bibliotecas necessárias.**

## Configuração

1.  **Instalação das Bibliotecas:** As seguintes bibliotecas são necessárias para executar o código. As linhas abaixo no código fazem a instalação no ambiente Colab:
    ```python
    %pip -q install google-genai
    %pip install -q google-adk
    ```
    Se você estiver executando em outro ambiente, pode instalar com `pip`:
    ```bash
    pip install google-genai google-adk
    ```

2.  **Configuração da Chave de API:** A chave de API do Google Gemini é armazenada de forma segura usando o recurso `userdata` do Google Colab.
    * No Google Colab, vá em `Secrets` (ícone de chave na barra lateral esquerda).
    * Crie um novo segredo com o nome `GOOGLE_API_KEY` e cole sua chave de API no campo de valor.
    * O código abaixo carrega a chave de API para uma variável de ambiente:
        ```python
        import os
        from google.colab import userdata

        os.environ["GOOGLE_API_KEY"] = userdata.get('GOOGLE_API_KEY')
        ```
    * **Importante:** Se você não estiver usando o Google Colab, precisará configurar a variável de ambiente `GOOGLE_API_KEY` de outra forma segura em seu sistema.

## Como Usar

1.  **Execute as células de código no ambiente Colab (ou em seu ambiente Python configurado).**
2.  **Quando solicitado, insira as informações sobre a viagem:**
    * Cidade de destino
    * Estado de destino
    * Cidade de origem
    * Estado de origem

3.  **O sistema de agentes irá processar sua solicitação em quatro etapas:**
    * **Agente Buscador:** Buscará informações sobre o destino.
    * **Agente Planejador:** Criará um plano de viagem.
    * **Agente Redator:** Redigirá um rascunho de e-mail marketing.
    * **Agente Revisor:** Revisará o rascunho do e-mail.

4.  **Os resultados de cada agente serão exibidos na tela em formato Markdown.** O resultado final será o e-mail marketing revisado.

## Estrutura do Código

O código é organizado em seções bem definidas:

* **Instalação de Bibliotecas:** Garante que as dependências necessárias estejam instaladas.
* **Configuração da API Key:** Autentica o acesso aos serviços Gemini.
* **Configuração do Cliente Gemini SDK:** Inicializa o cliente para interagir com os modelos Gemini.
* **Funções Auxiliares:**
    * `call_agent()`: Envia uma mensagem para um agente e retorna a resposta final.
    * `to_markdown()`: Formata o texto para exibição em Markdown no Colab.
* **Agentes:**
    * `agente_buscador()`: Implementa a lógica do agente de busca de destinos.
    * `agente_planejador()`: Implementa a lógica do agente de planejamento de viagens.
    * `agente_redator()`: Implementa a lógica do agente redator de e-mails.
    * `agente_revisor()`: Implementa a lógica do agente revisor de qualidade.
* **Fluxo Principal:** Obtém a entrada do usuário, executa os agentes em sequência e exibe os resultados.

## Observações

* O modelo `gemini-2.0-flash` foi escolhido para este projeto, buscando um equilíbrio entre velocidade e qualidade das respostas.
* A ferramenta `google_search` é utilizada pelos agentes de busca e planejamento para obter informações atualizadas da web.
* As instruções fornecidas a cada agente (`instruction` dentro da definição do `Agent`) são cruciais para direcionar seu comportamento e a qualidade de suas respostas.
* A formatação em Markdown facilita a leitura dos resultados no ambiente Colab.

## Contribuições

Contribuições para melhorar este projeto são bem-vindas\! Sinta-se à vontade para propor melhorias, adicionar novos recursos ou corrigir bugs.


