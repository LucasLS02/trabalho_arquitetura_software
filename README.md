# O monolito

A plataforma da Twitch foi criada oficialmente em 6 de Junho de 2011, sendo um monolito desenvolvido utilizando Ruby on Rails. Essa arquitetura funcionou bem durante um tempo, porém ela foi posteriormente repensada, por problemas de perfomance. O chat, por exemplo, apresentava um grande problema para a Twitch, já que os servidores não conseguiam manter a comunicação de chat com qualidade em dias que possuiam eventos de jogos na plataforma.

## A transição para microsserviços

A ideia da nova arquitetura da Twitch era substituir o monolito por uma arquitetura baseada em microsserviços. Inicialmente, o foco era transformar o chat das lives em um microsserviço. Dentre as várias tecnologias estudadas para realizar essa mudança, Go foi a escolhida. Após testarem o chat e obterem bons resultados, outros times da Twitch tentaram utilizar o Go para outros serviços.

A linguagem foi experimentada, por exemplo, para listar as maiores livestreams para cada categoria na Twitch. Essa tecnologia foi apelidada de Jax, e apresentou uma série de desafios para seu desenvolvimento, como indexar dados em tempo real, tentando manter eles organizados.

# O monolito - Parte 2

## A migração em massa: Wexit

Em 2015, o Twitch iniciou uma campanha chamada "Wexit" para migrar seu código de back-end para microsserviços Go. A maioria do site ainda estava funcionando dentro de um monólito Rails, o que apresentava vários desafios para os desenvolvedores. Diversos esforços foram feitos para melhorar a situação, incluindo desacoplar o código dentro do monolito e adicionar um proxy reverso NGINX para redirecionar o tráfego para uma nova borda da API escrita em Go.

O processo de migração consistiu em desenvolver o novo microsserviço, replicar o endpoint antigo na nova borda, atualizar a configuração do NGINX para redirecionar parte do tráfego para o novo endpoint e, gradualmente, aumentar o tráfego até atingir 100%. Essa abordagem permitiu que as equipes desenvolvessem novas funcionalidades, tornando o monolito obsoleto ao longo do tempo.

Durante a campanha, os desenvolvedores tiveram que lidar com uma mudança significativa na cadeia de ferramentas, escrevendo código em vários repositórios com ciclos de implantação diferentes. Eles também tiveram que aprender a provisionar recursos na nuvem (AWS) usando a linguagem de programação Go. Chamadas para módulos dentro do monolito eram simples, mas chamar outros serviços exigia considerações adicionais, como tratamento de erros, monitoramento, limitação de taxa, segurança, testes de integração e muito mais.

Apesar do caos inicial, algumas estruturas úteis surgiram como resultado desse processo. Alguns desses frameworks se tornaram populares dentro da empresa e também projetos de código aberto, como o Twirp.

## Impacto Organizacional

O crescimento rápido de empresas como a Twitch requer mudanças rápidas na estrutura organizacional, o que adiciona dificuldades às migrações em andamento. A estrutura de comunicação das organizações tende a refletir em seus serviços, o que pode resultar em pontos cegos se os desenvolvedores se concentrarem apenas em suas áreas de responsabilidade.

Um exemplo disso ocorreu em 2017, quando uma nova versão do aplicativo móvel Twitch causou uma sobrecarga nos servidores da API. O problema foi causado por um novo comportamento de repetição no aplicativo móvel que resultou em uma grande quantidade de solicitações à API. As equipes responsáveis pelo aplicativo móvel e pela API realizaram testes, mas ninguém estava encarregado de verificar se as duas partes funcionavam bem juntas.

## A Cauda Longa

Durante a migração do Twitch, a regra de Pareto foi aplicada, onde os últimos 20% do trabalho exigiram 80% do tempo. Os endpoints mais difíceis de migrar foram deixados para o final. Para lidar com isso, um grupo interno foi formado para monitorar e migrar esses últimos serviços.

Alguns dos endpoints restantes ainda recebiam tráfego de fontes desconhecidas, como bots ou scripts, e não era claro qual era a função desses endpoints. A única maneira de determinar se era seguro desativá-los era forçar 10 minutos de inatividade e verificar se alguém relatava problemas.

No final de 2018, todo o tráfego foi removido do monólito e todas as instâncias do EC2 na conta principal da AWS puderam ser encerradas. No entanto, ainda era necessário mais um ano para limpar completamente a conta de dependências e funções de acesso, o que foi feito por meio de auditorias de segurança e atualizações tecnológicas em toda a empresa. Para todos os efeitos, a campanha "Wexit" foi concluída. Houve uma celebração com troféus para todos do grupo de trabalho e uma festa para comemorar o sucesso da migração.

## Microsserviços Hoje

Atualmente, no Twitch, a maioria das equipes trabalha com vários microsserviços. A linguagem preferida para o código do servidor é o Go, embora outras linguagens, como TypeScript, Python, C++, Java/Kotlin e ObjectiveC/Swift, também sejam usadas em outras plataformas. Cada serviço é isolado em uma conta separada da AWS, seguindo o padrão chamado de "Tiny Bubbles".

As equipes de produtos operam de forma independente, gerenciando sua própria infraestrutura e ajustando seus serviços conforme necessário. Equipes centrais fornecem estruturas e ferramentas específicas para padronizar a pilha de engenharia e as práticas operacionais. Embora ainda ocorram migrações de código à medida que novas tecnologias se tornam disponíveis, a natureza distribuída dos microsserviços permite que as equipes contribuam em escala.

# Fontes
https://blog.twitch.tv/en/2022/03/30/breaking-the-monolith-at-twitch/
https://blog.twitch.tv/en/2022/04/12/breaking-the-monolith-at-twitch-part-2/
