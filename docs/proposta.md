# Proposta do lucerna-routine

O `lucerna-routine` é um gerenciador de rotina em Rust. Funciona sozinho, com uma TUI, e ganha um painel no Lucerna.

Segue a estrutura de apps do [ecossistema](https://github.com/EduardoSA8006/lucerna-sdk/blob/main/docs/ecossistema.md): núcleo, serviço, TUI e painel em QML.

## O que é rotina

A rotina junta tarefas, hábitos e foco num app só. A inspiração vem de:

- o TickTick, pela base: tarefas, hábitos e foco juntos;
- o Structured, pela linha do tempo do dia;
- o Todoist, pela captura rápida;
- o Things 3, pela separação em Hoje, Próximos e Algum dia;
- o calcurse e o Taskwarrior, para a TUI.

### Captura rápida

É um formulário compacto, direto, sem configuração:

- um campo de título;
- chips de data (Hoje, Amanhã e Data, com seletor) e um campo de hora opcional;
- dropdowns de prioridade e de repetição;
- as etiquetas como caixas de seleção, com a opção de criar uma nova;
- o botão Adicionar.

Tudo vem com valor padrão (sem data, prioridade normal, sem repetição). Digitar o título e apertar Enter já cria a tarefa.

Há também um atalho de texto, como extra. No título, `amanhã 19h #estudo !alta` preenche os controles. O app entende, em português, "hoje", "amanhã", "sexta", "dia 20", "às 19h", "toda segunda", `#etiqueta` e `!prioridade`. O que ele não entende fica no título, sem erro.

Na TUI é o mesmo formulário, navegado pelo teclado: Tab passa de campo e espaço marca as caixas.

### O dia como linha do tempo

Os blocos de horário do dia (trabalho, almoço, estudo) e as tarefas com hora formam a linha do tempo. É ela que alimenta o "agora e próximo" do painel.

### Tarefas

Ficam em Hoje, Próximos e Algum dia, inclusive as que se repetem.

### Hábitos

Têm meta por dia ou por semana e a sequência de dias seguidos.

### Foco

Serve para estudos e programação:

- tem dois modos: pomodoro (25 min de foco e 5 de pausa, ajustáveis) ou cronômetro livre;
- fica ligado a uma tarefa ou etiqueta, para o histórico mostrar quanto tempo foi para cada coisa;
- o timer aparece na barra do shell enquanto roda, e há um aviso no fim de cada etapa;
- durante o foco, o app liga sozinho o "não perturbe" do shell e desliga na pausa e no fim (pedido pelo SDK, como em "O que o SDK oferece" no [ecossistema](https://github.com/EduardoSA8006/lucerna-sdk/blob/main/docs/ecossistema.md));
- as estatísticas (por dia e por etiqueta) ficam na TUI, e o painel mostra só o total de hoje.

## Painel e TUI

O painel serve para olhar e agir rápido. O trabalho completo fica na TUI.

**No painel:**

- o agora: o que está acontecendo, o que vem a seguir e quanto falta, a partir da linha do tempo do dia;
- a captura rápida;
- as tarefas de hoje, marcadas com um clique;
- os hábitos do dia, com anel de progresso;
- o botão "iniciar foco", com o total de foco de hoje.

**Lembretes:** pelas notificações do shell. Funcionam pelo timer do systemd do usuário, sem o serviço ficar rodando: o serviço registra o timer para o próximo horário, o timer o sobe, ele avisa e volta a sair. O desenho está em "Serviço sob demanda" no [ecossistema](https://github.com/EduardoSA8006/lucerna-sdk/blob/main/docs/ecossistema.md).

**Na TUI:**

- tudo o que o painel faz, inclusive a captura rápida, com o mesmo formulário navegado pelo teclado;
- planejar a semana;
- tarefas em Hoje, Próximos e Algum dia, e o dia como linha do tempo;
- histórico e estatísticas do foco, por dia e por etiqueta.

## Armazenamento

Os dados ficam só neste computador, por enquanto. As pastas seguem as regras de "Pastas e dados" no [ecossistema](https://github.com/EduardoSA8006/lucerna-sdk/blob/main/docs/ecossistema.md).

As tarefas, os hábitos, os blocos do dia e o histórico do foco ficam num banco SQLite interno, em `~/.local/share/lucerna/routine/`. Os dados da rotina são mais estruturados que as notas, então um banco serve melhor que arquivos soltos.

## Futuro

- A sincronização entre aparelhos.

## Em aberto

- Onde se configuram os valores padrão do pomodoro (25 min de foco e 5 de pausa).
- Como os blocos de horário do dia são definidos: manualmente ou por um modelo de dia.
