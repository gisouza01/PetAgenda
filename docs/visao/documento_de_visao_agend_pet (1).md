# Documento de Visão — Agend Pet

## 1\. Identidade do Projeto

* **Nome do Projeto:** Agend Pet  
* **Tipo de Aplicação:** Aplicação Web para Gerenciamento de Serviços e Agendamentos de Pet Shop  
* **Proposta Central:** Permitir que clientes cadastrem seus pets, consultem os serviços disponíveis e realizem agendamentos online de forma autônoma, enquanto funcionários administram o catálogo de serviços, a agenda de horários e a evolução dos atendimentos.  
* **Tecnologias Base:**  
  * **Linguagem & Framework:** Python com Django  
  * **Banco de Dados:** Banco de dados relacional (ex: PostgreSQL / SQLite em desenvolvimento)  
  * **API REST Própria:** Django REST Framework  
  * **API Externa:** *The Dog API* (consulta de informações sobre raças)  
    

---

## 2\. Problema e Oportunidade

O **Agend Pet** foi concebido para resolver a desorganização e a ineficiência causadas pela gestão manual ou descentralizada de agendamentos em pet shops.

### Benefícios para o Cliente

* Visualização clara e transparente dos serviços oferecidos e seus valores.  
* Cadastro e centralização do histórico e perfil de seus pets.  
* Autonomia para escolha de serviços, datas e horários disponíveis.  
* Acompanhamento em tempo real do status de atendimento do pet.

### Benefícios para o Estabelecimento

* Centralização e organização automatizada da agenda de atendimentos.  
* Controle eficiente sobre o catálogo e disponibilidade de serviços.  
* Eliminação de conflitos de horários (agendamentos duplicados).  
* Acesso a dados consolidados e relatórios operacionais para tomada de decisão.

---

## 3\. Perfil dos Usuários

O sistema atenderá a dois perfis principais de usuários:

### 3.1. Cliente

Usuário final do pet shop que busca agendar serviços para seus animais de estimação.

* **Permissões e Ações:**  
  * Criar conta e autenticar-se na plataforma.  
  * Cadastrar, visualizar e gerenciar seus pets.  
  * Consultar informações detalhadas de raças de cães (via integração externa).  
  * Consultar lista e detalhes dos serviços prestados.  
  * Agendar atendimentos escolhendo pet, serviço, data e horário.  
  * Visualizar histórico e status dos seus agendamentos.  
  * Cancelar agendamentos próprios (respeitando as regras de negócio).

### 3.2. Funcionário

Usuário administrativo responsável pela operação e gestão do pet shop.

* **Permissões e Ações:**  
  * Autenticar-se na área administrativa do sistema.  
  * Cadastrar, alterar, consultar e desativar serviços.  
  * Visualizar a agenda completa de atendimentos do estabelecimento.  
  * Atualizar o status dos agendamentos (ex: Confirmado, Em andamento, Concluído, Cancelado).  
  * Gerar e consultar relatórios operacionais com dados consolidados.

---

## 4\. Gerenciamento e Cadastro de Pets

O cliente poderá vincular múltiplos pets à sua conta.

### Dados do Pet

* Nome  
* Espécie (Cachorro ou Gato)  
* Raça  
* Sexo (Macho / Fêmea)  
* Data de nascimento ou idade estimada  
* Observações gerais (restrições, comportamento, alergias)  
* Vínculo com o Cliente responsável

---

## 5\. Integração com a *The Dog API*

A integração com a *The Dog API* tem utilidade funcional direta no fluxo do sistema, enriquecendo a experiência do cliente no cadastro e consulta de cães.

### Funcionamento

1. Durante o cadastro ou consulta de um pet da espécie **Cachorro**, o cliente informa/seleciona a raça.  
2. O **Agend Pet** efetua uma requisição à *The Dog API*.  
3. O sistema exibe informações relevantes da raça, tais como:  
   * Nome oficial e temperamento/características;  
   * Expectativa de vida e porte;  
   * Imagem ilustrativa da raça (quando disponível).

### Tratamento de Indisponibilidade (Resiliência)

Caso a *The Dog API* esteja fora do ar, apresente *timeout* ou retorne resposta inválida:

* O sistema captura a exceção e impede a falha da aplicação.  
* É exibida uma notificação amigável informando que as informações adicionais da raça não puderam ser carregadas.  
* O cadastro básico do pet **é concluído normalmente**, garantindo que a falha do serviço externo não bloqueie a operação do sistema.

---

## 6\. Catálogo de Serviços

Serviços iniciais previstos na plataforma:

| Serviço | Descrição |
| :---- | :---- |
| **Banho** | Higienização completa do pet com produtos específicos. |
| **Tosa** | Corte e aparo estilizado dos pelos. |
| **Banho e Tosa** | Pacote integrado de higienização e corte de pelos. |
| **Corte de Unhas** | Corte, aparo e cuidados com as unhas. |
| **Higienização** | Limpeza de ouvidos, dentes e cuidados básicos adicionais. |

### Atributos do Serviço

* Nome do Serviço  
* Descrição  
* Preço (R\$)  
* Duração estimada (em minutos/horas)  
* Situação / Disponibilidade (Ativo/Inativo)

---

## 7\. Regras e Fluxo de Agendamento

### Fluxo do Cliente

`Selecionar Pet` \$\\rightarrow\$ `Selecionar Serviço` \$\\rightarrow\$ `Escolher Data` \$\\rightarrow\$ `Escolher Horário` \$\\rightarrow\$ `Confirmar Agendamento`

### Regra de Disponibilidade

* O sistema realiza validação em tempo real da agenda.  
* **Bloqueio de Conflito:** Não é permitido registrar dois atendimentos simultâneos no mesmo horário.  
* Horários já ocupados ficam indisponíveis para seleção no painel do cliente.

---

## 8\. Ciclo de Vida do Agendamento (Status)

Um agendamento transita entre cinco status principais:

1. **Pendente:** Criado pelo cliente; aguarda confirmação inicial da equipe.  
2. **Confirmado:** Aprovado pelo funcionário e agendado na grade.  
3. **Em andamento:** Pet em atendimento no estabelecimento.  
4. **Concluído:** Serviço finalizado e pet pronto para entrega.  
5. **Cancelado:** Atendimento descontinuado.

\[ Fluxo Principal \]

Pendente ──\> Confirmado ──\> Em Andamento ──\> Concluído

\[ Fluxos Alternativos \]

Pendente   ──\> Cancelado

Confirmado ──\> Cancelado

---

## 9\. Politica de Cancelamento e Alteração

### Cancelamento

* **Cliente:** Pode cancelar o agendamento apenas enquanto o status for **Pendente** ou **Confirmado**.  
* **Bloqueio:** Após o início do serviço (**Em andamento** ou **Concluído**), o cliente fica impossibilitado de cancelar.  
* **Funcionário:** Pode cancelar o agendamento em qualquer etapa administrativa justificada.

### Alteração / Reagendamento

* Não haverá edição direta de agendamentos existentes no MVP.  
* Para alterar data, horário, serviço ou pet, o cliente deve **cancelar o agendamento atual** e **realizar um novo agendamento**.

---

## 10\. Agenda do Estabelecimento

A interface do funcionário apresenta a visão global da agenda do pet shop:

* Filtros por data e visualização diária/semanal.  
* Detalhamento de cada horário: Data, Horário, Cliente, Pet, Serviço e Status atual.  
* Ações rápidas para alteração de status do atendimento.

---

## 11\. Relatório de Agendamentos

Módulo destinado ao perfil de funcionário para geração de estatísticas operacionais consolidadas.

* **Filtros Disponíveis:**  
  * Período (Data Inicial e Data Final)  
  * Serviço  
  * Status do Agendamento  
* **Indicadores Apresentados:**  
  * Quantidade total de agendamentos no período.  
  * Distribuição quantitativa por status (Pendentes, Confirmados, Concluídos, Cancelados).  
  * Volume de atendimentos por tipo de serviço.  
  * Taxa/quantidade total de cancelamentos.

---

## 12\. Arquitetura da API REST Própria

O sistema disponibilizará endpoints RESTful para consumo interno e/ou integrações futuras:

* `/api/pets/`: CRUD para gerenciamento dos animais dos clientes.  
* `/api/servicos/`: Consulta e gestão do catálogo de serviços.  
* `/api/agendamentos/`: Criação, listagem, atualização de status e cancelamento de agendamentos.

*Observação: Contrato completo de API (métodos HTTP, payloads JSON, query params, cabeçalhos de autenticação JWT/Session e códigos de status HTTP) será documentado em especificação OpenAPI/Swagger.*

---

## 13\. Modelo Conceitual do Banco de Dados

Representação em alto nível das entidades do sistema:

USUARIO (Autenticação Base)

   │

   └── CLIENTE (Perfil estendido)

          │

          └── PET (Animais do cliente)

          

SERVICO (Catálogo do pet shop)

   │

   └── AGENDAMENTO

          │

          ├── Relaciona: CLIENTE

          ├── Relaciona: PET

          └── Relaciona: SERVICO

---

## 14\. Escopo do Projeto

### Dentro do Escopo (In Scope)

* Autenticação de usuários com perfis distintos (Cliente e Funcionário).  
* Gerenciamento de cadastro de Clientes e Pets.  
* Integração resiliente com *The Dog API* para informações de cães.  
* Gerenciamento de catálogo de serviços (CRUD por Funcionários).  
* Agendamento online de serviços com verificação automática de disponibilidade de horário.  
* Painel de controle da agenda e alteração de status por Funcionários.  
* Relatório consolidado com filtros e métricas operacionais.  
* API REST própria para os principais recursos.  
* Interface web responsiva e amigável.

### Fora do Escopo (Out of Scope \- Futuras Versões)

* Pagamento online e integração com gateways financeiros.  
* Emissão de nota fiscal eletrônica.  
* Aplicativos móveis nativos (Android/iOS).  
* Módulo de chat em tempo real entre cliente e funcionário.  
* Gestão de estoque de produtos do pet shop.  
* Marketplace de rações e acessórios.  
* Envio automatizado de mensagens via WhatsApp / SMS.  
* Sistema de transporte / busca e entrega de pets em domicílio.

---

## 15\. Regras de Negócio Consolidadas (RN)

* **RN01 — Autenticação:** Apenas usuários cadastrados e autenticados podem realizar agendamentos ou acessar áreas administrativas.  
* **RN02 — Associação de Pets:** Um cliente pode cadastrar e possuir múltiplos pets associados ao seu perfil.  
* **RN03 — Requisitos para Agendamento:** O agendamento exige obrigatoriamente a seleção de 1 Pet, 1 Serviço, Data e Horário válidos.  
* **RN04 — Exclusividade de Horário:** O sistema impede agendamentos simultâneos para o mesmo horário e serviço.  
* **RN05 — Controle de Status:** Todo agendamento deve conter obrigatoriamente um status válido (Pendente, Confirmado, Em andamento, Concluído ou Cancelado).  
* **RN06 — Restrição de Cancelamento:** O cliente não pode cancelar agendamentos com status "Em andamento" ou "Concluído".  
* **RN07 — Serviços Ativos:** Somente serviços marcados como "Disponíveis/Ativos" podem ser selecionados para novos agendamentos.  
* **RN08 — Privilégios Administrativos:** O gerenciamento do catálogo de serviços, alteração de status e consulta aos relatórios são de uso exclusivo do perfil Funcionário.  
* **RN09 — Enriquecimento por API Externa:** A *The Dog API* deve ser consultada para prover dados informativos das raças caninas no cadastro.  
* **RN10 — Tolerância a Falhas Externas:** Falhas de comunicação ou indisponibilidade da *The Dog API* não podem interromper o processo de cadastro básico do pet.

---

## 16\. Fluxo Geral da Aplicação

                           AGEND PET

                               │

               ┌───────────────┴───────────────┐

               │                               │

            CLIENTE                       FUNCIONÁRIO

               │                               │

        Cadastro/Login                  Cadastro/Login

               │                               │

          Cadastra Pet                 Gerencia Serviços

               │                               │

   (Se Cão ──\> The Dog API)            Consulta Agenda

               │                               │

        Consulta Serviços               Atualiza Status

               │                               │

        Escolhe Horário                Gera Relatórios

               │

        Confirma Agendamento

               │

        Acompanha Status