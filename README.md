# Controle PLC de Misturador Químico em Batelada

Este projeto implementa a lógica de controle PLC para um misturador químico em batelada no **Velocio Flow Builder**.

A lógica foi criada e validada em ambiente offline, sem programação em hardware físico. A execução real em PLC e a integração com **VFactory/HMI** exigem um PLC Velocio conectado ao computador via USB.

O controle utiliza uma máquina de estados com temporizador para comandar bombas de entrada, mixer, bomba de saída e pausa do processo pelo `RunProcess`.

## Objetivo

Controlar automaticamente a sequência de adição e mistura de três produtos químicos genéricos:

* Chemical 1
* Chemical 2
* Chemical 3

Cada produto químico é representado por uma bomba de entrada no PLC.

## Sequência de Funcionamento

* `State 0`: inicializa o sistema, desliga todas as saídas, zera o `Timer` e avança para `State 1`
* `State 1`: liga `RunIntakePump1` até `Timer > 2`
* `State 2`: liga `RunMixer`, `RunIntakePump2` e `RunIntakePump3` até `Timer > 4`
* `State 3`: mantém `RunIntakePump3` ativo até `Timer > 6`
* `State 4`: mantém `RunMixer` ativo até `Timer > 10`
* `State 5`: liga `RunOuttakePump` até `Timer > 15` e retorna para `State 0`

## Tags Principais

* `RunProcess`
* `State`
* `Timer`
* `RunIntakePump1`
* `RunIntakePump2`
* `RunIntakePump3`
* `RunMixer`
* `RunOuttakePump`
* `EmergencyFlush`

## Arquivos do Projeto

* `PLC Programming.viof`: arquivo principal do fluxo no Velocio Flow Builder
* `PLC Programming.vio`: configuração do projeto/I/O

## Hardware

O projeto foi configurado manualmente com o perfil **Velocio Ace 11**.

Para gravar o programa em um PLC físico, é necessário conectar o equipamento Velocio ao computador via USB. Sem o hardware, o projeto pode ser criado, editado, salvo e verificado, mas não pode ser enviado ao PLC real.

## Integração com HMI

A integração com **VFactory/HMI** depende da comunicação com o PLC físico. Sem o PLC conectado, é possível criar o layout visual da HMI, mas não é possível testar a comunicação em tempo real com as tags do controlador.

## Status

Lógica montada e validada no Velocio Flow Builder com **0 erros** e **0 avisos**.
