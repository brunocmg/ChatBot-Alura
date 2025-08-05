# 🤖 ChatBot com Gemini - Alura

Projeto desenvolvido para estudo de **Inteligência Artificial Generativa** utilizando a biblioteca **google-genai**.  
O chatbot se conecta aos modelos **Gemini** do Google, permitindo interações personalizadas com histórico de conversas e diferentes estilos de resposta.

---

## 🎯 Objetivo
Explorar a API de IA generativa do Google para:
- Criar um chatbot interativo em Python.
- Configurar **system instructions** para controlar o comportamento do modelo.
- Manter histórico de conversas.
- Executar comandos em loop com entrada do usuário.

---

## 🛠 Tecnologias Utilizadas
- **Python 3.11+**
- **google-genai** (`pip install google-genai`)
- **Google Colab** (ou qualquer ambiente Python)
- **Google Gemini API**

---

## 📂 Estrutura de Pastas
```
ChatBot-Alura/
├── chatbot.ipynb (Notebook com a implementação do chatbot)
├── requirements.txt (Dependências do projeto)
└── README.md (Documentação do projeto)
```

---

## 🚀 Como Executar o Projeto

### 1️⃣ Clonar o repositório
```bash
git clone https://github.com/brunocmg/ChatBot-Alura.git
```

### 2️⃣ Acesse a pasta do projeto
```bash
cd ChatBot-Alura
```

### 3️⃣ Instalar dependências
```bash
pip install -r requirements.txt
```

### Conteúdo do requirements.txt:
`google-genai`

### 4️⃣ Configurar a API Key do Google
No Google Colab ou ambiente local, adicione:

```bash
import os
from google.colab import userdata  # Apenas no Colab

os.environ['GOOGLE_API_KEY'] = userdata.get('GOOGLE_API_KEY')
```
Ou, no terminal:
```bash
export GOOGLE_API_KEY="SUA_API_KEY"
```

💡 Exemplo de Uso

Listar modelos disponíveis
```
from google import genai

client = genai.Client()

for model in client.models.list():
    print(model.name)
```
Criar chatbot básico
```
modelo = "gemini-2.0-flash"
chat = client.chats.create(model=modelo)

resposta = chat.send_message("Oi, tudo bem?")
print(resposta.text)
```
Chat com system instruction
```
from google.genai import types

chat_config = types.GenerateContentConfig(
    system_instruction="Você é um assistente pessoal e sempre responde de forma sucinta."
)

chat = client.chats.create(model=modelo, config=chat_config)

resposta = chat.send_message("O que é computação quântica?")
print(resposta.text)
```
Loop interativo de chat
```
prompt = input("Esperando prompt: ")

while prompt != "fim":
    resposta = chat.send_message(prompt)
    print("Resposta:", resposta.text, "\n")
    prompt = input("Esperando prompt: ")
```
Histórico de Conversa
```
print(chat.get_history())
```
Exemplo com comportamento sarcástico
```
chat_config_2 = types.GenerateContentConfig(
    system_instruction="Você é um assistente pessoal e sempre responde de forma muito sarcástica."
)

chat_2 = client.chats.create(model=modelo, config=chat_config_2)
resposta = chat_2.send_message("O que é computação quântica?")
print(resposta.text)
```

📄 Licença

Este projeto foi desenvolvido para fins educacionais e de estudo de IA generativa.
