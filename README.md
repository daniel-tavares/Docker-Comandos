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

### O que são os containers
        Container é o nome dado para a segregação de processos no mesmo kernel, de forma que o processo seja isolado o máximo possível de todo o resto do ambiente. Em termos práticos são File Systems, criados a partir de uma "imagem" e que podem possuir também algumas características próprias
        - Segregação de processos no mesmo kernel (isolamento)
        - Sistemas de arquivos criados a partir de uma imagem.
        - Ambientes leves e portateis no qual aplicações são executadas.
        - Encapsula todos apps e binarios necessários para a execução de um programa.
        - 


## O que é uma imagem Dockers?
Uma imagem Docker é a materialização de um modelo de um sistema de arquivos, modelo este
produzido através de um processo chamado build.

    - Modelo de sistema de aquivo para criar um container
    - Imagem é cradas a partir de um processo chamado build.
    - São armazenadas em repositórios no Registry
    - São compostas por uma ou mais camadas
    - Uma camada representa uma ou mais mudança no sistema de arquivo.
    - Uma camada é chamada também de imagem intermediária. A junção dessas camadas formam a imagem.
    - Apenas a ultima camada pode ser alterada quando o container for iniciado.
    - O AUFS(Advanced multi-layered Unification Filesystem) é muito utilizado. (O objetivo da divisão em camadas é o reuso)
    - É possivel compor imagens a partir de camadas de outras imagens. 

## Comparando MV e Docker   
   
   **Maquina vitual**
   
       - Kernel não compartilhado 
       - Biblioteca e binarios proprios
       - Requer uma quantidade de memória maior.
       - Um SO completo por maquina virtual.
       - Arquitetura: apps -> libs/bins -> Guests SO -> hypervisor -> Host OS -> Server.
    
   **Docker**
   
      - Kernel do SO compartilhado com os container
      - Usa biblioteca e binarios da máquina host.
      - Necessidade de memória muito menor.
      - Um SO para varios containers.
      - Arquitetura: apps -> libs/bins -> Container Engine -> Host OS -> Server.


# Arquitetura


 - **Docker Deamon/Server/Engine:** Interface que possui um conjunto de recursos (API, CLI, DOC) que auxiliam no gerenciamento dos containers.
          - CLI: Linha de comando para operar um container.
          - API REST: Outra forma de acesso aos recursos dos containers é através de apis.
          - KITEMATIC: Ferramenta grafica, uma alternativa para quem não gosta de linha de comando.

 - **DockerHost:**  SO que hospedarão os containers.
 
 - **Registry:** São repositórios de imagens na nuvem, como: DockHubs.



## COMANDOS DOCKER


### Criando um container

- **Comando: run**  
    - é a concatenação de quatro comandos: 
            - **docker container pull**  (baixa a imagem), 
            - **docker container create** (criação do container),
            - **docker container start** (inicialização do container), 
            - **docker container exec** (execução do container em modo interativo) 
    
    - Ele sempre cria um novo container
    
    - Atributos:
        - -i (modo iterativo)
        - -t (permitir acesso ao terminal)
        -  pode ser colocado como: -it ( permite o modo iterativo e permite acesso  ao terminal)
        - --rm (remove container)
        
     - Exemplos:
         - docker container run debian bash --version
         - sudo docker container ps -a   (exibe os container baixados)
         - docker container run --rm debian  bash --version (executar e remove um container)
         - docker container run -it debian bash  (criar um novo container e acessa o terminal de acesso ao container em modo iterativo)
         
         
### Colocando um nome para  
      Os containes possuem nomes unicos.
         
   - **docker container run --name mydeb -it debian bash:**  (cria e nomeia um container)  

### Exibindo lista de containers
    
   - **docker container ls** (lista todos os containers criados)
   - **docker container ps:** (exibe todos os containes ativos ou processos ativos)
   - **docker container ps -a:** (exibe os container baixados - ativos ou inativos)
   
   - **docker image ls:** lista todas as imagens ativas 
   - **docker volume ls:** lista todos os volumes ativas.
    
### Parar, reiniciar e iniciar container
   - **sudo docker container stop deamon-basic:** Para um container com nome deamon-basic
   - **sudo docker container restart deamon-basic:** Reinicia um container com nome deamon-basic
   - **sudo docker container start deamon-basic:** Inicia um container com nome deamon-basic
    
    * Também é possivel executar os comandos acima utilizando o ID ao invés do nome do container.
      
### Reutilizar um container
   
   - **sudo docker container start -ai mydeb**: acessa o console do container mydeb sem criar um novo container.
   
### Mapear portas dos containers

   - **sudo docker container run -p 8081:80 nginx :** comando que criar um container com servidor nginx mapeando a porta interna(80) do servidor para ser acessado externamente atraves da porta (8081)

### Mapear volumes(Diretorios)

   - **sudo docker container run -p 4201:80 -v $(pwd)/projeto:/usr/share/nginx/html nginx:** inicia container com servidor nginx e alterar o diretorio padrão (/usr/share/nginx/html) do servidor para um diretório específico (/projeto).
   
   * $(pwd): diretorio atual.
   
### Rodar um servidor em background (-d = deamon)

  - **sudo docker container run -d --name deamon-basic -p 8080:80 -v $(pwd)/projeto:/usr/shared/nginx/html nginx:** cria um container baseado em nginx e inicia o servidor internamente na porta 80 e expoe o servico externamente na porta 8080, roda o servidor em background (-d) e nomeia o container para deamon-basic.
  
  -  **sudo docker container logs deamon-basic:** comando para verificar o log de containers em background
  
  -  **sudo docker container inspect deamon-basic:** exibe em formato json diversas caracteristica do container.
  
  -  **sudo docker container exec deamon-basic uname -or:**  informa o tipo de sistema que esta sendo executado pelo container.
  

### Removendo imagens e container

-  **sudo docker rmi ID (sintaxe antiga):** remove uma imagem docker
-  **sudo docker image rm ID (sintaxe nova):** remove uma imagem docker
-  **sudo docker rm ID:** remove um container pelo ID


   
### HELP

- **sudo docker help:**  mostra os comandos para docker 
- **sudo docker image help**  mostra os comando para image
- **sudo docker volume help**  mostra o camando para volume.

### Comandos basicos para manipular imagens

- **docker image pull ID/TAG:** Baixa a imagem solicitada, este comando pode ser executado implicitamente, quando o docker
precisa de uma imagem para outra operação e não consegue localiza-la no cache local.
- **docker image ls:** Lista todas as imagens já baixadas, é possível ainda usar a sintaxe antiga: docker images
- **docker image rm ID_HASH/TAG:** Remove uma imagem do cache local, é possível ainda usar a sintaxe antiga: docker rmi ID/TAG - - **docker image inspect ID_HASH/TAG:** Extrai diversas informações utilizando um formato JSON da imagem indicada.
- **docker image ID_HASH/TAG <source> ID_HASH/TAG** Cria uma nova tag baseada em uma tag anterior ou hash.
- **docker image build -t ID_HASH/TAG:** Permite a criação de uma nova imagem
- **docker image push ID_HASH/TAG:** Permite o envio de uma imagem ou tag local para um registry.
      
### Construindo imagem com Dockerfile: Instruções de preparação.

      FROM:  Especifica a imagem base a ser utilizada pela nova imagem.
      
      LABEL: Especifica vários metadados para a imagem como o mantenedor. A especificação do mantenedor
      era feita usando a instrução específica, MAINTAINER que foi substituída pelo LABEL.
      
      ENV: Especifica variáveis de ambiente a serem utilizadas durante o build.
      
      ARG:  Define argumentos que poderão ser informados ao build através do parâmetro --build-arg.
    
      
      Exemplo de Arquivo Dockerfile sem extensão
         
            FROM debian 
            LABEL maintainer 'Daniel Tavares'

            ARG S3_BUCKET=files
            ENV S3_BUCKET=${S3_BUCKET}

      
- **docker image build -t build-exemplo .** : constroi uma imagem a partir do arquivo Dockerfile (-t define um nome para a imagem)
- **sudo docker container run build-exemplo bash -c 'echo $S3_BUCKET'** imprime a variavel descrita no Dockerfile
- **sudo docker image build --build-arg S3_BUCKET=myapp -t build-exemplo .** substitui o valor da variável S3_BUCKET do dockerfile


### BUILD DE DOCKERFILE: Instruções de povoamento.



## LINKS UTEIS
 
 - DOCKHUBS: https://hub.docker.com/
 - 
 
   
 
 
