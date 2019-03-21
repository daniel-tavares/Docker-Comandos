# Docker-Comandos

## CONCEITOS

### O que é docker ?
   - É uma engine de administração de container. 
   - É uma tecnologia de virtualização, porém, não é um sistema de virtualização tradicional (baseado em máquinas virtuais)
   - É um sistema de virtualização baseado em Software (Kernel host compartilhado com os container).
   - É baseado em uma tecnologia chamada de LXC (Linux Containers), ou seja, é necessário uma tecnologia unix para rodar os containers.
   - É uma tecnologia de linguagem aberta (Open source).
   - Desenvolvida na linguagem GO.
   - Empacota o software com vários níveis de isolamento (quantidade de: memória, CPU, rede, etc.).
   
## Comparando MV e Docker   
   Maquina vitual
    - Kernel não compartilhado 
    - Biblioteca e binarios proprios
    - Requer uma quantidade de memória maior.
    - Um SO completo por maquina virtual.
    - Arquitetura: apps -> libs/bins -> Guests SO -> hypervisor -> Host OS -> Server.
    
   Docker
   - Kernel do SO compartilhado com os container
   - Usa biblioteca e binarios da máquina host.
   - Necessidade de memória muito menor.
   - Um SO para varios containers.
   - Arquitetura: apps -> libs/bins -> Container Engine -> Host OS -> Server.


- **DockerHost:** Maquina ou SO que hospedarão os containers.
- **DockerEngine:** Possui um conjunto de recursos (API, CLI, DOC) que auxiliam no gerenciamento dos containers
- ****

## INSTALAÇÃO DO DOCKER
   -  


## BAIXANDO E EXECUTANDO UM CONTAINER

- **run**  
    - é a concatenação de quatro comandos: **docker container pull**  (baixa a imagem), **docker container create** (criação do container),
    **docker container start** (inicialização do conatiner), **docker container exec** (execução do container em modo interativo) 
    - Ele sempre cria um novo container
    - Atributos:
        - -i (modo iterativo)
        - -t (permitir acesso ao terminal)
        -  pode ser colocado como: -it
        
    
 -  docker container run hello-world
 -  docker container run debian bash --version
 -  sudo docker container ps -a   (exibe os container baixados)
 -  docker container run --rm debian  bash --version (executar e remove um container)
 -  docker container run -it debian bash  (carregar um novo container debian e exibe o terminal de acesso ao container)
 
 ## COLOCANDO NOME PARA O CONTAINER
   
 
 
