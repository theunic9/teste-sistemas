# Plano de Teste – Sistema de Reservas de Laboratório (SRL)

## 1. Escopo
Este plano abrange a validação funcional e de segurança da **API REST** do Sistema de Reservas de Laboratório (SRL).
* **Módulos Incluídos:** Autenticação (Login/Registro), Gestão de Salas, Sistema de Reservas e Registro de Incidentes.
* **Tipos de Teste:** Testes de Caixa-Preta, Testes de Regressão e Validação de Regras de Negócio (RN).
* **Fora de Escopo:** Testes de Interface de Usuário (UI), Testes de Performance e Pentest.

## 2. Objetivo
Garantir que todos os endpoints da API SRL funcionem conforme os Requisitos Funcionais (RF), respeitando as Regras de Negócio (RN) e as permissões de acesso (ADMIN/USER).

## 3. Estratégia de Teste
* **Nível de Teste:** Integração e Sistema.
* **Técnica:** Particionamento por Equivalência e Análise de Valor Limite.
* **Ferramentas:** Postman (Execução), Newman (Automação CLI), Git (Versionamento).

## 4. Ambiente
* **Ambiente:** Localhost / Staging.
* **Dados de Teste:** Massa de dados contendo usuários de ambos os perfis (ADMIN/USER) e salas previamente cadastradas.

## 5. Critérios de Entrada
* Documento de Requisitos (v1.0) revisado.
* API disponível para consumo.

## 6. Critérios de Saída
* 100% dos testes planejados executados.
* Zero bugs de severidade "Crítica" ou "Alta" em aberto.

## 7. Responsáveis
| Papel | Responsabilidade |
| :--- | :--- |
| Analista de QA | Planejamento, escrita e execução dos testes. |
| Desenvolvedor | Correção de bugs. |
