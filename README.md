# Domine Apache Kafka
Acompanhamento prático do curso ["Domine Apache Kafka, Fundamentos e Aplicações Reais [2022]"](https://www.udemy.com/course/aprenda-apache-kafka/) na [Udemy](https://www.udemy.com/)
 
## Contexto
Esse treinamento foca na instalação e execução da ferramenta em uma `VM Linux` rodando no `Virtualbox`, o que pode ser problemático em instalações sem a ferramenta.

A proposta foi adaptar o exercício usando `docker` no lugar e levando em conta recentes problemas com as imagens `docker` da `confluent`.

## Comandos úteis
Para iniciar o cluster com o `Jupyter Lab`, com o [`docker`](https://docs.docker.com/get-started/) e o [`docker-compose`](https://docs.docker.com/compose/gettingstarted/) instalado, faça o seguinte:

### Comandos Iniciais

Faça um fork do repositório, clone este repositório e abra a pasta que foi criada

```console
$ git clone git@github.com:<GH_USERNAME>/aprenda-apache-kafka.git
$ cd aprenda-apache-kafka/
```

Execute o `docker-compose`:

```console
$ docker-compose up -d
```

Caso tenha o `Visual Studio Code` instalado:

```console
$ code .
```

Para usar a plataforma `Jupyter`, abra os logs do servidor e copie a URL no final do log:

```console
$ docker logs $(basename $PWD)-jupyter-1
```

```console
[C 2022-06-20 18:36:52.730 ServerApp] 
    
    To access the server, open this file in a browser:
        file:///home/jovyan/.local/share/jupyter/runtime/jpserver-8-open.html
    Or copy and paste one of these URLs:
        http://05bb7e4861b4:8888/lab?token=53d752a5f1e1633a7bf4a31a3999068318e7e7db8873af13
     or http://127.0.0.1:8888/lab?token=53d752a5f1e1633a7bf4a31a3999068318e7e7db8873af13
```

As alterações feitas na pasta notebooks serão gravadas diretamente na sua pasta de fontes para versionamento.

### Interagindo com o Kafka

Para executar comandos do kafka, faça da seguinte forma:

```console
$ docker exec -it $(basename $PWD)-kafka-1 kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic mensagens --group consumidores
```

ou

```console
$ docker exec -it $(basename $PWD)-kafka-1 kafka-topics.sh --bootstrap-server 127.0.0.1:9092 --list
```

ou

```console
$ docker exec -it $(basename $PWD)-kafka-1 kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --list
```

ou

```console
$ docker exec -it $(basename $PWD)-kafka-1 kafka-console-producer.sh --broker-list kafka:9092 --topic mensagens
```

Os exemplos acima são baseados no curso, usando os hosts do cluster

### Encerrando o Lab

Execute o seguinte comando para desligar os serviços e reduzir o consumo da sua máquina:

```console
$ docker-compose down
$ docker system prune
```

Um prompt será mostrado

```console
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images
  - all dangling build cache

Are you sure you want to continue? [y/N] 
```

Digite `y` e `<enter>`

```console
Deleted Containers:
077b2d307d758cc82a3415c80197a9d4a52d65f165917673e6822459ab1c77b2
d7e05d5bd30121a33663f1536f62ee3981b77a1e3f377b7f90fd21878c779741
b6f32bddf7fb4730bfac6f6ba8d7d5f7a310ad0ac5c4f2cb2ff777cda3df8740
1b1f87bf1b5961d591efac57e6c44d9a6de6af6f8e4d4da1b9d4655d1b414dfc

Deleted build cache objects:
vp26llxcmap78tow3fkgy4vkc
3c4wq50vo12pxh7cxwl244kx3
dnjoiycjt6esc6sifvxop97b4
p5f9pt1acqficbn8ncgjn8f3k
iieocgduqdmmoygohurekot6q
dho0x813t7laaxjutzq3c8cqh
thyst0vpa1r1g9in2eihsdfl2
33cfw8qekjj11q0d93f6fnk8y
kxx403g6yzvma2iqpl9mq2p15
ikbkoy89vomrzfyz4ncrcp636
ltns71o5k9o7zhtq4leql5dse
uq2ruid29g6nicugcofue57ct
sle3nu6vw9pok9pw8y9nuhmg8
ngsuen8yrnd9sviqrteex3pbw

Total reclaimed space: 239.3MB
```

## Saiba mais

* https://jupyter-docker-stacks.readthedocs.io/en/latest/index.html
* https://hub.docker.com/r/jupyter/scipy-notebook
