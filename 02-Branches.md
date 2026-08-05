# 🌿 Trabalhando com Branches

Uma **branch** é uma ramificação do projeto. Ela permite desenvolver novas funcionalidades, corrigir bugs ou realizar testes sem afetar a versão principal do código.

Imagine que a branch **main** é a linha principal do projeto. Sempre que uma nova funcionalidade for desenvolvida, é recomendado criar uma nova branch.

---

# O que é uma Branch?

Exemplo:

```
main

A --- B --- C
```

Criando uma nova branch:

```
main

A --- B --- C
             \
feature-login  D --- E
```

Após finalizar o desenvolvimento, essa branch poderá ser unida novamente à **main** através de um **Merge**.

---

# git branch

Lista todas as branches existentes.

```bash
git branch
```

Exemplo:

```
* main
  develop
  feature-login
```

O asterisco (*) indica a branch atual.

---

# git branch <nome>

Cria uma nova branch.

```bash
git branch feature-login
```

Após executar esse comando, você continuará na branch atual.

---

# git switch

Troca para outra branch.

```bash
git switch feature-login
```

Resultado:

```
Switched to branch 'feature-login'
```

---

# git switch -c

Cria uma nova branch e já muda para ela.

```bash
git switch -c feature-dashboard
```

É equivalente a:

```bash
git branch feature-dashboard

git switch feature-dashboard
```

---

# git checkout

Versão antiga para trocar de branch.

```bash
git checkout feature-login
```

Hoje recomenda-se utilizar:

```bash
git switch feature-login
```

pois deixa o comando mais intuitivo.

---

# git checkout -b

Cria uma branch e troca para ela.

```bash
git checkout -b feature-api
```

Equivalente a:

```bash
git branch feature-api

git checkout feature-api
```

Hoje pode ser substituído por:

```bash
git switch -c feature-api
```

---

# git branch -v

Lista todas as branches juntamente com o último commit.

```bash
git branch -v
```

Exemplo:

```
* main           4fa7c18 Atualizando README
  develop        a4d82fd Criando API
  feature-login  b8e97d2 Tela de Login
```

---

# git branch -a

Mostra todas as branches locais e remotas.

```bash
git branch -a
```

Exemplo:

```
* main
  develop
  remotes/origin/main
  remotes/origin/develop
```

---

# git branch -r

Mostra apenas as branches remotas.

```bash
git branch -r
```

---

# git branch -d

Remove uma branch local que já foi integrada.

```bash
git branch -d feature-login
```

Caso a branch ainda possua commits não mesclados, o Git impedirá sua exclusão.

---

# git branch -D

Força a exclusão da branch.

```bash
git branch -D feature-login
```

⚠ Utilize com cuidado.

Esse comando apaga a branch mesmo que existam alterações ainda não integradas.

---

# git branch -m

Renomeia uma branch.

Renomeando a branch atual:

```bash
git branch -m nova-branch
```

Renomeando outra branch:

```bash
git branch -m antiga nova
```

---

# git branch --merged

Lista as branches que já foram mescladas.

```bash
git branch --merged
```

Muito útil para limpar branches antigas.

---

# git branch --no-merged

Lista apenas branches que ainda não foram mescladas.

```bash
git branch --no-merged
```

---

# git merge

Une duas branches.

Exemplo:

Estamos na branch **main**.

```
main

A --- B --- C
         \
feature   D --- E
```

Executando:

```bash
git merge feature
```

Resultado:

```
A --- B --- C -------- M
         \           /
          D ------- E
```

A branch feature continua existindo.

---

# git merge --no-ff

Força a criação de um commit de Merge.

```bash
git merge --no-ff feature-login
```

Esse comando preserva o histórico da branch, facilitando auditorias e revisões de código.

Muito utilizado em equipes.

---

# git merge --abort

Cancela um merge em andamento.

```bash
git merge --abort
```

Útil quando ocorre conflito.

---

# git log --graph

Exibe o histórico das branches em formato gráfico.

```bash
git log --graph --oneline --all
```

Exemplo:

```
* 8ad43c Merge branch feature-login
|\
| * 9bc123 Criando Login
| * 4af23b Ajustando CSS
|/
* 1ca552 Atualizando README
```

É um dos comandos mais úteis para visualizar o histórico do projeto.

---

# Fluxo recomendado

1. Atualize a branch principal.

```bash
git switch main
git pull
```

---

2. Crie uma nova branch.

```bash
git switch -c feature-login
```

---

3. Faça suas alterações.

---

4. Adicione os arquivos.

```bash
git add .
```

---

5. Crie um commit.

```bash
git commit -m "Implementando tela de login"
```

---

6. Envie para o GitHub.

```bash
git push -u origin feature-login
```

---

7. Abra um Pull Request.

---

8. Após aprovação, faça o Merge.

---

9. Exclua a branch.

```bash
git branch -d feature-login
```

---

# Convenção de nomes

Boas práticas para nomear branches.

```
feature/login

feature/dashboard

feature/api

bugfix/login

bugfix/navbar

hotfix/security

release/v1.0.0

docs/readme

refactor/auth

test/api
```

Evite:

```
teste

nova

branch1

caio

projeto2

aaaa
```

Sempre utilize nomes que descrevam claramente o objetivo da branch.

---

# Boas práticas

✅ Crie uma branch para cada funcionalidade.

✅ Nunca desenvolva diretamente na `main`.

✅ Faça commits pequenos e frequentes.

✅ Atualize sua branch antes de abrir um Pull Request.

✅ Exclua branches antigas após o Merge.

✅ Utilize nomes padronizados para facilitar a organização do projeto.

---

# Resumo dos principais comandos

| Comando | Descrição |
|----------|-----------|
| `git branch` | Lista as branches |
| `git branch nome` | Cria uma branch |
| `git switch nome` | Troca de branch |
| `git switch -c nome` | Cria e troca para a branch |
| `git checkout nome` | Troca de branch (antigo) |
| `git checkout -b nome` | Cria e troca de branch (antigo) |
| `git branch -v` | Lista branches com último commit |
| `git branch -a` | Lista branches locais e remotas |
| `git branch -r` | Lista apenas branches remotas |
| `git branch -d` | Remove uma branch |
| `git branch -D` | Força a remoção |
| `git branch -m` | Renomeia uma branch |
| `git branch --merged` | Branches já mescladas |
| `git branch --no-merged` | Branches pendentes |
| `git merge` | Une duas branches |
| `git merge --no-ff` | Cria um commit de merge |
| `git merge --abort` | Cancela um merge |
| `git log --graph --oneline --all` | Exibe o histórico em formato gráfico |
