# Introdução a rede de computadores

## O que é Internet
Internet é um tipo de rede de computadores, é a mais conhecida e ela que interliga os dispositivos do mundo, a internet utiliza de vários dispositivos de hardware e protocolos para comunicação entre dispositivos, vamos ver o que cada componente da internet é

## Componentes da internet

* Hosts
    * Os hosts são os dispositivos que utilizamos, como celulares, computadores, televisões, relogios e etc. Eles também são chamados de end systems

* Communication links
    * Os communication links são realmente como os nomes dizem, links para comunicação, faz parte da camada mais baixa da internet. Exemplos são cabos coaxiais, fibra otica, espectros de radio.

* Packet switches
    * Os packet switches junto com os communication links fazem a comunicação de hosts. Os packet switches fazer a troca de um communication link de entrada para um communication link de saida, ou seja, eles pegam os dados que vieram de um link (link de entrada) e transmitem esses dados para outro switch ou host por outro link (link de saida). Os packet switches mais conhecidos são os routers e os link-layer switches

* Path ou Route
    * É chamado de Path o caminho que o dado faz de um host origem até um host destino, a sequência de  communication links e packet switches

* Internet Service Provider (ISPs)
    * Os hosts acessam a internet através dos ISPs, eles são compainhas de telefone, provedores de internet em aeroports, empresas, universidades...

* Protocols
    * Os hosts, packet switches e outras partes da rede se comunicam através de protocolos, que controlam a forma de mandar e receber dados na internet, exemplos de protocolos são Transmission Control Protocol TCP e Internet Protocol IP, que quando usados em conjuntos é muito conhecido como TCP/IP

## O que é um protocolo?
Protocolos são as "regras" de comunicação entre duas partes de uma conversa, no caso de redes entre dois dispositivos (não apenas hosts).  
Para entender um pouco melhor, nós usamos protocolos o tempo todo, primeiro que duas pessoas só conseguem se comunicar se eles souberem a mesma lingua, no caso de computadores, se eles conversam sobre o mesmo protocolo. Algumas outras regras também são formadas para uma boa conversação, como por exemplo, geralmente as conversas começam com um "Oi" e a resposta para isso é outro "Oi", depois disso cada pessoa geralmente fala uma por vez, para que não fique dificil entender o que o outro está falando. Procolos em redes seguem também essas regras, começa com uma apresentação de ambas as partes e após isso utilizam de palavras chaves para conseguirem se entender, sempre uma das partes se comunicando enquanto a outra escuta  
Um exemplo uma comunicação usando TCP é a seguinte:  
![Exemplo TCP](https://memoria.rnp.br/newsgen/9901/fig02a.gif)

### Packets
Na internet o dado é dividido em pedaços menores para serem transmitidos e quando esses dados se juntam com um header que contém informações sobre aqueles dados, esses dois juntos são chamados de pacotes, o que são transmitidos pela rede são pacotes.

## Internet sobre camadas
A Internet é dividida em camadas, cada camada tem seus protocolos e seus componentes, existem 7 camadas de redes, mas que podem ser resumidas em 5
* Camada de Aplicação
    * É onde ficam as aplicações e seus protocolos da camada de aplicação, como HTTP (protocolo muito usada para documentos Web), SMTP (protocolo para transmissão de e-mails). Seus pacotes são chamados de mensagens
* Camada de Transporte
    * É a camada responsavel pelo transporte das mensagens da camada de Aplicação entre os endpoints das aplicações, existem dois protocolos o TCP e o UDP. Seus pacotes são chamados de segmentos
* Camada de Rede
    * É a camada responsavel pelo transporte de pacotes, conhecidos como datagramas, da camada de rede entre hosts
* Camada de enlace
    * É a camada responsavel por mover os pacotes de um nó (host ou router) para outro, seus pacotes são referidos como frames
* Camada Fisica
    * É a camada mais "baixa" da internet é aonde estão a comunicação através dos communication links

## Encapsulamento

Encapsulamento é o que acontece quando um dado é passado por cada camada, esse dado ao ser passado para a proxima camada ele é "encapsulado", com o header necessários para que a camada funcione e após isso ele é entregue à proxima camada, esse ato de formar o pacote da camada é chamado de encapsulamento

## Desencapsulamento

Desencapsulamento é o ato inverso do encapsulamento, ao receber dado de uma camada, os headers dessa camada são retirados e o header que importa para a camada atual é lido.  

Um exemplo de encapsulamento e desencapsulamento é visto a seguir:  
![Exemplo encapsulamento](https://embeddedgeeks.com/wp-content/uploads/2020/06/encap-1.png)


**Referências**  
Livro James Kurose e Keith Ross, Computer networking a top down approach  
![Logo Tebas](https://github.com/rcrs4/Tebas/blob/novas-aulas/LogoIcon.png)

Feito por [Rafael Carneiro Reis de Souza](https://github.com/rcrs4)