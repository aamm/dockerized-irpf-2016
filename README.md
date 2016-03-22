# dockerized-irpf-2016
Dockerized Brazilian income tax declaration app

Primeiro faça o build da imagem:

    docker build -t aaakiraaa/dockerized-irpf-2016 .

A seguir execute o seguinte script localmente (arquivo *dockerized-irpf-2016* no repositorio GIT):

    #!/usr/bin/env bash
    
    xhost local:
    [ ! -d $HOME/irpf-2016-shared ] && mkdir $HOME/irpf-2016-shared
    if [ "$(docker ps -a | grep irpf-2016 | wc -l)" == "1" ]; then
        docker start irpf-2016
    else
        docker run -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix/:rw \
            -v /dev/snd:/dev/snd \
            -v $HOME/irpf-2016-shared:/root/shared:rw \
            --name irpf-2016 \
            aaakiraaa/dockerized-irpf-2016 /bin/irpf-2016
    fi

Infelizmente não é possível automatizar a instalação do programa de declaração de imposto de renda. Então a primeira execução do container pedirá que você para você instalar o programa da declaração do imposto de renda e a seguir o ReceitaNet. Simplesmente deixe toda as opções **com o valor default** e termine a instalação clicando em "Avançar".

As execuções seguintes deste container não vão mais pedir a instalação do programa.

A imagem no Docker Hub esta hospedada aqui: https://hub.docker.com/r/aaakiraaa/dockerized-irpf-2016/
