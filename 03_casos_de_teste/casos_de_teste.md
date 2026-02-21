# Documentação de Casos de Teste - SRL

Este documento detalha os cenários de teste para a API do Sistema de Reservas de Laboratório.

---

## Módulo 1: Autenticação

**CT01 – Registro de novo usuário com sucesso**
- **Requisito:** RF01
- **Descrição:** Validar o cadastro de um novo usuário com perfil USER.
- **Pré-condição:** E-mail não deve estar cadastrado.
- **Entrada:** Nome: "João Silva", Email: "joao@email.com", Senha: "Senha123", Perfil: "USER".
- **Resultado Esperado:** Status 201 Created e usuário persistido.

**CT02 – Registro com e-mail duplicado**
- **Tipo:** NEGATIVO (RN01)
- **Requisito:** RF01
- **Descrição:** Validar que o sistema impede e-mails repetidos.
- **Pré-condição:** Usuário "joao@email.com" já cadastrado.
- **Entrada:** Email: "joao@email.com".
- **Resultado Esperado:** Status 409 Conflict ou 400 Bad Request.

**CT03 – Registro com senha inválida**
- **Tipo:** NEGATIVO (RN02)
- **Requisito:** RF01
- **Descrição:** Validar restrição de senha menor que 8 caracteres.
- **Pré-condição:** Nenhuma.
- **Entrada:** Senha: "123".
- **Resultado Esperado:** Status 400 Bad Request.

**CT04 – Login e geração de Token**
- **Requisito:** RF02, RF03
- **Descrição:** Validar se o sistema retorna o token após login válido.
- **Pré-condição:** Usuário cadastrado.
- **Entrada:** Email: "joao@email.com", Senha: "Senha123".
- **Resultado Esperado:** Status 200 OK e retorno do Token Bearer.

---

## Módulo 2: Salas

**CT05 – Cadastro de sala por ADMIN**
- **Requisito:** RF04
- **Descrição:** Validar criação de sala por perfil administrador.
- **Pré-condição:** Token de ADMIN válido.
- **Entrada:** Nome: "Lab 01", Capacidade: 30, Recursos: ["Projetor"].
- **Resultado Esperado:** Status 201 Created.

**CT06 – Tentativa de cadastro de sala por USER**
- **Tipo:** NEGATIVO (RBAC)
- **Requisito:** Seção 2 - Permissões
- **Descrição:** Validar que perfil USER não possui permissão de escrita em salas.
- **Pré-condição:** Token de USER válido.
- **Entrada:** POST /rooms.
- **Resultado Esperado:** Status 403 Forbidden.

**CT07 – Listagem de salas**
- **Requisito:** RF05
- **Descrição:** Validar se a lista de salas é retornada para usuários logados.
- **Pré-condição:** Token válido.
- **Entrada:** GET /rooms.
- **Resultado Esperado:** Status 200 OK e array de objetos.

---

## Módulo 3: Reservas

**CT08 – Criação de reserva válida**
- **Requisito:** RF06, RF08
- **Descrição:** Validar reserva em horário disponível.
- **Pré-condição:** Token válido, Sala ID 1 existente.
- **Entrada:** Data: "2026-03-10", Início: "09:00", Fim: "11:00".
- **Resultado Esperado:** Status 201 Created e status "CONFIRMED".

**CT09 – Reserva fora do horário permitido**
- **Tipo:** NEGATIVO (RN07)
- **Requisito:** RF06
- **Descrição:** Validar bloqueio de reserva fora da janela 08h-22h.
- **Pré-condição:** Token válido.
- **Entrada:** Início: "22:30", Fim: "23:30".
- **Resultado Esperado:** Status 400 Bad Request.

**CT10 – Conflito de horário na mesma sala**
- **Tipo:** NEGATIVO (RN08)
- **Requisito:** RF06
- **Descrição:** Validar impedimento de reservas sobrepostas.
- **Pré-condição:** Reserva existente para o horário solicitado.
- **Entrada:** Mesma Data/Sala/Horário do CT08.
- **Resultado Esperado:** Status 409 Conflict.

**CT11 – Início maior que término**
- **Tipo:** NEGATIVO (RN06)
- **Requisito:** RF06
- **Descrição:** Validar erro lógico de horário.
- **Pré-condição:** Token válido.
- **Entrada:** Início: "10:00", Fim: "08:00".
- **Resultado Esperado:** Status 400 Bad Request.

**CT12 – Visualizar próprias reservas**
- **Requisito:** RF07
- **Descrição:** Validar filtro de reservas por usuário logado.
- **Pré-condição:** Usuário possui reservas.
- **Entrada:** GET /bookings/my.
- **Resultado Esperado:** Status 200 OK.

---

## Módulo 4: Incidentes

**CT13 – Abertura de incidente**
- **Requisito:** RF09, RF11
- **Descrição:** Registrar problema em sala com status inicial OPEN.
- **Pré-condição:** Token válido.
- **Entrada:** Sala_ID: 1, Descrição: "Cabo HDMI com mau contato".
- **Resultado Esperado:** Status 201 Created e Status: OPEN.

**CT14 – Descrição curta de incidente**
- **Tipo:** NEGATIVO (RN10)
- **Requisito:** RF09
- **Descrição:** Validar mínimo de 10 caracteres.
- **Pré-condição:** Token válido.
- **Entrada:** Descrição: "Quebrado".
- **Resultado Esperado:** Status 400 Bad Request.

**CT15 – Finalização de incidente por ADMIN**
- **Requisito:** RF10, RF12
- **Descrição:** Validar fechamento de incidente por perfil ADMIN.
- **Pré-condição:** Incidente OPEN e Token ADMIN.
- **Entrada:** PATCH /incidents/{id}/close.
- **Resultado Esperado:** Status 200 OK e Status: CLOSED.

**CT16 – Tentativa de finalizar incidente por USER**
- **Tipo:** NEGATIVO (RN11)
- **Requisito:** RF10
- **Descrição:** Validar que apenas ADMIN pode fechar incidentes.
- **Pré-condição:** Token USER.
- **Entrada:** PATCH /incidents/{id}/close.
- **Resultado Esperado:** Status 403 Forbidden.
