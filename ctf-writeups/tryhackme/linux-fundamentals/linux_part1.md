# Linux Fundamentals Part 1

![Categoria](https://img.shields.io/badge/categoria-linux-yellow?style=flat-square)
![Dificuldade](https://img.shields.io/badge/dificuldade-info-lightgrey?style=flat-square)
![Plataforma](https://img.shields.io/badge/TryHackMe-free-red?style=flat-square&logo=tryhackme&logoColor=white)
![Tempo](https://img.shields.io/badge/tempo-7min-blue?style=flat-square)

## Objetivo

Aprender os fundamentos do Linux — o sistema operativo usado na grande maioria
dos servidores e ferramentas de cibersegurança, incluindo o Kali Linux que vou
usar no home lab.

## Tarefas Completadas

### Task 1 & 2 — Introdução e Background
O Linux é um sistema operativo open source criado em 1991 por Linus Torvalds.
Existem muitas distribuições (distros) baseadas em Linux — Ubuntu, Debian, Kali, etc.
É o sistema mais usado em servidores, dispositivos IoT e ferramentas de segurança.

### Task 3 — Primeira Máquina Linux no Browser
O TryHackMe permite correr uma máquina Linux diretamente no browser sem instalar nada.
Isto é possível através de uma VM remota acessível via interface web.

### Task 4 — Primeiros Comandos

| Comando | Função |
|---|---|
| `echo` | Imprime texto no terminal |
| `whoami` | Mostra o utilizador atual |

Exemplos:
```bash
echo "Hello World"   # imprime Hello World
whoami               # mostra o nome do utilizador atual
```

### Task 5 — Sistema de Ficheiros

| Comando | Função |
|---|---|
| `ls` | Lista ficheiros e pastas |
| `cd` | Muda de diretório |
| `pwd` | Mostra o caminho atual |
| `cat` | Mostra o conteúdo de um ficheiro |

Exemplos:
```bash
ls                  # lista o conteúdo da pasta atual
ls -la              # lista com detalhes e ficheiros ocultos
cd /home            # navega para a pasta /home
cd ..               # volta uma pasta atrás
pwd                 # mostra onde estás ex: /home/user
cat ficheiro.txt    # mostra o conteúdo do ficheiro
```

### Task 6 — Pesquisa de Ficheiros

| Comando | Função |
|---|---|
| `find` | Procura ficheiros no sistema |
| `grep` | Procura texto dentro de ficheiros |

Exemplos:
```bash
find /home -name "passwords.txt"   # procura ficheiro pelo nome
grep "password" ficheiro.txt       # procura a palavra "password" no ficheiro
```

### Task 7 — Shell Operators

| Operador | Função |
|---|---|
| `&` | Corre comando em background |
| `&&` | Corre segundo comando só se o primeiro tiver sucesso |
| `>` | Redireciona output para ficheiro (substitui) |
| `>>` | Redireciona output para ficheiro (acrescenta) |

Exemplos:
```bash
echo "texto" > ficheiro.txt    # cria/substitui ficheiro com "texto"
echo "mais" >> ficheiro.txt    # acrescenta "mais" ao ficheiro
comando1 && comando2           # corre comando2 só se comando1 funcionar
```

## O que Ficou em Memória

O `grep` e o `find` são os comandos que mais vou usar em cibersegurança —
procurar ficheiros e texto dentro de ficheiros é essencial tanto em pentest
como em análise forense. O operador `>>` é útil para guardar resultados
de scans sem perder o que já estava no ficheiro.

## Ligação ao Home Lab

Todos estes comandos vão ser usados diariamente no Kali Linux.
O `find` e `grep` são especialmente importantes para procurar
ficheiros de configuração e passwords em máquinas comprometidas.
