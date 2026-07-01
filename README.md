# chatbot

# Engenharia de Prompt – Produto genAI UFPR – Turma 2026

## Sumário

- [Introdução](#introdução)
- [Infraestrutura](#infraestrutura)
- [Modelo Escolhido](#modelo-escolhido)
- [Desenvolvimento](#desenvolvimento)
- [Implantação](#implantação)
- [Discussão](#discussão)

## Introdução

Este repositório se refere a uma aplicação criada durante a especialização de IA Generativa (GenIA) da UFPR, turma de 2026.

Esta aplicação em Python deve ser inicializada em uma máquina na Cloud (utilizada para testes a Oracle Cloud Infrastructure).

Ao utilizar o IP público desta máquina, será possível fazer consultas via prompt para a interface do modelo de LLM carregado nesta Virtual Machine.

## Infraestrutura

Aplicação rodando em **PROD** em uma máquina virtual `VM.Standard.E2.1.Micro`, disponível na OCI Free Tier, com a seguinte configuração:

| Item   | Especificação |
|--------|----------------|
| SO     | Ubuntu 22.04.5 LTS |
| Kernel | Linux 6.8.0-1050-oracle |
| Disco  | 47 GB |
| RAM    | 1 GB |
| CPU    | 1 OCPU (equivalente a 2 vCPU x86 Intel ou AMD) |
| Core   | 1 |

## Modelo Escolhido

- **Nome do modelo:** `meta/llama-3.3-70b-instruct`
- **Justificativa da escolha:** gratuito e disponível na plataforma NVIDIA, além de ser um modelo de uso geral.

## Desenvolvimento

**Arquitetura da aplicação:** API REST recebendo, via interface Streamlit, as perguntas das conversas e disparando, através do `chatlas`, a chamada à API do modelo exposta na NVIDIA.

**Bibliotecas utilizadas:**

```
streamlit>=1.45.0
chatlas>=0.11.0
openai>=1.99.0
python-dotenv>=1.1.0
```

**Estratégia de gerenciamento de credenciais:** arquivo `.env` com as chaves da plataforma NVIDIA (`NVIDIA_API_KEY`) e o token de acesso, além do IP e porta do Ollama em `IP_OLLAMA`.

## Implantação

1. Criar um ambiente virtual Python e ativá-lo.
2. Baixar os arquivos necessários e instalar as dependências:

```bash
pip install -r requirements.txt
```

> **Importante:** ao utilizar a máquina OCI, é necessário liberar o firewall para acesso público ao IP:
> ```bash
> sudo ufw disable
> ```

## Discussão

**Lições aprendidas:** a parte de redes é o principal desafio ao subir a máquina OCI, pois, mesmo após alguns comandos aplicados, a aplicação só ficava disponível em alguns navegadores. Isso aconteceu devido a problemas de cache no acesso à aplicação, resolvido posteriormente conectando com navegadores distintos (por exemplo, Safari). A conexão HTTP acaba sendo identificada como **NÃO SEGURA** e barrada por algumas redes e navegadores.

**Possíveis melhorias futuras:** fluxo de melhoria contínua com o servidor OCI e uma máquina mais robusta para testar melhor a performance.
