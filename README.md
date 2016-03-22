# dockerized-irpf-2016
Dockerized Brazilian income tax declaration app

Primeiro faça o build da imagem:

    docker build -t irpf-2016 .

A seguir execute o seguinte script localmente:

    #!/usr/bin/env bash
    
    xhost local:
    docker run -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix/:rw \
        -v /dev/snd:/dev/snd \
        irpf-2016 /bin/irpf-2016

Infelizmente não é possível automatizar a instalação do programa de declaração de imposto de renda. Então a primeira execução do container pedirá que você para você instalar o programa da declaração do imposto de renda e a seguir o ReceitaNet. Simplesmente deixe toda as opções **com o valor default** e termine a instalação clicando em "Avançar".

As execuções seguintes deste container não vão mais pedir a instalação do programa.
