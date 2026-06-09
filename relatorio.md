# Relatório — Atividade Prática: Sockets TCP

**Disciplina:** Sistemas Distribuídos
**Dupla:** André Filipe Martins / Davi Roberge Machado
**Data:** 09/06/2026

---

## Nível 1 — Inspecionar o código

### 1.1 Servidor (`servidor.py`)

Descreva com suas palavras o que cada chamada abaixo faz e por que ela
é necessária:

| Chamada | O que ela faz? |
|---------|---------------|
| `socket.socket(AF_INET, SOCK_STREAM)` | `Cria um socket TCP, AF_INET sendo relativo ao IPv4 e SOCK_STREAM ao TCP` |
| `servidor_socket.bind((HOST, PORTA))` | `Associa o socket ao endereço IP e porta especificados` |
| `servidor_socket.listen(5)` | `Coloca o socket em modo de escuta, aceitando até 5 conexões na fila` |
| `servidor_socket.accept()` | `Aguarda e aceita uma conexão de cliente` |
| `conn.recv(TAMANHO_BUFFER)` | `Recebe os dados do cliente` |
| `conn.sendall(resposta.encode("utf-8"))` | `Envia a resposta para o cliente (eco)` |
| `conn.close()` | `Encerra a conexão com o cliente` |

### 1.2 Cliente (`cliente.py`)

| Chamada | O que ela faz? |
|---------|---------------|
| `socket.socket(AF_INET, SOCK_STREAM)` | `Cria um socket TCP, AF_INET sendo relativo ao IPv4 e SOCK_STREAM ao TCP` |
| `cliente_socket.connect((HOST_SERVIDOR, PORTA_SERVIDOR))` | `Conecta ao servidor pelo hostname e porta` |
| `cliente_socket.sendall(mensagem.encode("utf-8"))` | `Envia a mensagem codificada em bytes (UTF-8) ao servidor` |
| `cliente_socket.recv(TAMANHO_BUFFER)` | `Aguarda e recebe o eco do servidor` |

### 1.3 Rede e contêineres

Por que o cliente usa o hostname `"servidor"` em vez de `"localhost"`
para se conectar? O que aconteceria se usasse `"localhost"`?

> _Resposta: O nome "servidor" é o hostname definido no docker-compose.yml, o Docker resolve esse nome diretamente para o IP interno do contêiner. Se fosse usado "localhost", o cliente tentaria se conectar ao próprio ao contêiner cliente, que não possui o serviço de servidor._

---

## Nível 2 — Modificar o servidor

Descreva as mudanças que você fez no `servidor.py` para:

1. Devolver a mensagem **em maiúsculas**:

   > _O que foi alterado e por quê: A variável "reposta", que antes recebeia apenas "mensagem" diretamente, agora recebe a versão em maiúsculas da mensagem, usando o método upper() para isso. Dessa maneira, apenas a resposta enviada ao cliente é convertida em maiúsculas._

2. Exibir no log o **contador de mensagens recebidas** acumulado:

   > _O que foi alterado e por quê: Existia uma variável global "total_mensagens", inicializada com 0. Ela agora é incrementada em 1 sempre que uma mensagem é recebida. Cada vez que ela é incrementada, uma mensagem de log é exibida._

Após a modificação, você precisou rodar `docker compose up --build`.
Por que o `--build` é necessário aqui?

> _Resposta: O build é necessário para que o Docker compile o código Python dentro do contêiner e crie uma nova imagem com as modificações. Como o arquivo foi alterado, o Docker precisa reconstruir a imagem para que as mudanças tenham efeito._

---

## Observações livres

Anote aqui qualquer comportamento inesperado que observaram, erros que
apareceram e como resolveram, ou dúvidas que ainda têm:

> Não tenho nenhuma observação.

---

## Dúvida para a próxima aula

Escreva **uma pergunta** que surgiu durante a atividade e que vocês
gostariam de ver respondida na aula seguinte:

> Não tenho nenhuma dúvida.
