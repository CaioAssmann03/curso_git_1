# ☁️ GitHub

O **Git** é um sistema de controle de versão distribuído, enquanto o **GitHub** é uma plataforma que hospeda repositórios Git na nuvem.

Com o GitHub é possível:

- Armazenar projetos online;
- Compartilhar código;
- Trabalhar em equipe;
- Criar Pull Requests;
- Abrir Issues;
- Gerenciar versões;
- Automatizar processos com GitHub Actions.

---

# Git x GitHub

| Git | GitHub |
|------|---------|
| Funciona localmente | Plataforma online |
| Controla versões | Hospeda repositórios |
| Não precisa de internet | Requer internet |
| Software | Serviço Web |

---

# Criando um repositório

1. Faça login no GitHub.
2. Clique em **New Repository**.
3. Escolha um nome.
4. Defina se será Público ou Privado.
5. Clique em **Create Repository**.

---

# git remote

Exibe os repositórios remotos configurados.

```bash
git remote
```

Resultado:

```
origin
```

---

# git remote -v

Mostra os endereços do repositório remoto.

```bash
git remote -v
```

Resultado:

```
origin  https://github.com/usuario/projeto.git (fetch)

origin  https://github.com/usuario/projeto.git (push)
```

---

# git remote add

Conecta um repositório local ao GitHub.

```bash
git remote add origin https://github.com/usuario/projeto.git
```

Verifique:

```bash
git remote -v
```

---

# git remote remove

Remove um repositório remoto.

```bash
git remote remove origin
```

---

# git remote rename

Renomeia um remoto.

```bash
git remote rename origin github
```

---

# git push

Envia os commits locais para o GitHub.

```bash
git push
```

---

# git push origin main

Envia a branch main.

```bash
git push origin main
```

---

# git push -u origin main

Envia a branch e cria o vínculo entre a branch local e a remota.

```bash
git push -u origin main
```

Depois disso basta utilizar:

```bash
git push
```

---

# git push --force

Força o envio do histórico.

```bash
git push --force
```

⚠ Muito perigoso.

Pode apagar alterações de outros colaboradores.

---

# git push --force-with-lease

Versão mais segura do Force Push.

```bash
git push --force-with-lease
```

É a opção recomendada quando realmente for necessário sobrescrever o histórico.

---

# git fetch

Busca alterações do GitHub sem alterar seu projeto.

```bash
git fetch
```

Você poderá analisar as mudanças antes de fazer Merge.

---

# git pull

Atualiza seu projeto.

Internamente ele executa:

```
git fetch

+

git merge
```

Uso:

```bash
git pull
```

---

# git pull origin main

Atualiza apenas a branch main.

```bash
git pull origin main
```

---

# git pull --rebase

Atualiza utilizando Rebase.

```bash
git pull --rebase
```

Muito utilizado para manter o histórico linear.

---

# git clone

Baixa um projeto existente.

```bash
git clone https://github.com/usuario/repositorio.git
```

Também é possível definir outro nome para a pasta.

```bash
git clone https://github.com/usuario/repositorio.git meu-projeto
```

---

# SSH x HTTPS

## HTTPS

```
https://github.com/usuario/projeto.git
```

Vantagens

- Fácil configuração
- Funciona imediatamente

Desvantagens

- Pode solicitar autenticação

---

## SSH

```
git@github.com:usuario/projeto.git
```

Vantagens

- Não pede senha a cada operação
- Mais prático para uso diário

Desvantagens

- Exige configuração da chave SSH

---

# Gerando uma chave SSH

Criar chave:

```bash
ssh-keygen -t ed25519 -C "email@exemplo.com"
```

Iniciar o agente:

```bash
eval "$(ssh-agent -s)"
```

Adicionar a chave:

```bash
ssh-add ~/.ssh/id_ed25519
```

Copiar a chave pública:

```bash
cat ~/.ssh/id_ed25519.pub
```

Cole essa chave nas configurações do GitHub.

---

# Testando conexão

```bash
ssh -T git@github.com
```

Resultado esperado:

```
Hi username!

You've successfully authenticated...
```

---

# Fork

Um Fork cria uma cópia completa de outro repositório em sua conta.

Fluxo:

```
Projeto Original

↓

Fork

↓

Sua Conta

↓

Clone

↓

Alterações

↓

Pull Request
```

Muito utilizado em projetos Open Source.

---

# Pull Request

O Pull Request (PR) solicita que suas alterações sejam analisadas antes de serem incorporadas ao projeto.

Fluxo:

```
Criar Branch

↓

Commit

↓

Push

↓

Abrir Pull Request

↓

Code Review

↓

Merge
```

---

# O que deve conter um Pull Request?

Um bom Pull Request descreve:

- Objetivo da alteração;
- O problema resolvido;
- Como testar;
- Prints (quando necessário);
- Referência à Issue relacionada.

---

# Code Review

Antes do Merge, outros desenvolvedores analisam:

- Qualidade do código;
- Organização;
- Performance;
- Segurança;
- Padrões do projeto.

---

# Issues

As Issues servem para registrar:

- Bugs;
- Melhorias;
- Novas funcionalidades;
- Documentação;
- Dúvidas.

Exemplo:

```
Título

Corrigir erro no Login

Descrição

Ao tentar realizar login ocorre erro 500.
```

---

# Labels

As Labels organizam as Issues.

Exemplos:

```
bug

documentation

enhancement

good first issue

help wanted
```

---

# Milestones

Agrupam várias Issues em uma versão.

Exemplo:

```
Versão 2.0

✔ Login

✔ Dashboard

✔ API

✔ Perfil
```

---

# Releases

As Releases representam versões oficiais do projeto.

Exemplo:

```
v1.0.0

v1.1.0

v2.0.0
```

Normalmente acompanham Tags.

---

# Tags

Criando uma Tag.

```bash
git tag v1.0.0
```

Enviar:

```bash
git push origin v1.0.0
```

Enviar todas:

```bash
git push --tags
```

---

# GitHub CLI

O GitHub possui uma ferramenta oficial chamada **GitHub CLI (gh)**.

Ver autenticação:

```bash
gh auth status
```

Fazer login:

```bash
gh auth login
```

Clonar um projeto:

```bash
gh repo clone usuario/projeto
```

Criar Pull Request:

```bash
gh pr create
```

Listar PRs:

```bash
gh pr list
```

---

# Fluxo completo

```
git clone

↓

git switch -c feature-login

↓

Alterações

↓

git add .

↓

git commit

↓

git push

↓

Pull Request

↓

Code Review

↓

Merge

↓

git pull
```

---

# Boas práticas

✅ Faça Pull antes de começar a desenvolver.

✅ Utilize uma branch para cada funcionalidade.

✅ Escreva boas mensagens de commit.

✅ Nunca faça Force Push na branch main.

✅ Revise o código antes de abrir um Pull Request.

✅ Mantenha o README atualizado.

✅ Utilize Releases para versões estáveis.

---

# Principais comandos

| Comando | Descrição |
|----------|-----------|
| `git remote -v` | Lista os repositórios remotos |
| `git remote add origin URL` | Adiciona um remoto |
| `git remote remove origin` | Remove um remoto |
| `git push` | Envia commits |
| `git push -u origin main` | Define upstream |
| `git push --force` | Força o envio |
| `git push --force-with-lease` | Force Push seguro |
| `git fetch` | Busca alterações remotas |
| `git pull` | Atualiza o projeto |
| `git pull --rebase` | Atualiza usando Rebase |
| `git clone URL` | Clona um repositório |
| `git tag v1.0.0` | Cria uma tag |
| `git push --tags` | Envia todas as tags |
| `gh auth login` | Login no GitHub CLI |
| `gh pr create` | Cria um Pull Request |

---

# Conclusão

O GitHub complementa o Git ao oferecer uma plataforma para hospedagem, colaboração e gerenciamento de projetos. Dominar recursos como Pull Requests, Issues, Forks, Releases e GitHub CLI é essencial para trabalhar em equipes e contribuir para projetos open source ou corporativos.
