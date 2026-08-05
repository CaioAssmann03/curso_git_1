# 🚑 Desfazendo Erros

Errar faz parte do desenvolvimento. Felizmente, o Git oferece diversas ferramentas para recuperar arquivos, desfazer commits e restaurar versões anteriores do projeto.

Neste capítulo você aprenderá os principais comandos utilizados para corrigir erros sem comprometer o histórico do projeto.

---

# Entendendo os estados dos arquivos

Antes de aprender os comandos, é importante entender como o Git controla os arquivos.

```
Working Directory
        │
        ▼
Staging Area
        │
        ▼
Repository
```

- **Working Directory:** onde você edita seus arquivos.
- **Staging Area:** arquivos preparados para o próximo commit.
- **Repository:** histórico de commits.

Dependendo de onde o erro aconteceu, o comando utilizado será diferente.

---

# git restore

Restaura um arquivo para a última versão salva.

```bash
git restore arquivo.txt
```

Esse comando descarta todas as alterações feitas no arquivo.

---

## Restaurar todos os arquivos

```bash
git restore .
```

Volta todos os arquivos modificados para o último commit.

⚠ Atenção: essa operação não pode ser desfeita.

---

# git restore --staged

Remove um arquivo da Staging Area.

Imagine:

```bash
git add .
```

Você adicionou um arquivo por engano.

Remova apenas ele:

```bash
git restore --staged arquivo.txt
```

O arquivo continua modificado, apenas deixa de estar preparado para o commit.

---

# git reset

O comando reset altera o ponteiro do HEAD.

Existem três modos principais:

- soft
- mixed
- hard

---

# git reset --soft

Remove commits mantendo tudo preparado para um novo commit.

Exemplo:

```
A --- B --- C
```

Executando:

```bash
git reset --soft HEAD~1
```

Resultado:

```
A --- B
```

As alterações do commit C continuam na Staging Area.

Ideal para corrigir mensagens de commit ou juntar commits.

---

# git reset --mixed

É o comportamento padrão do Git.

```bash
git reset HEAD~1
```

ou

```bash
git reset --mixed HEAD~1
```

Resultado:

- Remove o commit.
- Remove os arquivos da Staging Area.
- Mantém as alterações no projeto.

---

# git reset --hard

Apaga completamente os commits e as alterações locais.

```bash
git reset --hard HEAD~1
```

Resultado:

```
A --- B
```

O commit C desaparece completamente.

⚠ Utilize apenas quando tiver certeza.

---

# git revert

Desfaz um commit sem alterar o histórico.

Imagine:

```
A --- B --- C
```

Executando:

```bash
git revert C
```

Resultado:

```
A --- B --- C --- D
```

O commit D desfaz todas as alterações feitas por C.

É o método recomendado para projetos compartilhados.

---

# Qual a diferença entre Reset e Revert?

| Reset | Revert |
|--------|---------|
| Remove commits | Cria um novo commit |
| Reescreve histórico | Mantém histórico |
| Uso local | Uso em equipe |
| Pode apagar trabalho | Muito mais seguro |

---

# git checkout

Embora atualmente o recomendado seja utilizar `git switch` e `git restore`, ainda é comum encontrar:

```bash
git checkout arquivo.txt
```

Ele restaura o arquivo.

Hoje o equivalente é:

```bash
git restore arquivo.txt
```

---

# git clean

Remove arquivos não rastreados pelo Git.

Visualizar o que será removido:

```bash
git clean -n
```

Remover:

```bash
git clean -f
```

Remover inclusive diretórios:

```bash
git clean -fd
```

Muito útil após testes.

---

# git stash

Guarda temporariamente alterações sem realizar commit.

Imagine que você precisa trocar de branch rapidamente.

```bash
git stash
```

Suas alterações ficam armazenadas.

---

# git stash list

Lista todas as alterações salvas.

```bash
git stash list
```

Exemplo:

```
stash@{0}

stash@{1}
```

---

# git stash pop

Recupera as alterações e remove o stash.

```bash
git stash pop
```

---

# git stash apply

Recupera as alterações mantendo o stash salvo.

```bash
git stash apply
```

---

# git stash drop

Remove um stash específico.

```bash
git stash drop stash@{0}
```

---

# git stash clear

Remove todos os stashes.

```bash
git stash clear
```

---

# git reflog

Um dos comandos mais importantes do Git.

Mostra todas as movimentações do HEAD.

```bash
git reflog
```

Exemplo:

```
a34c9d HEAD@{0}

f45a1e HEAD@{1}

34ab21 HEAD@{2}
```

Mesmo após um reset --hard, normalmente o commit ainda pode ser recuperado utilizando o reflog.

---

# Recuperando um commit perdido

Primeiro:

```bash
git reflog
```

Depois:

```bash
git reset --hard HASH
```

Ou:

```bash
git checkout HASH
```

---

# git diff

Mostra exatamente o que foi alterado.

```bash
git diff
```

Comparando commits:

```bash
git diff HEAD~1 HEAD
```

Comparando branches:

```bash
git diff main feature-login
```

---

# git show

Mostra informações completas de um commit.

```bash
git show
```

Ou:

```bash
git show HASH
```

---

# git log

Visualiza o histórico.

```bash
git log
```

Versão resumida:

```bash
git log --oneline
```

Versão gráfica:

```bash
git log --graph --oneline --all
```

---

# Recuperando arquivo deletado

Descubra o commit:

```bash
git log
```

Depois:

```bash
git restore --source=HASH arquivo.txt
```

---

# Recuperando apenas um arquivo

Também é possível recuperar um arquivo específico de outra branch.

```bash
git restore --source=main README.md
```

---

# Situações comuns

## Adicionei arquivos errados

```bash
git restore --staged .
```

---

## Editei um arquivo por engano

```bash
git restore arquivo.txt
```

---

## Fiz commit com mensagem errada

```bash
git commit --amend
```

---

## Quero apagar o último commit

```bash
git reset --soft HEAD~1
```

---

## Quero apagar tudo

```bash
git reset --hard HEAD
```

---

## Quero salvar temporariamente meu trabalho

```bash
git stash
```

---

## Quero recuperar trabalho perdido

```bash
git reflog
```

---

# Fluxograma

```
Erro?

│

├── Alteração ainda não foi adicionada?

│        │

│        └── git restore

│

├── Está na Staging?

│        │

│        └── git restore --staged

│

├── Já fez commit?

│        │

│        ├── git reset

│        └── git revert

│

└── Perdeu tudo?

         │

         └── git reflog
```

---

# Boas práticas

✅ Utilize `git revert` em projetos compartilhados.

✅ Evite `git reset --hard` sem necessidade.

✅ Consulte o `git diff` antes de descartar alterações.

✅ Faça commits pequenos.

✅ Utilize `git stash` antes de trocar de branch.

✅ Aprenda a utilizar `git reflog`.

Ele pode salvar horas de trabalho.

---

# Resumo dos comandos

| Comando | Função |
|----------|---------|
| `git restore arquivo` | Restaura arquivo |
| `git restore .` | Restaura tudo |
| `git restore --staged` | Remove da Staging Area |
| `git reset --soft` | Remove commit mantendo alterações preparadas |
| `git reset --mixed` | Remove commit mantendo alterações locais |
| `git reset --hard` | Remove tudo |
| `git revert` | Desfaz um commit criando outro |
| `git clean -f` | Remove arquivos não rastreados |
| `git stash` | Guarda alterações temporariamente |
| `git stash list` | Lista stashes |
| `git stash pop` | Recupera e remove stash |
| `git stash apply` | Recupera mantendo stash |
| `git stash drop` | Remove um stash |
| `git stash clear` | Remove todos os stashes |
| `git reflog` | Histórico do HEAD |
| `git diff` | Mostra diferenças |
| `git show` | Exibe detalhes de um commit |
| `git log --graph --oneline --all` | Histórico gráfico |

---

# Conclusão

Saber desfazer alterações é tão importante quanto saber criar commits. Comandos como `git restore`, `git reset`, `git revert`, `git stash` e `git reflog` fazem parte do dia a dia de qualquer desenvolvedor e permitem recuperar rapidamente alterações, corrigir erros e manter o histórico do projeto organizado e seguro.
