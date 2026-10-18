# Proposta do lucerna-routine

O `lucerna-routine` é um gerenciador de rotina em Rust. Funciona sozinho, com uma TUI, e ganha um painel no Lucerna.

Segue a estrutura de apps do [ecossistema](https://github.com/EduardoSA8006/lucerna-sdk/blob/main/docs/ecossistema.md): núcleo, serviço, TUI e painel em QML.

## Painel e TUI

O painel serve para olhar e agir rápido. O trabalho completo fica na TUI.

**No painel:**

- o agora: o que está acontecendo, o que vem a seguir e quanto falta;
- as tarefas de hoje, marcadas com um clique;
- os hábitos do dia, com anel de progresso;
- o botão "iniciar foco", um timer pomodoro que aparece na barra.

**Lembretes:** pelas notificações do shell. Funcionam pelo timer do systemd do usuário, sem o serviço ficar rodando: o serviço registra o timer para o próximo horário, o timer o sobe, ele avisa e volta a sair. O desenho está em "Serviço sob demanda" no [ecossistema](https://github.com/EduardoSA8006/lucerna-sdk/blob/main/docs/ecossistema.md).

**Só na TUI:**

- planejar a semana;
- rotinas recorrentes;
- histórico e estatísticas.

## Armazenamento

Os dados ficam só neste computador, por enquanto. As pastas seguem as regras de "Pastas e dados" no [ecossistema](https://github.com/EduardoSA8006/lucerna-sdk/blob/main/docs/ecossistema.md).

As tarefas, os hábitos e o histórico ficam num banco SQLite interno, em `~/.local/share/lucerna/routine/`. Os dados da rotina são mais estruturados que as notas, então um banco serve melhor que arquivos soltos.

## Futuro

- A sincronização entre aparelhos.

## Em aberto

- O que é "rotina" para o usuário: tarefas, hábitos, agenda, lembretes ou uma mistura.
