---

# Roteiro de hoje

1. [Finalizar o jogo](#edukids-animals) **EduKids Animals** <!-- {.righteous} -->
1. [Transformações](#transformacoes)
1. [Transições](#transicoes)
1. [Animações](#animacoes)

---
<!--
{
  "layout": "section-header",
  "hash": "edukids-animals"
}
-->
# EduKids Animals <!-- {.righteous} -->
## Jogo para irmã(o)zinh@s

![Desenho de um urso](../../images/urso.jpg) <!-- {.portrait.centered style="box-shadow: 0 0 10px 5px rgba(0, 0, 0, 0.34);"} -->

---
<!-- {"layout": "2-column-content"} -->
## Motivação

> Seus pais vão viajar e você deve cuidar do seu mini irmãozinho de 3 anos.
>
> Com um comportamento de anjinho (#sqn), o pequeno Joãozinho vai dar trabalho.
>
> Você, como um ótimo irmã(ão) e programador(a)
> exímio, decide que é hora de criar um jogo Web para, além de entreter seu
> mini-irmão, ensiná-lo como falar o nome de alguns animais.

![](../../images/edukids.png) <!-- {.full-width.bordered.rounded} -->

---
## O jogo **Edukids Animals** <!-- {.righteous} -->

- Funcionamento do jogo:
  - Assim que apertar **play**, o jogo começa
  - A cada ...2s, um animal é sorteado e começa a ficar com fome
  - Você deve clicar no animal agitado para alimentá-lo antes que ele coma
    alguém
    - Fazendo isso, ganha-se 1 ponto
  - Se um animal não é clicado a tempo, perde-se 2 pontos
  - Se um animal que estava sossegado é perturbado fora de hora, perde-se 1
    ponto
- Essa funcionalidade **já está implementada** em um arquivo JavaScript

---
## O que está **faltando**

1. O jogo ainda não dá um _feedback_ visual interessante para o jogador
   - Apenas o nome do animal aparece escrito e seu irmão ainda não sabe ler
1. O arquivo `jogo.js` controla o jogo. Ele tem um temporizador que
   fica **adicionando e removendo classes dos elementos** dos animais
   
   `com-fome`
   ... quando o animal está com fome
   
   `satisfeito`
   ... quando o animal acabou de comer
   
   `com-raiva`
   ... quando um animal sossegado é perturbado
   
   `atacando`
   ... quando um animal com fome não é alimentado a tempo

---
## Pede-se: fazer os **2 exercícios** abaixo

1. Criar uma **transição para quando o mouse estiver em cima dos botões**
   _play/stop_ (para que o elemento se revele lentamente)
1. Você deve implementar uma **metáfora visual** para cada um dos 4 estados dos
   animais. Algumas sugestões:
   1. `com-fome`, animal piscando (opacidade variando)
   1. `satisfeito`, uma borda verde no animal e o animal fica girando de alegria
   1. `com-raiva`, animal vai crescendo, ou fica pulsando
   1. `atacando`, animal dá um salto e cresce, com uma borda vermelha

---
