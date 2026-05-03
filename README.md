[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/TPGyf4AW)
This is a simple example to demonstrate how stubs can be used as remote references in RPC systems. The example was extracted from (Tanenbaum and van Steen, 2025).

## Arquitetura

O sistema é distribuído em três máquinas (AWS EC2):

* EC2 1: Servidor (`server_main.py`)
* EC2 2: Cliente 1 (`client1_main.py`)
* EC2 3: Cliente 2 (`client2_main.py`)

---

## Funcionamento

1. O Cliente 1:

   * Cria uma lista no servidor
   * Adiciona um valor
   * Envia o stub (`DBClient`) para o Cliente 2

2. O Cliente 2:

   * Recebe o stub
   * Usa o stub para acessar a mesma lista remota
   * Adiciona outro valor
   * Recupera e imprime a lista final

3. O Servidor:

   * Processa requisições (`CREATE`, `APPEND`, `GETVALUE`)
   * Mantém o estado das listas

---

## Estrutura dos Arquivos

* `server.py`: lógica do servidor
* `client.py`: comunicação entre clientes
* `dbclient.py`: implementação do stub (referência remota)
* `constRPC.py`: constantes e configuração de rede
* `server_main.py`: inicializa o servidor
* `client1_main.py`: executa cliente 1
* `client2_main.py`: executa cliente 2

---

## Execução

```bash
python3 server_main.py
```
|
```bash
python3 client2_main.py
```
|
```bash
python3 client1_main.py
```

---

## Resultado

No Cliente 2:

```
Client2 esperando dados...
Lista final: ['Client 1', 'Client 2']
```
