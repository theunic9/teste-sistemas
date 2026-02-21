# Matriz de Rastreabilidade de Requisitos (RTM) - Sistema SRL

A Matriz de Rastreabilidade abaixo correlaciona os Requisitos Funcionais (RF) e Regras de Negócio (RN) aos seus respectivos Casos de Teste (CT), garantindo a cobertura total do sistema.

| Requisito / Regra | Descrição Técnica | Casos de Teste Associados |
| :--- | :--- | :--- |
| **RF01** | Registro de usuários (ADMIN/USER) | CT01, CT02, CT03 |
| **RF02 / RF03** | Login e retorno de Token JWT | CT04 |
| **RF04** | Cadastro de salas (Exclusivo ADMIN) | CT05, CT06 |
| **RF05** | Listagem de salas cadastradas | CT07 |
| **RF06** | Criação de reserva de sala | CT08, CT09, CT10, CT11 |
| **RF07** | Listar reservas do próprio usuário | CT12 |
| **RF08** | Status automático CONFIRMED em reservas | CT08 |
| **RF09** | Abertura de incidente vinculado a sala | CT13, CT14 |
| **RF10** | Finalização de incidente (Exclusivo ADMIN) | CT15, CT16 |
| **RF11 / RF12** | Fluxo de Status: OPEN -> CLOSED | CT13, CT15 |
| **RN01** | Unicidade de e-mail (Email único) | CT02 |
| **RN02** | Validação de Senha (8+ caracteres, Alfanumérica) | CT03 |
| **RN04** | Nome da sala não pode ser duplicado | CT05 |
| **RN05** | Capacidade da sala > 0 | CT05 |
| **RN06** | Início da reserva < Término | CT11 |
| **RN07** | Horário permitido (08:00 às 22:00) | CT09 |
| **RN08** | Bloqueio de conflito de horários | CT10 |
| **RN10** | Descrição do incidente (mín. 10 chars) | CT14 |
| **RN11** | Permissão de fechamento apenas para ADMIN | CT16 |
| **RN12** | Status deve estar OPEN para ser fechado | CT16 |

---
**Legenda:**
* **RF:** Requisito Funcional
* **RN:** Regra de Negócio
* **CT:** Caso de Teste
