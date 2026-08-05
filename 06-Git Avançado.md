# 🚀 Git Avançado

Após dominar os comandos básicos do Git, é hora de conhecer ferramentas mais avançadas. Elas ajudam a investigar problemas, otimizar repositórios, trabalhar com múltiplas cópias do projeto e manipular o histórico de forma mais eficiente.

---

# git cherry-pick

Aplica um commit específico de outra branch na branch atual.

Imagine:

```
main

A ---- B ---- C

feature

A ---- B ---- D ---- E
```

Você deseja trazer apenas o commit **D** para a branch `main`.

```bash
git switch main

git cherry-pick HASH_DO_COMMIT
```

Resultado:

```
A ---- B ---- C ---- D'
```

O commit será copiado para a branch atual.

---

## Quando utilizar?

- Aproveitar uma correção de bug.
- Copiar apenas uma funcionalidade.
- Evitar fazer Merge completo.

---

# git blame

Mostra quem alterou cada linha de um arquivo.

```bash
git blame app.js
```

Resultado:

```
3fa2d12 João      2026-06-10

const nome = "Caio";
```

Muito útil para descobrir:

- quem fez determinada alteração;
- quando foi feita;
- qual commit realizou a modificação.

---

# git grep

Pesquisa texto dentro do repositório.

```bash
git grep "login"
```

Pesquisar somente arquivos JavaScript:

```bash
git grep "login" -- "*.js"
```

É muito mais rápido que procurar manualmente.

---

# git bisect

Ajuda a descobrir qual commit introduziu um bug.

Imagine:

```
A ✔

B ✔

C ✔

D ❌

E ❌

F ❌
```

Em vez de testar commit por commit, o Git utiliza busca binária.

Iniciando:

```bash
git bisect start
```

Commit com erro:

```bash
git bisect bad
```

Último commit funcionando:

```bash
git bisect good HASH
```

O Git irá indicar qual commit testar até encontrar o responsável.

Finalizar:

```bash
git bisect reset
```

---

# git worktree

Permite abrir várias branches ao mesmo tempo em diretórios diferentes.

Adicionar uma nova árvore:

```bash
git worktree add ../projeto-feature feature-login
```

Agora você terá:

```
Projeto/

Projeto-feature/
```

Cada pasta pode estar em uma branch diferente.

Muito útil para:

- corrigir bugs enquanto desenvolve outra feature;
- comparar implementações;
- evitar trocar constantemente de branch.

---

# git archive

Cria um arquivo compactado do projeto sem incluir a pasta `.git`.

ZIP:

```bash
git archive --format=zip HEAD -o projeto.zip
```

TAR:

```bash
git archive --format=tar HEAD -o projeto.tar
```

Muito utilizado para distribuir versões do projeto.

---

# git gc

Executa a limpeza e otimização do repositório.

```bash
git gc
```

Ele:

- remove objetos desnecessários;
- compacta arquivos;
- melhora a performance.

Na maioria das vezes o Git executa esse processo automaticamente.

---

# git fsck

Verifica a integridade do repositório.

```bash
git fsck
```

Detecta:

- objetos corrompidos;
- commits perdidos;
- referências inválidas.

Muito utilizado quando existe suspeita de corrupção do histórico.

---

# git notes

Permite adicionar anotações aos commits sem modificar seu conteúdo.

Adicionar:

```bash
git notes add -m "Revisado pela equipe."
```

Visualizar:

```bash
git notes show
```

---

# git describe

Mostra a tag mais próxima de um commit.

```bash
git describe
```

Exemplo:

```
v1.2.0-4-gab12ef3
```

Indica:

- última tag encontrada;
- quantidade de commits desde a tag;
- hash do commit atual.

---

# git shortlog

Gera estatísticas dos commits.

```bash
git shortlog
```

Agrupando por autor:

```bash
git shortlog -sn
```

Resultado:

```
150 João

90 Maria

32 Pedro
```

Muito utilizado para gerar relatórios.

---

# git rev-parse

Mostra informações sobre referências do Git.

Hash do HEAD:

```bash
git rev-parse HEAD
```

Nome da branch atual:

```bash
git rev-parse --abbrev-ref HEAD
```

---

# git show-branch

Compara branches.

```bash
git show-branch
```

Ajuda a visualizar diferenças entre linhas de desenvolvimento.

---

# git ls-files

Lista todos os arquivos monitorados pelo Git.

```bash
git ls-files
```

Muito útil para scripts de automação.

---

# git cat-file

Mostra informações internas de objetos do Git.

```bash
git cat-file -p HASH
```

Permite visualizar:

- commits;
- blobs;
- árvores.

É uma ferramenta de baixo nível.

---

# git hash-object

Calcula o hash SHA-1 de um arquivo.

```bash
git hash-object arquivo.txt
```

Muito utilizado para entender o funcionamento interno do Git.

---

# git update-index

Manipula diretamente o índice (Staging Area).

Exemplo:

```bash
git update-index --assume-unchanged config.local
```

O Git deixa de verificar alterações nesse arquivo.

Para voltar:

```bash
git update-index --no-assume-unchanged config.local
```

---

# git verify-commit

Verifica a assinatura GPG de um commit.

```bash
git verify-commit HASH
```

---

# git verify-tag

Verifica uma Tag assinada.

```bash
git verify-tag v1.0.0
```

---

# git bundle

Cria um único arquivo contendo todo o histórico do repositório.

Criar:

```bash
git bundle create projeto.bundle --all
```

Clonar:

```bash
git clone projeto.bundle
```

Muito útil para transferir repositórios sem internet.

---

# git config --global alias

Criando atalhos.

Exemplo:

```bash
git config --global alias.st status
```

Agora basta utilizar:

```bash
git st
```

Outro exemplo:

```bash
git config --global alias.lg "log --graph --oneline --all"
```

Agora:

```bash
git lg
```

---

# git maintenance

Executa tarefas de manutenção.

```bash
git maintenance run
```

Melhora o desempenho de repositórios grandes.

---

# Fluxo de investigação de bugs

```
Bug encontrado

↓

git blame

↓

git log

↓

git show

↓

git bisect

↓

Encontrar commit responsável

↓

Corrigir

↓

git cherry-pick (se necessário)
```

---

# Boas práticas

✅ Utilize `git cherry-pick` para copiar apenas commits necessários.

✅ Aprenda `git bisect`; ele economiza horas de depuração.

✅ Execute `git gc` em repositórios muito grandes.

✅ Utilize aliases para acelerar o trabalho.

✅ Evite alterar arquivos dentro da pasta `.git`.

✅ Não utilize comandos de baixo nível sem entender seus efeitos.

---

# Resumo dos comandos

| Comando | Função |
|----------|---------|
| `git cherry-pick HASH` | Copia um commit específico |
| `git blame arquivo` | Mostra quem alterou cada linha |
| `git grep texto` | Pesquisa no projeto |
| `git bisect` | Localiza o commit que introduziu um bug |
| `git worktree add` | Trabalha com várias branches simultaneamente |
| `git archive` | Exporta o projeto sem a pasta `.git` |
| `git gc` | Otimiza o repositório |
| `git fsck` | Verifica a integridade do repositório |
| `git notes` | Adiciona anotações aos commits |
| `git describe` | Mostra a tag mais próxima |
| `git shortlog` | Estatísticas dos commits |
| `git rev-parse` | Informações sobre referências |
| `git show-branch` | Compara branches |
| `git ls-files` | Lista arquivos rastreados |
| `git cat-file` | Visualiza objetos internos |
| `git hash-object` | Calcula o hash de um arquivo |
| `git update-index` | Manipula a Staging Area |
| `git verify-commit` | Verifica assinatura de commits |
| `git verify-tag` | Verifica assinatura de tags |
| `git bundle` | Empacota um repositório completo |
| `git config --global alias` | Cria atalhos personalizados |
| `git maintenance run` | Executa manutenção do repositório |

---

# Conclusão

Os comandos avançados do Git são voltados para cenários específicos, como depuração, manutenção, auditoria e otimização de repositórios. Embora muitos deles não sejam utilizados diariamente, conhecer essas ferramentas pode economizar tempo, facilitar a investigação de problemas e demonstrar um domínio mais profundo do Git em ambientes profissionais.
