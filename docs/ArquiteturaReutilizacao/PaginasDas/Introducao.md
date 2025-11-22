# Documento de Arquitetura de Software

## Introdução

### Objetivo

Este documento tem como objetivo apresentar a arquitetura do sistema **EuRecomendo**, fornecendo uma visão abrangente e detalhada de suas estruturas, componentes, decisões arquiteturais e padrões aplicados.

O documento serve como:
- **Guia de referência** para desenvolvedores e arquitetos
- **Base para tomada de decisões** técnicas
- **Documentação** para manutenção e evolução do sistema
- **Comunicação** entre stakeholders técnicos e não-técnicos

### Escopo

Este documento cobre a arquitetura completa do sistema EuRecomendo, incluindo:

- **Estrutura do Sistema**: Organização em camadas, módulos e componentes
- **Comportamento Dinâmico**: Fluxos de processos e interações entre componentes
- **Infraestrutura**: Deployment, servidores e configurações
- **Decisões Arquiteturais**: Justificativas e trade-offs
- **Padrões e Práticas**: Frameworks, bibliotecas e padrões de projeto aplicados

O escopo **não inclui**:
- Detalhes de implementação de algoritmos específicos
- Código-fonte completo
- Procedimentos operacionais detalhados
- Documentação de APIs (coberta em documento separado)

### Público-Alvo

Este documento é destinado a:
- **Arquitetos de Software**: Para entender e evoluir a arquitetura
- **Desenvolvedores**: Para implementar funcionalidades seguindo os padrões estabelecidos
- **Engenheiros de DevOps**: Para configurar infraestrutura e deployment
- **Gerentes de Projeto**: Para entender capacidades e limitações técnicas
- **Estudantes e Pesquisadores**: Para fins acadêmicos e de aprendizado

## Definições, Acrônimos e Abreviações

### Termos do Domínio

| Termo | Definição |
|-------|-----------|
| **Recomendação** | Sugestão de livro gerada pelo sistema baseada em algoritmos |
| **Avaliação** | Nota e comentário atribuído por um usuário a um livro |
| **Biblioteca Pessoal** | Coleção de livros de um usuário (lidos, lendo, desejados) |
| **Perfil de Leitura** | Conjunto de preferências e histórico de um usuário |
| **Score de Recomendação** | Valor numérico indicando relevância de uma recomendação |

### Acrônimos Técnicos

| Acrônimo | Significado |
|----------|-------------|
| **API** | Application Programming Interface |
| **DAS** | Documento de Arquitetura de Software |
| **DTO** | Data Transfer Object |
| **JWT** | JSON Web Token |
| **ORM** | Object-Relational Mapping |
| **REST** | Representational State Transfer |
| **CRUD** | Create, Read, Update, Delete |
| **ML** | Machine Learning |
| **WSGI** | Web Server Gateway Interface |

### Abreviações de Frameworks e Tecnologias

| Abreviação | Tecnologia Completa |
|------------|---------------------|
| **DRF** | Django REST Framework |
| **PostgreSQL** | PostgreSQL Database Management System |
| **Redis** | Remote Dictionary Server |
| **Celery** | Distributed Task Queue |
| **Docker** | Container Platform |
| **Nginx** | Web Server and Reverse Proxy |

## Contexto do Sistema

### Visão Geral

O **EuRecomendo** é um sistema web de recomendação de livros que utiliza algoritmos de machine learning para sugerir leituras personalizadas aos usuários. O sistema analisa o histórico de leituras, avaliações e preferências declaradas para gerar recomendações relevantes.

### Problema a Resolver

Com a vasta quantidade de livros disponíveis, leitores frequentemente enfrentam dificuldade em descobrir novos títulos que correspondam aos seus gostos. O EuRecomendo resolve este problema através de:

1. **Filtragem Colaborativa**: Encontra usuários com gostos similares
2. **Filtragem Baseada em Conteúdo**: Analisa características dos livros
3. **Sistema Híbrido**: Combina ambas abordagens para melhores resultados

### Stakeholders

| Stakeholder | Interesse | Preocupações |
|-------------|-----------|--------------|
| **Usuários Leitores** | Descobrir novos livros relevantes | Qualidade das recomendações, privacidade |
| **Desenvolvedores** | Implementar e manter o sistema | Qualidade do código, documentação |
| **Arquitetos** | Garantir qualidade arquitetural | Escalabilidade, manutenibilidade |
| **Equipe de Produto** | Entregar valor aos usuários | Features, usabilidade |
| **Administradores** | Gerenciar catálogo e usuários | Ferramentas de administração |

### Artefatos de Contexto Reutilizados (Entrega 01)

<p align="center">
  <img src="./assets/outros/rich-picture.png" alt="Rich Picture EuRecomendo" width="720">
</p>
<div align="center"><font size="3">Figura 1 – Rich picture produzido na Entrega 01, reutilizado como visão de contexto.</font></div>

<p align="center">
  <img src="./assets/outros/storyboard.png" alt="Storyboard EuRecomendo" width="720">
</p>
<div align="center"><font size="3">Figura 2 – Storyboard da experiência do usuário (Entrega 01), base para os cenários do DAS.</font></div>

## Representação Arquitetural

### Visão de Alto Nível

O sistema EuRecomendo segue uma arquitetura em camadas com os seguintes componentes principais:

```
┌─────────────────────────────────────────┐
│         Camada de Apresentação          │
│    (Django REST Framework - API)        │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│       Camada de Lógica de Negócio       │
│  (Services, Recommendation Engine)      │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│         Camada de Persistência          │
│      (Django ORM + PostgreSQL)          │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│       Camada de Infraestrutura          │
│    (Redis Cache, Celery Workers)        │
└─────────────────────────────────────────┘
```

### Princípios Arquiteturais

1. **Separação de Responsabilidades**: Cada camada tem responsabilidades bem definidas
2. **Baixo Acoplamento**: Módulos independentes com interfaces claras
3. **Alta Coesão**: Componentes com funcionalidades relacionadas agrupados
4. **Reutilização**: Uso extensivo de frameworks e bibliotecas estabelecidas
5. **Testabilidade**: Arquitetura que facilita testes automatizados

## Restrições e Premissas

### Restrições Técnicas

- **Linguagem**: Python 3.10 ou superior
- **Framework Web**: Django 4.x
- **Banco de Dados**: PostgreSQL 14 ou superior
- **Deployment**: Containerização obrigatória (Docker)
- **Autenticação**: JWT para APIs stateless

### Restrições de Negócio

- **Privacidade**: Conformidade com LGPD
- **Performance**: Recomendações em menos de 2 segundos
- **Disponibilidade**: Sistema disponível 99.5% do tempo
- **Escalabilidade**: Suportar crescimento de 100% ao ano

### Premissas

- Usuários têm acesso à internet
- Navegadores modernos com suporte a JavaScript
- Dados de livros disponíveis via APIs externas ou importação
- Infraestrutura cloud disponível para deployment

## Referências

1. **Material da Disciplina**: Arquitetura e Desenho de Software - UnB, 2025.2
2. **Django Documentation**: https://docs.djangoproject.com/
3. **Django REST Framework**: https://www.django-rest-framework.org/
4. **KRUCHTEN, Philippe**: The 4+1 View Model of Architecture. IEEE Software, 1995.
5. **BASS, Len et al.**: Software Architecture in Practice. 3rd ed. Addison-Wesley, 2012.

## Histórico de Versões

| **Data**       | **Versão** | **Descrição**                         | **Autor**                                      | **Revisor**                                      | **Data da Revisão** |
| :--------: | :----: | :-------------------------------- | :----------------------------------------: | :----------------------------------------: | :-------------: |
| 21/11/2025 |  `1.0`   | Criação da introdução do DAS | Pedro Braga ([@Stain19](https://github.com/Stain19)) | - |   -    |
