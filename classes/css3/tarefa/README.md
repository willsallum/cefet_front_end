<!-- {"layout": "section-header", "hash": "unicornios"} -->
## Comp / Specs

[![](../../images/unicorns-comp-lpw.png)](../../images/unicorns-comp-lpw.png) <!-- {.bordered style="max-width: 35%"} --> <!-- {a:target="_blank"} -->
[![](../../images/unicorns-specs-lpw.png)](../../images/unicorns-specs-lpw.png) <!-- {.bordered style="max-width: 35%"} --> <!-- {a:target="_blank"} -->

*[Comp]: Comprehensive Layout*
*[Specs]: Specifications*

<!-- {p:.center-aligned} -->

---
<!-- {"hash": "quebra-de-linha"} -->
# Quebra de linha (tag `<br>`)

- A _tag_ `<br>` funciona para quebrarmos linha em um parágrafo
  - `<br>` vem de _break line_
- Utilize-a para **quebrar linhas**, porém, **não** para separar parágrafos
  ou outros elementos
- Exemplo: escrevendo um poema

<iframe width="400" height="460" src="https://jsfiddle.net/fegemo/5xfek8yq/embedded/html,result" allowfullscreen="allowfullscreen" frameborder="0" class="rounded bordered flex-align-center"></iframe>


---
<!-- {"embeddedStyles": ".box-model-part {color: #333; border-radius: 4px; font-style: normal; padding: 1px 3px; } .box-model-part code { background: initial; }", "backdrop": "oldtimes", "hash": "box-model"} -->
## _Box Model_ ([na MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/box_model))

- ![](../../images/box-model.png) <!-- {.push-right} -->
  O navegador enxerga todo elemento de conteúdo como uma "caixa"
- A "caixa" é formada por:
  - Espaço do _conteúdo_ <!-- {.box-model-part style="background: #8bb4c0;"} -->
  - Espaço de _preenchimento (`padding`)_ <!-- {em:.box-model-part style="background: #c2ce89;"} -->
  - Bordas _(`border`)_ <!-- {em:.box-model-part style="background: #fddc9a;"} -->
  - Espaço _externo (`margin`)_ <!-- {em:.box-model-part style="background: #f9cc9d;"} -->

<!-- {ul^1:style="margin-bottom: 0;"} -->

![](../../images/box-model-sample.png) <!-- {p:.centered.no-margin.invert-colors-dark-mode} -->

---
<!-- {"backdrop": "oldtimes"} -->
## _Box Model_: **largura** e **altura**

- Quando definimos a **largura** (`width`) ou **altura** (`height`) de
  um elemento, estamos definindo o tamanho
  do _conteúdo da caixa_, <!-- {em:.box-model-part style="background: #8bb4c0;"} -->
  e não da caixa inteira

![](../../images/box-model-product-0.png)<!-- {.bullet.figure-step.bullet-no-anim.rounded.bordered} -->
![](../../images/box-model-product-1.png)<!-- {.bullet.figure-step.bullet-no-anim.rounded.bordered} -->
![](../../images/box-model-product-2.png)<!-- {.bullet.figure-step.bullet-no-anim.rounded.bordered} -->
![](../../images/box-model-product-3.png)<!-- {.bullet.figure-step.bullet-no-anim.rounded.bordered} -->
![](../../images/box-model-product-4.png)<!-- {.bullet.figure-step.bullet-no-anim.rounded.bordered} -->
![](../../images/box-model-product-5.png)<!-- {.bullet.figure-step.bullet-no-anim.rounded.bordered} -->

---
<!-- {"layout": "tall-figure-right", "hash": "alterando-o-box-model", "backdrop": "oldtimes"} -->
## Alterando o _box model_

As **margens** de um elemento formam um **espaçamento externo** e não contam
espaço dentro da caixa.

- É possível alterar o significado da `width` e `height` que damos a um elemento <!-- {ul:style="margin-bottom: 0"} -->
   <br>**usando _a propriedade `box-sizing`_** <!-- {em:.underline.upon-activation.delay-3000} -->:
  - `box-sizing: content-box` (valor padrão)
    - `width` = largura do _conteúdo_ <!-- {.box-model-part style="background: #8bb4c0;"} -->
  - `box-sizing: border-box`
    - `width` = _conteúdo_ <!-- {.box-model-part style="background: #8bb4c0;"} --> +
      _padding_ <!-- {.box-model-part style="background: #c2ce89;"} --> +
      _border_ <!-- {.box-model-part style="background: #fddc9a;"} -->
    - Esta forma é mais intuitiva :thumbsup: :thumbsup: :thumbsup:

![](../../images/box-model-product-0.png)<!-- {.bullet.figure-step.bullet-no-anim.rounded.bordered} -->
![](../../images/box-model-product-2.png)<!-- {.bullet.figure-step.bullet-no-anim.rounded.bordered} -->
![](../../images/box-model-product-border-box-1.png)<!-- {.bullet.figure-step.bullet-no-anim.rounded.bordered} -->
![](../../images/box-model-product-border-box-2.png)<!-- {.bullet.figure-step.bullet-no-anim.rounded.bordered} -->

---

# _Unicorns are real_
## Conheça a verdade

![Little Pony](../../../images/little-pony.png) <!-- {.portrait.push-right} -->
- Atividade de hoje
  - _Layouts_ no Photoshop
  - Quebrando linhas no texto
  - Relembrando o _Box Model_
<!-- {ul:.content} -->

---

# Atividade de Hoje

- Criar uma página para expor a verdade sobre esses pôneis.
  - Seu amigo _designer_ criou um _layout_ no Photoshop para sua página e você
    deve criá-la de forma a reproduzir esse _layout_ na sua página HTML
  - Você pode ver o _layout_ na página seguinte
  - Você vai precisar lembrar: `div`, `span`, _Box Model_,
    `float` e `clear`
- [Baixe os arquivos][unicorns-seminal] contendo o HTML e estilize a
  página pra que ela fique idêntica ao _layout_ do _designer_
  - Leia as instruções detalhadas no arquivo `README.md`

[unicorns-seminal]: https://github.com/fegemo/cefet-front-end-unicorns/archive/master.zip

---