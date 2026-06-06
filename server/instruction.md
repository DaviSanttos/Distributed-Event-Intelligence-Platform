# Jarvis MVP - Voz → Texto → IA → Voz

## Objetivo

Criar um assistente de voz local capaz de:

1. Capturar áudio do microfone.
2. Converter fala em texto.
3. Enviar o texto para uma IA local.
4. Receber uma resposta.
5. Converter a resposta em voz.
6. Reproduzir o áudio para o usuário.

---

# Arquitetura

```text
Microfone
    ↓
Faster-Whisper
    ↓
Ollama
    ↓
Piper
    ↓
Alto-falante
```

---

# Tecnologias

## Backend

* Node.js
* TypeScript

## Speech To Text

* Faster-Whisper

Responsável por converter voz em texto.

Exemplo:

Usuário fala:

"Qual a previsão do tempo?"

Resultado:

```text
Qual a previsão do tempo?
```

---

## IA

* Ollama

Responsável por gerar respostas.

Modelos recomendados:

* qwen3
* llama3
* gemma

Exemplo:

Entrada:

```text
Qual a previsão do tempo?
```

Saída:

```text
Hoje o clima está ensolarado.
```

---

## Text To Speech

* Piper

Responsável por converter texto em voz.

Entrada:

```text
Hoje o clima está ensolarado.
```

Saída:

```text
audio.wav
```

---

# Estrutura do Projeto

```text
jarvis/
│
├── src/
│   ├── audio/
│   │   ├── recorder.ts
│   │   ├── speechToText.ts
│   │   └── textToSpeech.ts
│   │
│   ├── ai/
│   │   └── ollama.ts
│   │
│   ├── core/
│   │   └── assistant.ts
│   │
│   └── index.ts
│
├── recordings/
│
├── generated/
│
├── package.json
│
└── tsconfig.json
```

---

# Fluxo Principal

## 1 - Gravar áudio

O sistema inicia a gravação do microfone.

Arquivo gerado:

```text
recordings/input.wav
```

---

## 2 - Transcrever áudio

Enviar o arquivo para o Faster-Whisper.

Entrada:

```text
recordings/input.wav
```

Saída:

```text
"Qual a previsão do tempo?"
```

---

## 3 - Consultar IA

Enviar o texto para o Ollama.

Exemplo:

```text
Usuário:
Qual a previsão do tempo?
```

Resposta:

```text
Hoje o clima está ensolarado.
```

---

## 4 - Gerar voz

Enviar resposta para o Piper.

Entrada:

```text
Hoje o clima está ensolarado.
```

Saída:

```text
generated/response.wav
```

---

## 5 - Reproduzir áudio

Executar o áudio gerado.

Resultado:

O usuário ouve a resposta.

---

# Classe Principal

```ts
class Assistant {
    async listen(): Promise<string>;
    async think(prompt: string): Promise<string>;
    async speak(text: string): Promise<void>;
}
```

Fluxo:

```ts
const question = await assistant.listen();

const answer = await assistant.think(question);

await assistant.speak(answer);
```

---

# Primeira Meta

Fazer funcionar apenas:

* Gravação de áudio.
* Transcrição.
* Resposta da IA.
* Reprodução da voz.

Sem:

* Memória.
* Comandos do computador.
* Hotword "Jarvis".
* Integrações externas.

---

# Segunda Meta

Adicionar ativação por voz.

Exemplo:

```text
Jarvis
```

Quando detectar a palavra:

```text
Jarvis, abra o VS Code.
```

O sistema começa a escutar comandos.

---

# Terceira Meta

Adicionar memória.

Exemplo:

```text
Meu nome é Davi.
```

Salvar em banco local:

```json
{
  "name": "Davi"
}
```

Depois:

```text
Qual meu nome?
```

Resposta:

```text
Seu nome é Davi.
```

---

# Quarta Meta

Controle do computador.

Exemplos:

```text
Abra o Chrome.
```

```text
Abra o VS Code.
```

```text
Abra o Docker Desktop.
```

---

# Quinta Meta

Modo Agente.

Capacidades:

* Ler arquivos.
* Criar arquivos.
* Executar comandos.
* Corrigir código.
* Rodar testes.
* Automatizar tarefas.

---

# Resultado Esperado

Ao final do MVP:

Usuário:

"Jarvis, como funciona uma árvore B+?"

Jarvis:

1. Escuta a pergunta.
2. Converte para texto.
3. Consulta o modelo local.
4. Gera a resposta.
5. Fala a resposta em voz alta.

Tudo executando localmente e sem custos de API.
