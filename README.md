# O monolito

A plataforma da Twitch foi criada oficialmente em 6 de Junho de 2011, sendo um monolito desenvolvido utilizando Ruby on Rails. Essa arquitetura funcionou bem durante um tempo, porém ela foi posteriormente repensada, por problemas de perfomance. O chat, por exemplo, apresentava um grande problema para a Twitch, já que os servidores não conseguiam manter a comunicação de chat com qualidade em dias que possuiam eventos de jogos na plataforma.

# A transição para microsserviços

A ideia da nova arquitetura da Twitch era substituir o monolito por uma arquitetura baseada em microsserviços. Inicialmente, o foco era transformar o chat das lives em um microsserviço. Dentre as várias tecnologias estudadas para realizar essa mudança, Go foi a escolhida. Após testarem o chat e obterem bons resultados, outros times da Twitch tentaram utilizar o Go para outros serviços.

A linguagem foi experimentada, por exemplo, para listar as maiores livestreams para cada categoria na Twitch. Essa tecnologia foi apelidada de Jax, e apresentou uma série de desafios para seu desenvolvimento, como indexar dados em tempo real, tentando manter eles organizados.
