# 🌳 Git Flow

À medida que um projeto cresce, torna-se necessário organizar o desenvolvimento para evitar conflitos e facilitar a colaboração entre desenvolvedores.

Para isso, surgiram estratégias de gerenciamento de branches, conhecidas como **Branching Models**.

As três mais utilizadas atualmente são:

- Git Flow
- GitHub Flow
- Trunk-Based Development

Cada uma possui vantagens e é indicada para diferentes tipos de projeto.

---

# O que é Git Flow?

Git Flow é uma estratégia criada por **Vincent Driessen** em 2010 para organizar o desenvolvimento utilizando branches com funções bem definidas.

É muito utilizada em:

- Grandes empresas
- Sistemas corporativos
- Projetos com versões bem definidas
- Equipes grandes

---

# Estrutura do Git Flow

```

main
│
├── develop
│
├── feature/login
├── feature/dashboard
├── feature/api
│
├── release/v1.0.0
│
└── hotfix/login

```

Cada tipo de branch possui uma finalidade específica.

---

# Branch Main

A branch **main** representa a versão estável do sistema.

Ela deve conter apenas código testado e pronto para produção.

Nunca desenvolva diretamente nela.

---

# Branch Develop

A branch **develop** reúne todas as funcionalidades em desenvolvimento.

Fluxo:

```

feature

↓

develop

↓

release

↓

main

```

---

# Feature Branch

Cada nova funcionalidade deve possuir sua própria branch.

Exemplos:

```

feature/login

feature/dashboard

feature/api

feature/cadastro

```

Criando:

```bash
git switch develop

git pull

git switch -c feature/login
```

Após concluir:

```bash
git switch develop

git merge feature/login
```

---

# Release Branch

Quando todas as funcionalidades estiverem prontas:

```
develop

↓

release/v1.0.0
```

Nessa etapa são realizados:

- testes;
- correções;
- documentação;
- ajustes finais.

Após aprovação:

```
release

↓

main

↓

develop
```

---

# Hotfix

Caso um erro grave aconteça em produção:

```
main

↓

hotfix/login

↓

main

↓

develop
```

Criando:

```bash
git switch main

git switch -c hotfix/login
```

Depois:

```bash
git merge hotfix/login
```

---

# Fluxo completo do Git Flow

```
main
 │
 │
 ▼
develop
 │
 ├──────────────┐
 │              │
 ▼              ▼
feature      feature
 │              │
 └──────┬───────┘
        │
        ▼
    develop
        │
        ▼
 release/v1.0.0
        │
        ▼
      main
```

---

# Vantagens do Git Flow

✅ Organização

✅ Histórico bem definido

✅ Fácil controle de versões

✅ Ideal para grandes equipes

---

# Desvantagens

- Muitas branches
- Fluxo mais complexo
- Não é ideal para entregas muito rápidas

---

# GitHub Flow

O GitHub criou uma estratégia muito mais simples.

Fluxo:

```
main

↓

feature/login

↓

Pull Request

↓

Code Review

↓

Merge

↓

main
```

Não existe branch develop.

---

## Como funciona?

1. Criar uma branch.

```bash
git switch -c feature/login
```

---

2. Desenvolver.

---

3. Commit.

```bash
git commit -m "Criando tela de login"
```

---

4. Push.

```bash
git push origin feature/login
```

---

5. Pull Request.

---

6. Merge.

---

7. Excluir branch.

---

# Quando utilizar GitHub Flow?

Ideal para:

- Startups
- Projetos pequenos
- APIs
- Aplicações Web
- Deploy contínuo

---

# Trunk-Based Development

Hoje muitas empresas como Google e Meta utilizam essa estratégia.

Existe apenas uma branch principal.

```
main

↓

Commits pequenos

↓

Deploy contínuo
```

As funcionalidades são protegidas por **Feature Flags**.

---

# O que são Feature Flags?

São recursos que permitem esconder funcionalidades do usuário.

Exemplo:

```javascript
if (featureLoginNovo) {
    mostrarNovoLogin();
}
```

Assim é possível enviar código para produção sem disponibilizar a funcionalidade imediatamente.

---

# Comparação entre os modelos

| Git Flow | GitHub Flow | Trunk-Based |
|-----------|-------------|-------------|
| Muito organizado | Simples | Extremamente simples |
| Muitas branches | Poucas branches | Apenas uma branch principal |
| Ideal para grandes equipes | Equipes pequenas e médias | Times de alta performance |
| Releases planejadas | Deploy frequente | Deploy contínuo |

---

# Convenção de nomes

## Feature

```
feature/login

feature/dashboard

feature/api
```

---

## Bugfix

```
bugfix/login

bugfix/navbar

bugfix/api
```

---

## Hotfix

```
hotfix/security

hotfix/payment
```

---

## Refactor

```
refactor/auth

refactor/database
```

---

## Docs

```
docs/readme

docs/api
```

---

## Test

```
test/login

test/api
```

---

## Release

```
release/v1.0.0

release/v2.1.0
```

---

# Fluxo recomendado para projetos pessoais

```
main

↓

feature/projeto

↓

Commit

↓

Push

↓

Pull Request

↓

Merge

↓

Delete Branch
```

Mesmo trabalhando sozinho, esse fluxo ajuda a criar bons hábitos.

---

# Fluxo recomendado para empresas

```
main

↓

develop

↓

feature

↓

Pull Request

↓

Code Review

↓

Merge

↓

Release

↓

Produção
```

---

# Dicas

✅ Nunca desenvolva diretamente na `main`.

✅ Crie uma branch para cada funcionalidade.

✅ Faça Pull Requests pequenos.

✅ Exclua branches antigas.

✅ Utilize nomes descritivos.

✅ Atualize sua branch antes do Merge.

---

# Resumo

| Branch | Objetivo |
|----------|-----------|
| `main` | Código em produção |
| `develop` | Integração das funcionalidades |
| `feature/*` | Desenvolvimento de funcionalidades |
| `release/*` | Preparação para uma nova versão |
| `hotfix/*` | Correções urgentes em produção |
| `bugfix/*` | Correções de bugs |
| `docs/*` | Alterações na documentação |
| `refactor/*` | Refatoração de código |
| `test/*` | Testes |

---

# Conclusão

Escolher um modelo de branching adequado é essencial para manter um projeto organizado e facilitar a colaboração. O **Git Flow** é indicado para projetos grandes e com ciclos de lançamento bem definidos. O **GitHub Flow** é ideal para aplicações com entregas frequentes e integração contínua. Já o **Trunk-Based Development** é amplamente utilizado em equipes de alta performance que realizam deploys contínuos e trabalham com pequenas alterações integradas rapidamente à branch principal.
