# Planejamento do Projeto — PetAgenda

## 1. Objetivo do planejamento

Organizar as atividades de documentação, arquitetura, desenvolvimento e testes do PetAgenda, distribuindo as responsabilidades entre os quatro integrantes do grupo.

O objetivo é concluir o desenvolvimento da aplicação até **26/11/2026**, reservando o período restante para validação, testes, correção de erros e preparação da entrega final, prevista para **30/11/2026**.

## 2. Responsabilidades dos integrantes

| Responsabilidade principal | Atividades |
|---|---|
| Cadastro e gerenciamento de pets | Desenvolver o CRUD de pets, implementar pesquisas e filtros e validar os dados dos formulários. |
| Responsáveis e atendimentos | Desenvolver o gerenciamento de responsáveis, o CRUD de atendimentos e o histórico dos pets. |
| API REST e banco de dados | Implementar os endpoints da API REST, configurar os modelos e relacionamentos do banco e desenvolver os relatórios consolidados. |
| Interface e integração externa | Desenvolver a interface visual, integrar a Dog CEO API, implementar a consulta de raças e auxiliar na responsividade das telas. |

### Responsabilidades compartilhadas

Todos os integrantes deverão participar de:

- Elaboração e revisão da documentação.
- Integração dos componentes desenvolvidos.
- Versionamento do código e da documentação no GitHub.
- Revisão das alterações realizadas pelos colegas.
- Execução dos testes e correção de problemas.
- Preparação da versão final para apresentação e entrega.

A distribuição poderá ser ajustada conforme as necessidades do projeto, desde que as responsabilidades sejam registradas e todos contribuam para o desenvolvimento.

## 3. Backlog de atividades

| ID | Atividade | Prioridade | Status |
|---|---|---|---|
| T01 | Organizar o repositório GitHub | Alta | Concluído |
| T02 | Elaborar o documento de visão | Alta | Concluído |
| T03 | Elaborar os casos de uso e suas especificações | Alta | Em andamento |
| T04 | Elaborar a arquitetura da aplicação | Alta | Concluído |
| T05 | Elaborar o modelo de dados | Alta | Concluído |
| T06 | Definir o contrato da API REST | Alta | Pendente |
| T07 | Documentar a integração com a Dog CEO API | Alta | Em andamento |
| T08 | Criar a identidade visual e os protótipos | Média | Pendente |
| T09 | Finalizar o README e a documentação da Fase 1 | Alta | Em andamento |
| T10 | Configurar o projeto Django e o banco de dados | Alta | Pendente |
| T11 | Desenvolver o CRUD de pets | Alta | Pendente |
| T12 | Desenvolver o gerenciamento de responsáveis e atendimentos | Alta | Pendente |
| T13 | Implementar a API REST própria | Alta | Pendente |
| T14 | Implementar relatórios, pesquisas e filtros | Alta | Pendente |
| T15 | Integrar a Dog CEO API ao cadastro de pets | Alta | Pendente |
| T16 | Finalizar as telas e a responsividade | Alta | Pendente |
| T17 | Integrar os componentes e publicar a aplicação | Alta | Pendente |
| T18 | Realizar testes funcionais e de integração | Alta | Pendente |
| T19 | Corrigir os problemas identificados | Alta | Pendente |
| T20 | Revisar a documentação e preparar a entrega | Alta | Pendente |

## 4. Cronograma e marcos do projeto

O planejamento será organizado por etapas, com acompanhamento contínuo do backlog e das atividades de cada integrante.

| Etapa | Atividades | Resultado esperado |
|---|---|---|
| Documentação e arquitetura | Elaborar os documentos, diagramas, modelo de dados, contrato da API e protótipos. | Documentação da Fase 1 concluída. |
| Estrutura inicial | Configurar o Django, o ambiente de desenvolvimento e o banco de dados. | Estrutura básica da aplicação funcionando. |
| Desenvolvimento das funcionalidades | Implementar os cadastros, consultas, atendimentos, relatórios e API REST. | Funcionalidades principais implementadas. |
| Integração e publicação | Integrar a Dog CEO API, finalizar a interface e disponibilizar a aplicação. | Componentes integrados e aplicação publicada. |
| Conclusão do desenvolvimento | Finalizar as funcionalidades previstas e preparar a versão candidata à entrega. | **Desenvolvimento concluído até 26/11/2026.** |
| Validação e testes | Executar testes, identificar falhas, realizar correções e validar os requisitos. | Aplicação validada até 30/11/2026. |
| Entrega final | Conferir o repositório, a documentação e a versão publicada. | **Entrega do projeto em 30/11/2026.** |

## 5. Estratégia de testes e validação

Após a conclusão do desenvolvimento, o grupo concentrará seus esforços na verificação da qualidade da aplicação.

Serão realizados:

- Testes de cadastro, consulta, edição e exclusão de pets.
- Testes de cadastro e gerenciamento de responsáveis e atendimentos.
- Testes de pesquisas, filtros e relatórios.
- Testes dos endpoints da API REST.
- Testes da integração com a Dog CEO API, incluindo tratamento de indisponibilidade.
- Testes de validação de formulários e dados inválidos.
- Verificação dos relacionamentos e da persistência no banco de dados.
- Testes de permissões e acesso às operações protegidas.
- Testes de regressão após as correções.
- Verificação da interface em diferentes tamanhos de tela.

O período de **27/11/2026 a 30/11/2026** será reservado para testes, correções e validação final. Não deverão ser iniciadas novas funcionalidades nesse período, salvo ajustes indispensáveis para corrigir problemas identificados.

## 6. Riscos e estratégias de prevenção

| Risco | Estratégia |
|---|---|
| Atraso no desenvolvimento | Acompanhar o backlog e priorizar as funcionalidades obrigatórias. |
| Dificuldade na integração dos componentes | Definir contratos e responsabilidades antes da implementação e integrar gradualmente. |
| Indisponibilidade da Dog CEO API | Tratar erros de comunicação e permitir o preenchimento manual da raça. |
| Problemas no banco de dados | Definir os relacionamentos antecipadamente e testar as migrações. |
| Falta de participação dos integrantes | Distribuir tarefas identificáveis e acompanhar os commits de cada pessoa. |
| Erros próximos da entrega | Reservar o período final para testes, correções e validação, evitando novas funcionalidades. |

## 7. Critérios de conclusão

O desenvolvimento será considerado concluído quando:

- [ ] Os CRUDs previstos estiverem implementados.
- [ ] As pesquisas e os filtros estiverem funcionando.
- [ ] Os atendimentos e seus relacionamentos estiverem implementados.
- [ ] O relatório com dados consolidados estiver disponível.
- [ ] A API REST própria estiver implementada.
- [ ] A integração com a Dog CEO API estiver funcionando, com tratamento de indisponibilidade.
- [ ] A interface estiver finalizada e adaptada a diferentes tamanhos de tela.
- [ ] As validações e os controles de acesso previstos estiverem implementados.
- [ ] A aplicação estiver publicada em ambiente acessível.
- [ ] O README e os documentos técnicos estiverem atualizados.

A validação final será concluída após a execução dos testes, a correção dos problemas encontrados e a conferência dos requisitos obrigatórios.

## 8. Estratégia de execução

O desenvolvimento será realizado de forma incremental, com tarefas distribuídas entre os quatro integrantes e acompanhamento pelo GitHub.

Cada integrante deverá manter suas alterações versionadas, registrar o andamento das atividades e comunicar impedimentos ao grupo. Os componentes serão integrados progressivamente para reduzir o risco de incompatibilidades no final do projeto.

O grupo adotará os seguintes marcos:

- **26/11/2026:** prazo final para conclusão do desenvolvimento.
- **27/11/2026 a 30/11/2026:** período destinado à validação, aos testes e às correções.
- **30/11/2026:** entrega final do projeto.
