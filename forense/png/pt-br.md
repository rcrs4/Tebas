# PNG

### Breve história sobre

PNG, _Portable Network Graphics_, trata-se de um tipo de arquivo de imagem que usa de compactação sem perdas. Criado inicialmente com o objetivo de substituir o formato _Graphics Interchange Format_ (GIF), pelo fato de que este possuia um algoritmo de compreensão patenteado, no entanto, o PNG não suporta animações (Este também não possuí limitações de direitos autorais). Ao longo dos anos, evoluiu e tornou-se um das extensões de imagens mais utilizadas hoje em dia.

### _Chunks_ e sua estrutura
PNG contém _chunks_ (blocos/pedaços) de estruturas críticos e auxiliares, onde estes são os que compõe os dados de um arquivo PNG, juntamente com o _header_ e _trailer_. Todos os chunks possuem o seguinte layout:

|Nome | Tamanho | Descrição |
|-----|:-------------:|:-------------|
| Tamanho|4 bytes| Comprimento que indicam o tamanho do bloco. Definem _n_ bytes de conteúdo. |
| Tipo/Nome|4 bytes| Indicam o nome do bloco. |
| Data|_n_ bytes| Conteúdo do bloco (com n bytes definidos pelo tamanho). |
| CRC|4 bytes| Verificação cíclica de redundância (utiliza dos bytes predecessores - desconsiderando os bytes de conteúdo - para efetuar esse cálculo).|

Convenção no nome dos _chunks_, suponhamos que tenhamos um bloco chamado de ***tBAs***, vamos fazer a análise em cima desse exemplo.

**t ->** Esta posição representa o _Ancillary bit_, indica se trata-se de um _chunk_ crítico ou auxiliar, caso seja crítico deve vir com a letra maiúscula. _Ancillary bit_: 0 (maiúscula) = crítico ou 1 (minúsculo) = auxiliar.

**B ->** Esta posição representa o _private bit_, indica se o bloco está registrado na lista de oficial de tipos de _chunks_ de PNG ou se é privado, que se resume em uso pessoal._Private bit_: 0 (maiúsculo) = pública ou 1 (minúsculo) = privado.

**A ->** Esta posição representa o _Reserved bit_, reservado para possíveis extensões do PNG futuras. Atualmente no padrão internacional a terceira letra deve vir maiúscula._Reserved bit_: 0 (maiúsculo) = padrão internacional ou 1 (minúsculo) = não suportado.

**s ->** Esta posição representa o _Safe-to-copy bit_, define o manuseio adequado de pedaços não reconhecidos em um fluxo de dados. _Safe-to-copy bit_: 0 (maiúsculo) = não seguro para cópia ou 1 (minúsculo) = seguro para cópia

### Estrutura do arquivo

* _Header_: Primeiros 8 bytes [89, 50, 4e, 47, 0d, 0a, 1a, 0a] (Em hexadecimal) de um arquivo PNG. Em um arquivo PNG é obrigatório a presença deles, sendo considerado uma estrutura crítica, caso contrário, a imagem será dada como corrompida e não poderá ser visualizada.
	
* **_Chunks_ críticos**
	* **IHDR** (Abreviação de _image header_): Como todo campo crítico, tem grande importância na composição da imagem. Este em particular, possuí dados relevantes em seu conteúdo, estes que são detalhados a seguir:
		
      |Nome | Tamanho | Descrição |
      |-----|:-------------:|:-------------|
      | Largura (_Width_)|4 bytes| Referente à dimensão da imagem |
      | Comprimento (_Height_)|4 bytes| Referente à dimensão da imagem |
      | Profundidade de bit (_Bit depth_)|1 byte| Fornece número de bits por amostra/índice de paleta|
      | Tipo de cor (_Color type_)|1 byte| Descreve a interpretação dos dados da imagem.|
      | Método de compreensão (_Compression method_)|1 byte| Indica o método usado para comprimir os dados da imagem|
      | Método do filtro (_Filter method_)|1 byte| Indica o método de pré-processamento aplicado aos dados da imagem antes da compressão |
      | Método de entrelaçamento (_Interlace method_)|1 byte| Indica a ordem de transmissão dos dados da imagem. |
	
    	- Tipos de cor são resultados da soma dos seguintes valores: 1 (indica que foi utilizado paleta), 2 (indica que foi usado coloração), and 4 (indica que o canal alfa foi utilizado). Valores finais válidos: 0, 2, 3, 4, e 6.
    	- Para largura e comprimento, zero é um valor inválido, sendo assim, caso estes possuam tal valor a imagem não poderá ser visualizada (Será tida como corrompida).
    	- Em matéria de curiosidade, até o momento, só temos definido um tipo de método de compreensão, este que recebe o valor de 0.

	* **IDAT** (Abreviação de _image data_):
		Podem haver múltiplos blocos IDAT, porém é necessário conter no mínimo um. Esse _chunk_ é o que contém o conteúdo de composição da imagem, em resumo, o bloco que possuí os bytes da imagem em si.
	* **PLTE** (Abreviação de _Palette_): Seu nome decorre de ser o bloco que trata de paletas de cor. Este _chunk_ é um caso especial, já que o mesmo pode não ser obrigatório dependendo do que já foi especificado até então. 
		- Precisa estar presente caso tenha sido específicado o tipo de cor 3 (Obrigatório aparecer).
		- Pode aparecer se o tipo de cor específicado for 2 ou 6 (Não obrigatório aparecer).
		- Não pode aparecer caso o tipo de cor seja 0 ou 4 (Obrigatório não aparecer).
		
      | Cor | Tamanho | Descrição |
      |-----|:-------------:|:-------------:|
      | R (Red/Vermelho) |1 byte| Onde 0 = Black (Preto) e 255 = Red (Vermelho) |
      | G (Green/Verde)|1 byte| Onde 0 = Black (Preto) e 255 = Green (Verde) |
      | B (Blue/Azul) |1 byte| Onde 0 = Black (Preto) e 255 = Blue (Azul) |
      
	* **IEND**: Campo que deve aparecer no final da imagem, possuí tamanho e conteúdo zerados, já que sua funcionalidade é apenas representar o final da imagem.

* **_Chunks_ auxiliares** (Algumas especificações foram resumidas para simplificação do conteúdo, caso tenha curiosidade ou interesse referências serão deixadas no final do documento para que possam ser consultadas): 
	* **cHRM** (Proveniente de _Primary chromaticities and white point_): Especificar as [cromáticas CIE x,y,z de 1931](https://www.hisour.com/pt/cie-1931-color-space-24840/) das primárias vermelha, verde e azul usadas na imagem, e o ponto branco referenciado.
	
	* **gAMA** (Proveniente de _Image gamma_): Especifica a relação entre as amostras de imagem e a intensidade de saída do display desejada.
	
	* **iCCP** (Proveniente de _Embedded ICC profile_): Estando presente significa que as amostras de imagem estão de acordo com o espaço de cor representado pelo perfil ICC incorporado, conforme definido pelo _International Color Consortium_. O espaço de cor do perfil ICC deve ser um espaço de cor RGB para imagens coloridas, ou um espaço de cor monocromática em escala de cinza para imagens em tons cinzentos. 
	
	* **sBIT** (Proveniente de _Significant bits_): Define o número original de bits significativos. Dessa forma, ele permite que os decodificadors PNG recuperem os dados originais sem perdas.
	
	* **sRGB** (Proveniente de _Standard RGB colour space_): Define a intenção de renderização específicada pelo _International Color Consortium_, sendo eles podendo ser _Perceptual_ (quando sRGB = 0), _Relative colorimetric_ (quando sRGB = 1), _Saturation_(quando sRGB = 2) e _Absolute colorimetric_ (quando sRGB = 3).
	
	* **bKGD** (Proveniente de _Background colour_): Especifica uma cor de fundo padrão para apresentar a imagem.
	
	* **hIST** (Proveniente de _Image histogram_): Fornece a frequência de uso aproximada de cada cor na paleta de cores. Quando este se encontra presente, é obrigatório a presença do PLTE também.
	
	* **tRNS**: Especifica valores alfa associados a entradas de paleta (para imagens de cores indexadas) ou uma única cor transparente (para escala de cinza e imagens de cores verdadeiras)
	
	* **pHYs** (Proveniente de _Physical pixel dimensions_): Especifica o tamanho/proporção em pixel pretendido para exibição da imagem. Caso este não se encontre presente, acredita-se que os pixels sejam quadrados, e o tamanho físico de cada pixel é desconhecido.
	
	* **sPLT** (Proveniente de _Suggested palette_): Fornece um conjunto recomendado de cores, com informações alfa e de frequência, que podem ser usadas para construir uma paleta reduzida.
	
    * **tIME** (Proveniente de _Image last-modification time_): Indica o tempo da última modificação de imagem, sendo estes mostrados por: Ano (2 bytes), mês (1 byte), dia, hora (1 byte), minuto (1 byte) e segundos (1 byte).
    
	* **iTXt, tEXt, e zTXt** (Todas são referente à _Textual information_): Usados como blocos de comentários (semelhantes à comentários de códigos).

### Ordem dos _chunks_
|Chunk|Ordem|
|-----|:---|
|IHDR|Primeiro a aparecer posteriormente dos bytes do _header_|
|PLTE|Se estiver presente, deve vir antes do IDAT |
|IDAT|Caso seja múltiplos IDATs, estes precisam ser consecutivos.|
|IEND|Último _chunk_|
|cHRM|Antes do PLTE e IDAT|
|gAMA|Antes do PLTE e IDAT|
|iCCP|Antes do PLTE e IDAT. Se possuir iCCP, o sRGB não pode estar presente.|
|sBIT|Antes do PLTE e IDAT|
|sRGB|Antes do PLTE e IDAT. Ao possuir sRGB, não pode conter iCCP.|
|bKGD|Depois do PLTE e antes do IDAT|
|hIST|Depois do PLTE e antes do IDAT|
|tRNS|Depois do PLTE e antes do IDAT|
|pHYs|Antes do IDAT|
|sPLT|Antes do IDAT|
|tIME|Não possuí|
|iTXt|Não possuí|
|tEXt|Não possuí|
|zTXt|Não possuí|


### Calculo do CRC
O polinômio CRC aplicado é o seguinte:
<p>x<sup>32</sup> + x<sup>26</sup> + x<sup>23</sup> +
x<sup>22</sup> + x<sup>16</sup> + x<sup>12</sup> + x<sup>11</sup>
+ x<sup>10</sup> + x<sup>8</sup> + x<sup>7</sup> + x<sup>5</sup>
+ x<sup>4</sup> + x<sup>2</sup> + x + 1</p>
Os dados de cada byte são processados do bit menos significativo para o bit mais significativo. Em seguida o CRC é invertido (seu complemento é tomado). Esse valor é transmitido (armazenado no fluxo de dados) utilizando da ordem de bit mais significativo primeiro.

**Referências**	

<https://www.w3.org/TR/PNG>

<http://www.libpng.org/pub/png/spec/1.2/PNG-Chunks.html>

![Logo Tebas](https://github.com/Pulho/Tebas/blob/novas-aulas/LogoIcon.png)

Feito por [Paulo Victor de Oliveira Andrade](https://github.com/Pulho)
