# 📚 Git & GitHub Cheat Sheet

> Um guia rápido com os principais comandos do Git e GitHub para consulta durante o desenvolvimento.

---

# Inicializando um Repositório

| Comando | Descrição |
|----------|-----------|
| `git init` | Inicializa um repositório Git |
| `git clone URL` | Clona um repositório remoto |
| `git --version` | Exibe a versão instalada |
| `git config --list` | Lista as configurações atuais |

---

# Configuração

| Comando | Descrição |
|----------|-----------|
| `git config --global user.name "Nome"` | Define o nome do usuário |
| `git config --global user.email "email@email.com"` | Define o e-mail |
| `git config --global init.defaultBranch main` | Define a branch padrão |
| `git config --global core.editor "code --wait"` | Define o editor padrão |

---

# Status e Informações

| Comando | Descrição |
|----------|-----------|
| `git status` | Mostra o estado do repositório |
| `git log` | Histórico completo |
| `git log --oneline` | Histórico resumido |
| `git log --graph --oneline --all` | Histórico gráfico |
| `git show` | Mostra detalhes do último commit |
| `git diff` | Exibe alterações |
| `git reflog` | Histórico do HEAD |

---

# Trabalhando com Arquivos

| Comando | Descrição |
|----------|-----------|
| `git add arquivo` | Adiciona um arquivo |
| `git add .` | Adiciona todos os arquivos |
| `git add -A` | Adiciona todas as alterações |
| `git restore arquivo` | Restaura um arquivo |
| `git restore .` | Restaura todos os arquivos |
| `git restore --staged arquivo` | Remove da Staging Area |
| `git rm arquivo` | Remove arquivo do Git |
| `git mv antigo novo` | Renomeia ou move um arquivo |

---

# Commits

| Comando | Descrição |
|----------|-----------|
| `git commit -m "Mensagem"` | Cria um commit |
| `git commit --amend` | Edita o último commit |
| `git commit -am "Mensagem"` | Adiciona e cria commit |

---

# Branches

| Comando | Descrição |
|----------|-----------|
| `git branch` | Lista branches |
| `git branch nome` | Cria uma branch |
| `git branch -d nome` | Remove branch |
| `git branch -D nome` | Força remoção |
| `git branch -m novo` | Renomeia branch |
| `git branch -a` | Lista branches locais e remotas |
| `git switch nome` | Troca de branch |
| `git switch -c nome` | Cria e troca de branch |
| `git checkout -b nome` | Cria e troca (legado) |

---

# Merge e Rebase

| Comando | Descrição |
|----------|-----------|
| `git merge branch` | Mescla branches |
| `git merge --abort` | Cancela merge |
| `git merge --no-ff` | Força Merge Commit |
| `git rebase main` | Rebase na branch main |
| `git rebase --continue` | Continua o rebase |
| `git rebase --abort` | Cancela o rebase |
| `git rebase -i HEAD~5` | Rebase interativo |
| `git cherry-pick HASH` | Copia um commit |

---

# GitHub

| Comando | Descrição |
|----------|-----------|
| `git remote -v` | Lista remotos |
| `git remote add origin URL` | Adiciona remoto |
| `git remote remove origin` | Remove remoto |
| `git fetch` | Busca alterações |
| `git pull` | Atualiza projeto |
| `git pull --rebase` | Atualiza usando rebase |
| `git push` | Envia commits |
| `git push -u origin main` | Define upstream |
| `git push --force-with-lease` | Force Push seguro |
| `git clone URL` | Clona um projeto |

---

# Tags

| Comando | Descrição |
|----------|-----------|
| `git tag` | Lista tags |
| `git tag v1.0.0` | Cria uma tag |
| `git push origin v1.0.0` | Envia uma tag |
| `git push --tags` | Envia todas as tags |

---

# Recuperando Erros

| Comando | Descrição |
|----------|-----------|
| `git reset --soft HEAD~1` | Remove commit mantendo alterações preparadas |
| `git reset --mixed HEAD~1` | Remove commit mantendo alterações locais |
| `git reset --hard HEAD~1` | Remove commit e alterações |
| `git revert HASH` | Desfaz um commit criando outro |
| `git clean -f` | Remove arquivos não rastreados |
| `git clean -fd` | Remove arquivos e diretórios |

---

# Stash

| Comando | Descrição |
|----------|-----------|
| `git stash` | Guarda alterações temporariamente |
| `git stash list` | Lista stashes |
| `git stash pop` | Recupera e remove o stash |
| `git stash apply` | Recupera mantendo o stash |
| `git stash drop` | Remove um stash |
| `git stash clear` | Remove todos os stashes |

---

# Comandos Avançados

| Comando | Descrição |
|----------|-----------|
| `git blame arquivo` | Mostra quem alterou cada linha |
| `git grep texto` | Pesquisa texto no projeto |
| `git bisect start` | Inicia busca por bug |
| `git worktree add` | Trabalha com várias branches |
| `git archive` | Exporta projeto |
| `git gc` | Otimiza o repositório |
| `git fsck` | Verifica integridade |
| `git notes` | Adiciona anotações |
| `git describe` | Mostra a tag mais próxima |
| `git shortlog -sn` | Estatísticas por autor |

---

# GitHub CLI

| Comando | Descrição |
|----------|-----------|
| `gh auth login` | Login no GitHub |
| `gh auth status` | Verifica autenticação |
| `gh repo clone usuario/projeto` | Clona repositório |
| `gh pr create` | Cria Pull Request |
| `gh pr list` | Lista Pull Requests |

---

# Conventional Commits

| Prefixo | Utilização |
|----------|------------|
| `feat:` | Nova funcionalidade |
| `fix:` | Correção de bug |
| `docs:` | Documentação |
| `style:` | Formatação |
| `refactor:` | Refatoração |
| `test:` | Testes |
| `perf:` | Performance |
| `build:` | Build |
| `ci:` | Integração Contínua |
| `chore:` | Manutenção |

---

# Fluxo Profissional

```text
git pull

↓

git switch -c feature/nova-funcionalidade

↓

Desenvolver

↓

git status

↓

git add .

↓

git commit -m "feat: adicionar nova funcionalidade"

↓

git push -u origin feature/nova-funcionalidade

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

# Dicas Rápidas

💡 Faça commits pequenos e frequentes.

💡 Nunca trabalhe diretamente na `main`.

💡 Sempre revise com `git diff` antes de commitar.

💡 Utilize `git status` constantemente.

💡 Prefira `git push --force-with-lease` ao invés de `git push --force`.

💡 Utilize `git stash` quando precisar trocar de branch sem perder alterações.

💡 Aprenda a usar `git reflog`: ele pode recuperar commits aparentemente perdidos.

💡 Mantenha o `.gitignore` atualizado e nunca envie arquivos sensíveis para o repositório.

---

# Referências Oficiais

- Git Documentation: https://git-scm.com/docs
- Pro Git Book: https://git-scm.com/book
- GitHub Docs: https://docs.github.com/

---

# Conclusão

Este Cheat Sheet reúne os comandos mais importantes do Git e GitHub para servir como referência rápida durante o desenvolvimento. Consulte-o sempre que precisar relembrar um comando, revisar um fluxo de trabalho ou solucionar problemas comuns.
