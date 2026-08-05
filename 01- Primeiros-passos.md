# Primeiros Passos

# git init

Inicializa um repositório Git na pasta atual.

```bash
git init
```

Resultado:

```
Initialized empty Git repository
```

---

# git clone

Clona um repositório remoto.

```bash
git clone https://github.com/usuario/repositorio.git
```

Também é possível escolher o nome da pasta.

```bash
git clone https://github.com/usuario/repositorio.git meu-projeto
```

---

# git status

Mostra o estado atual do repositório.

```bash
git status
```

Exibe:

- arquivos modificados
- arquivos novos
- arquivos rastreados
- arquivos não rastreados

É provavelmente o comando mais utilizado do Git.

---

# git add

Adiciona arquivos para staging.

Adicionar um arquivo:

```bash
git add arquivo.txt
```

Adicionar tudo:

```bash
git add .
```

Adicionar apenas arquivos modificados:

```bash
git add -u
```

Adicionar de forma interativa:

```bash
git add -p
```

---

# git commit

Salva as alterações.

```bash
git commit -m "Criando tela de login"
```

Editar última mensagem:

```bash
git commit --amend
```

Adicionar arquivos e commitar:

```bash
git commit -am "Mensagem"
```
