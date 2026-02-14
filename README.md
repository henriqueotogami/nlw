# Proffy - Sua plataforma de estudos online

> Projeto desenvolvido durante a **Next Level Week #2** da [Rocketseat](https://rocketseat.com.br/), trilha Discovery. Plataforma de cadastro de professores para lecionar disciplinas regulares do ensino médio, onde alunos podem buscar aulas particulares por dia da semana e horários disponíveis.

<div align="center">

<img src="public/images/logo.svg" alt="Proffy" width="200">

<br>

<img src="https://img.shields.io/github/release-date/HenriqueMAP/nlw?style=flat" alt="Release Date">
<img src="https://img.shields.io/github/last-commit/HenriqueMAP/nlw?style=flat" alt="Last Commit">
<img src="https://img.shields.io/github/license/HenriqueMAP/nlw?style=flat" alt="License">

<br>

<img src="https://img.shields.io/github/forks/HenriqueMAP/nlw?style=flat" alt="Forks">
<img src="https://img.shields.io/github/stars/HenriqueMAP/nlw?style=flat" alt="Stars">
<img src="https://img.shields.io/github/issues/HenriqueMAP/nlw?style=flat" alt="Issues">

</div>

---

## 📋 Sobre o Projeto

O **Proffy** é uma aplicação web full-stack que conecta professores e alunos. Professores cadastram suas disponibilidades (matérias, horários e valores), e alunos buscam aulas particulares com base em filtros de disciplina, dia da semana e horário. O projeto foi desenvolvido entre **03/08/2020 e 05/08/2020** como parte do evento Next Level Week da Rocketseat.

## 📁 Estrutura do Projeto

```
nlw/
├── LICENSE
├── README.md
├── package.json
│
├── src/                      # Código-fonte principal
│   ├── server.js             # Servidor Express e rotas
│   ├── pages.js              # Controllers e lógica das páginas
│   │
│   ├── views/                # Templates Nunjucks (HTML)
│   │   ├── index.html        # Página inicial (Landing)
│   │   ├── study.html        # Busca de professores
│   │   └── give-classes.html # Cadastro de professores
│   │
│   ├── database/             # Camada de dados
│   │   ├── db.js             # Conexão e criação do banco SQLite
│   │   ├── createProffy.js   # Inserção de professores/aulas
│   │   ├── fake_data.js      # Dados de exemplo
│   │   └── test.js           # Testes de banco
│   │
│   └── utils/
│       └── format.js         # Formatação (matérias, dias, horários)
│
├── public/                   # Assets estáticos
│   ├── styles/               # CSS
│   │   ├── main.css
│   │   └── partials/         # Estilos por página
│   ├── scripts/              # JavaScript do frontend
│   │   └── addField.js       # Adicionar horários dinamicamente
│   └── images/               # Imagens e ícones
│
├── Capa-Proffy-Web-Discovery.pdf   # Capa do projeto
├── Proffy-Web-Version-1.pdf        # Design v1 (Figma)
└── Proffy-Web-Version-2.pdf        # Design v2 (Figma)
```

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Uso |
|------------|-----|
| **Node.js** | Runtime JavaScript |
| **Express** | Framework web para servidor |
| **Nunjucks** | Template engine para HTML |
| **SQLite** | Banco de dados relacional (via sqlite-async) |
| **HTML5** | Estrutura das páginas |
| **CSS3** | Estilização e responsividade |
| **JavaScript** | Interatividade no frontend |

## 📝 Funcionalidades Principais

### Para Professores
- Cadastro de perfil (nome, avatar, WhatsApp, bio)
- Seleção de matéria lecionada e valor da hora
- Definição de múltiplos horários disponíveis (dia + período)
- Adição dinâmica de horários na página "Dar aulas"

### Para Alunos
- Busca de professores por:
  - **Matéria** (Artes, Biologia, Ciências, Educação física, Física, Geografia, História, Matemática, Português, Química)
  - **Dia da semana**
  - **Horário**
- Contato via WhatsApp com o professor

### Interface
- Landing page com opções "Estudar" e "Dar aulas"
- Página de busca com filtros e listagem de resultados
- Página de cadastro de professor com formulário completo

## 🚀 Como Usar

### Pré-requisitos

- [Node.js](https://nodejs.org/) (v12 ou superior)
- [npm](https://www.npmjs.com/) ou [yarn](https://yarnpkg.com/)

### Instalação

1. **Clone o repositório:**
```bash
git clone https://github.com/HenriqueMAP/nlw.git
cd nlw
```

2. **Instale as dependências:**
```bash
npm install
```

3. **Inicie o servidor:**
```bash
npm run test
```
*(O script `test` utiliza nodemon para reiniciar o servidor automaticamente em alterações.)*

4. **Acesse a aplicação:**
```
http://localhost:5500
```

### Rotas da Aplicação

| Rota | Método | Descrição |
|------|--------|-----------|
| `/` | GET | Página inicial (Landing) |
| `/study` | GET | Busca de professores (aceita query params: subject, weekday, time) |
| `/give-classes` | GET | Formulário de cadastro de professor |
| `/save-classes` | POST | Salva cadastro de professor e redireciona |

## ⚙️ Como Funciona

### Fluxo de Cadastro (Professor)
1. Professor acessa "Dar aulas" na landing
2. Preenche dados pessoais e da aula
3. Adiciona um ou mais horários (dia + período)
4. Formulário envia POST para `/save-classes`
5. Dados são inseridos em `proffys`, `classes` e `class_schedule`
6. Redirecionamento para `/study` com filtros pré-preenchidos

### Fluxo de Busca (Aluno)
1. Aluno acessa "Estudar"
2. Seleciona matéria, dia e horário
3. Query no SQLite filtra professores disponíveis
4. Resultados exibidos com link para WhatsApp

### Banco de Dados (SQLite)
- **proffys**: dados do professor (nome, avatar, WhatsApp, bio)
- **classes**: matéria e valor (vinculado a um proffy)
- **class_schedule**: horários disponíveis (dia, hora início, hora fim)

## 📚 Desafios Propostos

Após concluir a última aula, utilizar a **versão 2.0 do Proffy** disponibilizada no Figma:

| # | Desafio | Descrição |
|---|---------|-----------|
| 01 | Página de sucesso | Exibir página de sucesso após cadastro; aguardar 2s com `setTimeout` e redirecionar para listagem com filtro via `location.href` |
| 02 | Correção de bugs | Botão para remover horário na página "Dar aula"; impedir adicionar novo campo se dia/hora anterior estiver vazio |

## 📄 Licença

Este projeto está licenciado sob a **MIT License** - veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 📖 Referências

- [Rocketseat](https://rocketseat.com.br/)
- [Next Level Week #2](https://nextlevelweek.com/)
- [Express.js](https://expressjs.com/)
- [Nunjucks](https://mozilla.github.io/nunjucks/)
- [SQLite](https://www.sqlite.org/)

## 💼 Conecte-se

- [Perfil no LinkedIn](https://www.linkedin.com/in/henrique-matheus-alves-pereira)
- [GitHub](https://github.com/HenriqueMAP)

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Faça um **fork** deste repositório
2. Crie um **branch** para sua feature (`git checkout -b feature/nova-feature`)
3. Faça **commit** das suas mudanças (`git commit -am 'Adiciona nova feature'`)
4. Faça **push** para o branch (`git push origin feature/nova-feature`)
5. Abra um **Pull Request**

---

<div align="center">

> **Desenvolvido com 💜 durante a Next Level Week #2**

</div>
