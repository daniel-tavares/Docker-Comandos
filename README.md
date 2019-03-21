# Docker-Comandos

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
   
 
 
