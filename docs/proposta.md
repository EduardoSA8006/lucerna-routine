# Proposta do lucerna-routine

O `lucerna-routine` é um gerenciador de rotina em Rust. Funciona sozinho, com uma TUI, e ganha um painel no Lucerna.

Segue a estrutura de apps do [ecossistema](https://github.com/EduardoSA8006/lucerna-sdk/blob/main/docs/ecossistema.md): núcleo, TUI, provedor e painel em QML.

## Painel e TUI

O painel serve para olhar e agir rápido. O trabalho completo fica na TUI.

**No painel:**

- o agora: o que está acontecendo, o que vem a seguir e quanto falta;
- as tarefas de hoje, marcadas com um clique;
- os hábitos do dia, com anel de progresso;
- o botão "iniciar foco", um timer pomodoro que aparece na barra.

**Lembretes:** pelas notificações do shell.

**Só na TUI:**

- planejar a semana;
- rotinas recorrentes;
- histórico e estatísticas.

## Em aberto

- O que é "rotina" para o usuário: tarefas, hábitos, agenda, lembretes ou uma mistura.
- O armazenamento.
- A sincronização.
