# 🔀 Merge e Rebase

Quando trabalhamos com branches, chega um momento em que precisamos unir as alterações desenvolvidas. O Git oferece duas formas principais de fazer isso:

- **Merge** (Mescla)
- **Rebase** (Reescreve o histórico)

Ambos possuem o mesmo objetivo: integrar alterações de uma branch em outra, porém funcionam de maneiras diferentes.

---

# Merge

O comando `git merge` une duas branches preservando o histórico original.

Imagine o seguinte cenário:

```
main

A ---- B ---- C
         \
feature    D ---- E
```

Após executar:

```bash
git switch main
git merge feature
```

O Git cria um novo commit chamado **Merge Commit**.

Resultado:

```
A ---- B ---- C -------- M
         \             /
          D -------- E
```

O histórico continua mostrando que existiram duas linhas de desenvolvimento.

---

# Vantagens do Merge

✅ Mantém o histórico original.

✅ Fácil de entender.

✅ Não altera commits antigos.

✅ Mais seguro para projetos em equipe.

---

# Desvantagens

- O histórico pode ficar mais "poluído".
- Muitos Merge Commits podem dificultar a leitura.

---

# git merge

Une a branch atual com outra branch.

```bash
git merge feature-login
```

---

# Fast Forward Merge

Quando não existem commits novos na branch principal, o Git apenas move o ponteiro da branch.

Antes:

```
main

A ---- B

feature

A ---- B ---- C ---- D
```

Após:

```bash
git merge feature
```

Resultado:

```
main

A ---- B ---- C ---- D
```

Nenhum commit extra é criado.

Esse processo é chamado de **Fast Forward**.

---

# git merge --no-ff

Força a criação de um Merge Commit mesmo quando seria possível realizar um Fast Forward.

```bash
git merge --no-ff feature-login
```

Resultado:

```
A ---- B ---- C -------- M
         \             /
          D -------- E
```

Muito utilizado em empresas porque deixa claro quando uma funcionalidade foi integrada.

---

# git merge --abort

Cancela um Merge em andamento.

```bash
git merge --abort
```

Muito útil quando surgem conflitos difíceis de resolver.

---

# O que é um conflito?

Um conflito acontece quando duas branches modificam a mesma parte de um arquivo.

Exemplo.

Na branch **main**:

```js
const nome = "João";
```

Na branch **feature**:

```js
const nome = "Maria";
```

Ao executar:

```bash
git merge feature
```

O Git não sabe qual alteração manter.

Ele exibirá uma mensagem semelhante a:

```
CONFLICT (content): Merge conflict in app.js
```

---

# Como resolver um conflito

O Git marca o arquivo desta forma:

```text
<<<<<<< HEAD

const nome = "João";

=======

const nome = "Maria";

>>>>>>> feature
```

Você deve editar manualmente o arquivo, removendo as marcações.

Depois:

```bash
git add .

git commit
```

---

# git rebase

O Rebase possui o mesmo objetivo do Merge, porém funciona de outra maneira.

Ele "reposiciona" os commits de uma branch sobre outra.

Antes:

```
main

A ---- B ---- C

feature

A ---- B ---- D ---- E
```

Executando:

```bash
git switch feature

git rebase main
```

Resultado:

```
A ---- B ---- C ---- D' ---- E'
```

Os commits D e E são recriados.

Perceba que não existe Merge Commit.

O histórico fica linear.

---

# Vantagens do Rebase

✅ Histórico limpo.

✅ Fácil de ler.

✅ Evita vários Merge Commits.

---

# Desvantagens

- Reescreve o histórico.
- Pode causar problemas se utilizado em branches compartilhadas.

---

# Quando usar Rebase?

Ideal para:

- Atualizar sua branch antes do Pull Request.
- Organizar o histórico local.
- Projetos que utilizam histórico linear.

Evite utilizar Rebase em branches públicas.

---

# git rebase

Atualiza a branch atual utilizando outra branch como base.

```bash
git rebase main
```

---

# git rebase --continue

Após resolver um conflito durante o Rebase.

```bash
git rebase --continue
```

---

# git rebase --abort

Cancela o Rebase.

```bash
git rebase --abort
```

---

# git rebase -i

Rebase Interativo.

Permite:

- juntar commits
- apagar commits
- alterar mensagens
- reorganizar commits

```bash
git rebase -i HEAD~5
```

O Git abrirá uma lista semelhante a:

```
pick

pick

pick

pick

pick
```

Você pode alterar para:

```
pick

squash

reword

drop

edit
```

---

# Squash

O Squash junta vários commits em apenas um.

Antes:

```
Criando Login

Corrigindo Login

Ajustando Login

Alterando CSS

Finalizando Login
```

Depois:

```
Implementando tela de login
```

Isso deixa o histórico muito mais organizado.

---

# Cherry Pick

Permite copiar apenas um commit específico para outra branch.

```bash
git cherry-pick 3f4b9a2
```

Muito útil quando apenas uma alteração precisa ser reaproveitada.

---

# Comparação

| Merge | Rebase |
|--------|---------|
| Mantém histórico original | Reescreve histórico |
| Cria Merge Commit | Não cria Merge Commit |
| Mais seguro | Mais limpo |
| Melhor para equipes | Melhor para organização local |

---

# Fluxo recomendado utilizando Merge

```text
main

↓

Criar branch

↓

Desenvolver

↓

Commit

↓

Push

↓

Pull Request

↓

Merge

↓

Excluir Branch
```

---

# Fluxo recomendado utilizando Rebase

```text
main

↓

Criar Branch

↓

Desenvolver

↓

git fetch

↓

git rebase origin/main

↓

Resolver conflitos

↓

Push

↓

Pull Request
```

---

# Boas práticas

✅ Faça Merge na `main`.

✅ Utilize Rebase apenas em branches locais.

✅ Nunca faça Rebase em branches compartilhadas.

✅ Faça commits pequenos.

✅ Resolva conflitos imediatamente.

✅ Revise sempre o histórico antes de realizar Merge.

---

# Principais comandos

| Comando | Função |
|----------|---------|
| `git merge branch` | Mescla duas branches |
| `git merge --no-ff` | Força Merge Commit |
| `git merge --abort` | Cancela um Merge |
| `git rebase main` | Reposiciona commits |
| `git rebase --continue` | Continua após conflito |
| `git rebase --abort` | Cancela o Rebase |
| `git rebase -i HEAD~n` | Rebase interativo |
| `git cherry-pick hash` | Copia um commit específico |
| `git log --graph --oneline --all` | Exibe o histórico gráfico |

---

# Conclusão

O **Merge** e o **Rebase** são duas estratégias para integrar alterações entre branches. O Merge preserva o histórico original e é a opção mais segura para equipes, enquanto o Rebase reorganiza os commits para criar um histórico linear e mais limpo. Saber quando utilizar cada abordagem é uma habilidade essencial para qualquer desenvolvedor que trabalhe com Git em ambientes profissionais.
