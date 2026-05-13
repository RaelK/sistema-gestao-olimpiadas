# 🏅 Sistema de Gestão das Olimpíadas (SGO)

Projeto desenvolvido para a disciplina **Projeto de Software** do curso de **Engenharia de Software** da **PUC Minas**, sob orientação do professor **João Paulo Carneiro Aramuni**.

---

## 📑 Sumário

- [Descrição do Sistema](#-descrição-do-sistema)
- [Regras de Negócio](#-regras-de-negócio)
- [Histórias de Usuário](#-histórias-de-usuário)
- [Diagramas UML](#-diagramas-uml)
  - [Diagrama de Casos de Uso](#diagrama-de-casos-de-uso)
  - [Diagrama de Classes](#diagrama-de-classes)
  - [Diagrama de Pacotes](#diagrama-de-pacotes)
  - [Diagrama de Componentes](#diagrama-de-componentes)
  - [Diagrama de Implantação](#diagrama-de-implantação)
- [Estrutura do Repositório](#-estrutura-do-repositório)
- [Tecnologias e Ferramentas](#-tecnologias-e-ferramentas)
- [Como Gerar os Diagramas Localmente](#-como-gerar-os-diagramas-localmente)

---

## 📌 Descrição do Sistema

Com a chegada das Olimpíadas, um novo sistema de gestão é necessário para coordenar os diferentes aspectos do evento. O **Sistema de Gestão das Olimpíadas (SGO)** permite o gerenciamento de competições, inscrições de atletas, alocação de locais para as provas e controle de resultados, além de gerar relatórios de medalhas por país.

---

## 📋 Regras de Negócio

1. **Cadastro de competições:** o sistema deve permitir o cadastro de competições, que incluem o nome da modalidade, data, horário, local e lista de atletas inscritos.
2. **Inscrição de atletas:** atletas de diferentes países devem se inscrever em competições específicas. Cada atleta pode participar de várias competições, mas só pode representar um país em cada modalidade.
3. **Alocação de locais:** os locais para as competições devem ser alocados de forma a evitar conflitos de horário. Um local só pode abrigar uma competição por vez.
4. **Controle de resultados:** após a realização das competições, os resultados devem ser registrados, determinando o atleta vencedor e os classificados em segundo e terceiro lugares.
5. **Relatórios de medalhas:** o sistema deve gerar relatórios de medalhas, mostrando o desempenho de cada país com base nas medalhas de ouro, prata e bronze conquistadas.

---

## 👥 Histórias de Usuário

### US01 — Cadastro de Competição
**Como** administrador do sistema,
**quero** cadastrar uma nova competição informando modalidade, data, horário, local e lista de atletas,
**para que** o evento seja oficialmente registrado e disponibilizado no calendário olímpico.

**Critérios de aceitação:**
- O sistema deve exigir nome da modalidade, data, horário e local.
- O sistema não deve permitir o cadastro de competições com data/horário no passado.
- A competição deve ficar com status `AGENDADA` após o cadastro.

---

### US02 — Edição e Cancelamento de Competição
**Como** administrador do sistema,
**quero** editar ou cancelar uma competição já cadastrada,
**para que** eu possa ajustar informações em caso de mudanças ou imprevistos.

**Critérios de aceitação:**
- O sistema deve permitir editar dados de competições com status `AGENDADA`.
- Competições canceladas devem ter status `CANCELADA` e notificar atletas inscritos.

---

### US03 — Inscrição de Atleta em Competição
**Como** atleta,
**quero** me inscrever em uma competição da minha modalidade,
**para que** eu possa participar dos jogos olímpicos representando meu país.

**Critérios de aceitação:**
- O atleta só pode representar **um país** em cada modalidade.
- O atleta pode se inscrever em **várias** competições de modalidades diferentes.
- O sistema deve validar a inscrição antes de confirmá-la.

---

### US04 — Cadastro de Atletas e Países
**Como** administrador do sistema,
**quero** cadastrar atletas e seus respectivos países,
**para que** apenas atletas oficialmente registrados possam se inscrever nas competições.

**Critérios de aceitação:**
- Cada atleta deve estar vinculado a exatamente um país por modalidade.
- O sistema deve impedir cadastros duplicados (mesmo documento de identificação).

---

### US05 — Alocação de Locais para Competições
**Como** organizador do evento,
**quero** alocar um local para cada competição evitando conflitos de horário,
**para que** não haja sobreposição de provas no mesmo espaço físico.

**Critérios de aceitação:**
- Um local só pode abrigar **uma** competição por vez.
- O sistema deve detectar e impedir conflitos de horário automaticamente.
- O sistema deve sugerir locais alternativos disponíveis quando houver conflito.

---

### US06 — Cadastro de Locais
**Como** administrador do sistema,
**quero** cadastrar os locais disponíveis (estádios, ginásios, arenas),
**para que** eles possam ser alocados para as competições.

**Critérios de aceitação:**
- Cada local deve conter nome, endereço e capacidade.
- O sistema deve manter histórico de competições já realizadas em cada local.

---

### US07 — Registro de Resultados
**Como** juiz da competição,
**quero** registrar o resultado de uma competição finalizada,
**para que** os classificados em 1º, 2º e 3º lugares sejam oficialmente reconhecidos.

**Critérios de aceitação:**
- O sistema deve permitir registrar apenas resultados de competições com status `EM_ANDAMENTO` ou `FINALIZADA`.
- O sistema deve atribuir automaticamente as medalhas de **ouro**, **prata** e **bronze**.
- Os resultados ficam imutáveis após a confirmação.

---

### US08 — Consulta de Competições
**Como** atleta ou público em geral,
**quero** consultar as competições programadas e seus locais,
**para que** eu possa acompanhar os jogos e me planejar.

**Critérios de aceitação:**
- A consulta deve permitir filtros por modalidade, data e país.
- O sistema deve exibir status atual (agendada, em andamento, finalizada).

---

### US09 — Relatório de Medalhas por País
**Como** organizador do evento,
**quero** gerar um relatório consolidado das medalhas conquistadas por cada país,
**para que** o ranking olímpico seja divulgado oficialmente.

**Critérios de aceitação:**
- O relatório deve mostrar quantidade de medalhas de ouro, prata e bronze por país.
- O ranking deve seguir a ordem: ouro > prata > bronze.
- O relatório deve ser exportável em PDF.

---

### US10 — Consulta de Ranking Geral
**Como** público em geral,
**quero** consultar o ranking de medalhas em tempo real,
**para que** eu possa acompanhar o desempenho do meu país.

**Critérios de aceitação:**
- O ranking deve ser atualizado automaticamente a cada novo resultado registrado.
- O sistema deve permitir filtrar por modalidade ou ver o ranking geral.

---

### US11 — Autenticação de Usuários
**Como** usuário do sistema (administrador, organizador, juiz ou atleta),
**quero** autenticar-me com login e senha,
**para que** apenas usuários autorizados realizem ações restritas no sistema.

**Critérios de aceitação:**
- O sistema deve aplicar perfis distintos com permissões específicas.
- Tentativas inválidas devem ser registradas para auditoria.

---

## 🧩 Diagramas UML

### Diagrama de Casos de Uso

Modela os atores e as principais interações com o sistema, contemplando os casos de uso de **Cadastrar Competição**, **Inscrever Atleta**, **Alocar Local**, **Registrar Resultado** e **Gerar Relatório de Medalhas**.

<img width="900px" src="imagens/diagrama-de-caso-de-uso.png" alt="Diagrama de Casos de Uso"/>

📄 Código-fonte: [`codigos/diagrama-de-caso-de-uso.puml`](codigos/diagrama-de-caso-de-uso.puml)

---

### Diagrama de Classes

Representa a estrutura estática do sistema com as principais classes do domínio: `Competicao`, `Atleta`, `Local`, `Resultado`, `Pais`, `Modalidade`, `Inscricao`, `Medalha`, `RelatorioMedalhas` e `Usuario`, além dos enums `TipoMedalha` e `StatusCompeticao`.

<img width="900px" src="imagens/diagrama-de-classes.png" alt="Diagrama de Classes"/>

📄 Código-fonte: [`codigos/diagrama-de-classes.puml`](codigos/diagrama-de-classes.puml)

---

### Diagrama de Pacotes

Organiza o sistema em camadas (arquitetura em camadas / *layered architecture*) separando responsabilidades em **presentation**, **business**, **domain**, **persistence**, **security** e **utils**.

<img width="900px" src="imagens/diagrama-de-pacotes.png" alt="Diagrama de Pacotes"/>

📄 Código-fonte: [`codigos/diagrama-de-pacotes.puml`](codigos/diagrama-de-pacotes.puml)

---

### Diagrama de Componentes

Mostra os principais componentes do sistema e como eles se comunicam: **Interface de Usuário**, **API Gateway**, **Módulo de Competições**, **Módulo de Inscrições**, **Módulo de Alocação**, **Módulo de Resultados**, **Módulo de Relatórios**, **Módulo de Autenticação** e **Módulo de Notificações**.

<img width="900px" src="imagens/diagrama-de-componentes.png" alt="Diagrama de Componentes"/>

📄 Código-fonte: [`codigos/diagrama-de-componentes.puml`](codigos/diagrama-de-componentes.puml)

---

### Diagrama de Implantação

Ilustra a arquitetura física do sistema, incluindo **dispositivos dos usuários** (navegador e app mobile), **servidor web**, **servidor de aplicação**, **servidor de banco de dados (PostgreSQL/MySQL)**, **servidor de cache (Redis)**, **servidor de arquivos** e **serviços externos** (e-mail/SMTP).

<img width="900px" src="imagens/diagrama-de-implantacao.png" alt="Diagrama de Implantação"/>

📄 Código-fonte: [`codigos/diagrama-de-implantacao.puml`](codigos/diagrama-de-implantacao.puml)

---

## 📂 Estrutura do Repositório

```
sistema-gestao-olimpiadas/
├── README.md
├── imagens/
│   ├── diagrama-de-caso-de-uso.png
│   ├── diagrama-de-classes.png
│   ├── diagrama-de-pacotes.png
│   ├── diagrama-de-componentes.png
│   └── diagrama-de-implantacao.png
└── codigos/
    ├── diagrama-de-caso-de-uso.puml
    ├── diagrama-de-classes.puml
    ├── diagrama-de-pacotes.puml
    ├── diagrama-de-componentes.puml
    └── diagrama-de-implantacao.puml
```

---

## 🛠 Tecnologias e Ferramentas

- **[PlantUML](https://plantuml.com/)** — Linguagem textual para descrição de diagramas UML.
- **[PlantUML Guide](https://plantuml.com/guide)** — Documentação oficial.
- **[Projeto PlantUML API](https://github.com/joaopauloaramuni/projeto-de-software/tree/main/PROJETOS/Python/Projeto%20PlantUML%20API)** — Referência do professor para geração de diagramas via API.

---

## 🚀 Como Gerar os Diagramas Localmente

### Opção 1 — Servidor PlantUML Online

Acesse [https://www.plantuml.com/plantuml/uml/](https://www.plantuml.com/plantuml/uml/) e cole o conteúdo de qualquer arquivo `.puml` da pasta `codigos/`.

### Opção 2 — PlantUML via linha de comando

Pré-requisitos: **Java 8+** e o JAR do PlantUML.

```bash
# Gerar PNG de um diagrama específico
java -jar plantuml.jar codigos/diagrama-de-classes.puml -o ../imagens

# Gerar todos os diagramas
java -jar plantuml.jar codigos/*.puml -o ../imagens
```

### Opção 3 — Extensão no VSCode

Instale a extensão **PlantUML** e use `Alt+D` para visualizar.

---

## 👨‍🏫 Disciplina

- **Curso:** Engenharia de Software
- **Disciplina:** Projeto de Software
- **Professor:** João Paulo Carneiro Aramuni
- **Instituição:** PUC Minas
- **Período:** 4º
