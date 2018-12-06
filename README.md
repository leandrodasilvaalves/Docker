# Alguns comandos Docker

Instalar docker
```
curl -sSL https://get.docker.com | sh
```

Iniciar o docker
```
/etc/init.d/docker start
```

Listar containers rodando
```
docker container ls 
```

Listar imagens baixadas
```
docker image ls
```

Criar container utilizando ubuntu, inciando o processo "/bin/bash". Se a imagem não existir na máquina local ele irá baixar direto do repositório do docker.
```
docker run -i -t ubuntu:14.10 /bin/bash
```

Sair do container, mas deixando-o ativo
```
Ctrl+p+q
```

Volta para o container selecionado
```
docker attach <containerId>
```

Ver as alterações (arquivos criados, modificados, deletados) realizadas no container
```
docker diff <containerId>
```

Faz logout e mata a instância do container
```
Ctrl+d
```

Criar um container a partir da imagem previamente baixada
```
docker run -i -t -p 8080:80 ubuntu:14.10 /bin/bash
```

É importante passar a versão para que o docker organize os meu containers conforme o modificações e novos commits
```
docker commit <containerId> <nomedaImagem>(badtux/nginx-ubuntu:1.0)
```

```
docker run -i -t -p 6660:80 nomedaimagem(badtux/nginx-ubuntu:1.0) /bin/bash
```

Finalizar um container
```
docker stop <containerId>
```

Dá pra ver uma lista de processos do container em formato json
```
docker inspect <containerId>
```

Rodar container em background mapeando para uma pasta do host
```
docker container run -d --name ex-daemon-basic -p 8080:80 -v $(pwd)/html:/usr/share/nginx/html nginx
```

Ver processos como consumo de cpu e memória
```
docker stats <containerId>
```

Para executar um comando dentro do container
```
docker exec <containerId> <comando> (ps -ef)
```


EXEMPLO BASICO DE dockerfile
```
FROM nginx-ubuntu:1.0
MAINTAINER leandro.silva.alves@gmail.com
RUN apt-get update && apt-get install -y apache2 && apt-get clean
```


Criar imagem a partir do dockerfile, lembrando que o só pode haver um dockerfile por diretório.
```
docker build -t apache-nginx-ubuntu:1.0 .
```

O camando entre aspas lista somente a primeira coluna de todos os container. Em conjunto com 'docker rm' esse comando remove todos os containers.
```
    docker rm `docker ps -a -q`
```

Criar container limitando o uso de memória
```
docker run -ti -m 512M debian /bin/bash
```

Verificar o uso de memoria do container
```
docker inspect <containerId> | grep -i mem
```

Atualizar o limite de memoria de um container em excecução.
```
docker update -m 256M <containerId>
```

Limitar o uso do cpu. No exemplo do video ele criou 3 containers, sendo o primeiro com 1024 e os demais com 512. O primeiro pode acessar até 50% do cpu e os outros podem acessar até 25% do cpu
```
docker run -ti --cpu-shares 512 debian /bin/bash
```

Verificar o uso do cpu.
```
docker inspect <containerId> | grep -i cpu 
```

Atualizar o limite de cpu de um container em excecução.
```
docker update --cpu-shares 512 <containerId>
```

Fazer build de uma imagem a partir do Dockerfile e passando parâmetros
```
docker image build --build-arg S3_BUCKET=myapp -t ex-build-arg .
```

Criar container a partir de imagem com argumentos.
```
docker container run ex-build-arg bash -c 'echo $S3_BUCKET'
```

filtrar inspect
```
docker image inspect --format="{{index .Config.Labels \"maintainer\"}}" ex-build-arg
```

# Comandos auxiliares Linux

terminal como root:
```
sudo su 
```

Instalar as ferramentas netstat
```
apt-get install net-tools
```

Ver se o docker está rodando
```
ps -ef | grep docker 
```

Mostra dados do linux, no caso, dados do container
```
uname -a
```

Para mostrar que está realmente no ubuntu (container)
```
cat /etc/issue
```

mostra processos executados pelo container
```
ps -ef
```

Instalar e iniciar o nginx no container
```
apt-get install nginx

/etc/init.d/nginx start 
```

Mostra portas escutando no container
```
netstat -atunp
```

Mostra os logs de acesso do nginx
```
tail -f /var/log/nginx/access.log
```
Instalar ping
```
apt-get install iputils-ping
```

Quantidade de memória do host
```
free -m
```























































