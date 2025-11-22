# EuRecomendo - Arquitetura e Reutilização de Software

Bem-vindo à documentação de arquitetura do projeto **EuRecomendo**, um sistema de recomendação de livros baseado em preferências do usuário e algoritmos de machine learning.

## Sobre o Projeto

O **EuRecomendo** é uma plataforma que permite aos usuários:
- Descobrir novos livros através de recomendações personalizadas
- Avaliar e comentar sobre livros lidos
- Gerenciar sua biblioteca pessoal
- Receber sugestões baseadas em seus gostos e histórico de leitura

## Documentação de Arquitetura

Esta entrega apresenta a **Documentação de Arquitetura de Software (DAS)** completa do sistema, seguindo o modelo 4+1 do RUP:

- **Visão de Casos de Uso**: Funcionalidades e interações do sistema
- **Visão Lógica**: Estrutura de classes e pacotes
- **Visão de Processo**: Fluxos dinâmicos e comportamento em tempo de execução
- **Visão de Implantação**: Infraestrutura e deployment
- **Visão de Implementação**: Organização do código e módulos

## Artefatos Reutilizados das Entregas 01-03

- Rich picture e storyboard de contexto (Entrega 01)
- Diagramas UML consolidados (pacotes, classes, casos de uso, atividades, sequência, implantação) trazidos da Entrega 02
- Diagramas de padrões GoF (Adapter, Builder, Iterator) da Entrega 03
- Todos os arquivos estão em `docs/assets/` e são referenciados nas seções do DAS e da documentação de reutilização

## Tecnologias

- **Backend**: Django 4.x + Django REST Framework
- **Banco de Dados**: PostgreSQL
- **Cache/Message Broker**: Redis
- **Task Queue**: Celery
- **Autenticação**: JWT (SimpleJWT)

## Equipe

| Membro | GitHub |
|--------|--------|
| Pedro Braga | [@Stain19](https://github.com/Stain19) |

## Navegação

Use o menu lateral para navegar pela documentação completa de arquitetura e reutilização de software.
