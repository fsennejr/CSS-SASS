#CSS com SASS

##Instalando Sass com node

´´´
	npm install -g node-sass
´´´


##SASS 
é baseado em identação e não precisa de ponto e virgula.


##.SCSS
é feito da mesma forma que o próprio CSS


##Gerando CSS

´´´
	node-sass scss/style.css css/style.css
´´´


##Gerar automáticamente CSS

###Node vai ficar assistindo as alterações no terminal


´´´
	node-sass --watch scss/style.css css/style.css
´´´


##SELETORES
###exemplo CSS

nav {
	width:100%;
	background:#000;
}

nav ul {
	list-style: none;
}

nav li {
	color: #fff;
	display:inline-block;
}


###Exemplo SCSS
nav {
	width:100%;
	background:#000;

	ul {
		list-style: none;
	}

	li {
		color: #fff;
		display:inline-block;
	}

}


##Exer 1 
###trabalhando com Seletores

diretório > scss/exer1.scss


##Interpolação

###Exemplo 1

```
$name: destaque;
$attr: border;

p.#{$name}{
	#{$attr}-color:blue;
}
```

###Resultado 1
```
p.destaque {
	border-color: blue;
}
```

###Exemplo 2
```
p{
	$font-size:12px;
	$line-height:30px;
	font: #{$font-size}/#{$line-height};
}
```

###Resultado 2
```
p {
	font: 12px/30px;
}
```

##Extend
utilizado para reutilizar estilos de outras classes.

###Exemplo 1
```
.msg {
	border: 1px solid;
	padding: 4px;
	text-align: center;
}

.msg-error {
	@extend .msg;
	border-color: #ff0000;
	color:#ff0033;
}

.msg-alert {
	@extend .msg;
	border-color: #ff8e00;
	color: #ff0011;
}

.msg, .msg-error, .msg-alert {
	border: 1px #
}
```

###Resultado 1
```
.msg, .msg-error, .msg-alert {
	border: 1px solid;
	padding: 4px;
	text-align: center;
}

.msg-error {
	border-color: #ff0000;
	color:#ff0033;
}

.msg-alert {
	border-color: #ff8e00;
	color: #ff0011;
}
```

###Exemplo 2
```
a:hover{
	text-decoration: underline;
}

.hoverlink{
	@extend a:hover;
	color: red;
}
```

###Resultado 2
```
a:hover, .hoverlink{
	text-decoration: underline;
}

.hoverlink {
	color:red;
}
```

É possível dar um EXTEND em mais de uma classe se necessário.


##OPERADORES

###Existem três tipos de operações no SASS

####1 operações de números
	<ul>
		<li>Division</li>
		<li>Subtraction, Negative Numbers</li>
	</ul>

	<ul>
		<li>adição +</li>
		<li>subtração -</li>
		<li>multiplicação *</li>
		<li>divisão /</li>
		<li>módulo %</li>
	</ul>

####2 operações com cores

####3 operações com string


### adição e multiplicação

as unidades devem ser compatíveis

###Exemplo

2em + 10px; // unidades incompatíveis.

5px + 2; // 7px // mantém a primeira unidade e fica compatível.

5px * 2px; // faria o quadrado e daria incompatível //unidade inválida.

// manter apenas um número com unidade.



### subtração e números negativos.

O sinal de - (menos/subtração) tem N significados em CSS e em SASS então é importante tomar cuidado com ele.

<ul>
	<li>pode ser operador de subtração (10px - 5px)</li>
	<li>Pode simbolizar um número negativo (-5px)</li>
	<li>Operador de negação (- $var)</li>
	<li>E parte de identificador (border-color)</li>
</ul>

###Tips

incluir espaços antes de depois em um subrtração:
Exemplo: 4px - 2px

Com número negativos, incluir espaço antes mas não depois 
Exemplo: 5px + -4px

Colocar uma negação unário entre parênteses caso ela esteja em uma lista separada por espaço
Exemplo: 10px (-$var)

###Divisão e /

```
p{
	font: 10px/5px;
	$width:1000px;
	width: $width/2;
	width: round(1.5)/2;
	height: (500px/2);
	margin-left: 5px + 100px/10px;
	font: (italic bold 10px/2px); 
	font-size: #{base-size}/  #{$line-height};
```
font: (italic bold 10px/2px); // não daria certo pois os valores não estão entre ()



font-size: #{base-size}/  #{$line-height}; //teria que criar as váriaveis mas não dária certo por não estão entre ()

para dar certo essa linha não é necessário fazer a interpolação apenas utilizar as variáveis.


```
p {
	font: 10px/8px; invalido
	width:500px;
	height:250px;
	margin-left:15px;
	font:italic bold 10px/8px; //invalido
	font-size:20px/22px; invalido
}
```

###Módulo

```
$font-size:27px;

p{
	font-size: $font-size %2;
}
```

###Operações com cores
```
p {
	color: #010203 + #040506;
}
```
resultado:<br>
01+04 = 05<br>
02+05 =	07<br>
03+06 = 09<br>

```
p{
	#050709	
}
```

multiplcação seria:
exe: #010203 * 2;

01 * 2
02 * 2
03 * 2

RGB e RGBA é a mesma coisa
RGBA devem ter o mesmo valor de alpha

###Operações com string
p{
	cursor: e + -resize;
}


p{
	cursor: e-resize; 
}



###Mixins
####SCSS
```
@mixin border-radius($radius){
	-webkit-border-radius: $radius;
	   -moz-border-radius: $radius;
		-ms-border-radius: $radius;
			border-radius: $radius;
}

.box {
	@include border-radius(10px);
}

```

####CSS
```
.box {
	-webkit-border-radius: 10px;
	   -moz-border-radius: 10px;
		-ms-border-radius: 10px;
			border-radius: 10px;
}
```

```
@mixin titulo($size, $color: blue){
	color: $color;
	font-size: $size
}

h1 {
	@include titulo(14px);
}

h1 {
	@include titulo(14px, green);
}

```


Mixins de Lista
```
@mixin pad ($values...) {
	padding: $values;
}
 p{
 	@include pad(20px);
 }

 p {
 	@include pad(10px 20px);
 }

 p {
	@include pad(10px 20px 30px);  
 }

 p {
 	@include pad(10px 20px 30px 40px );
 }

```


###Functions

###Exemplo1

```
$red: 100;
$green: 200;
$blue: 100;
$alpha: 0.8;
$color: red;
$amount: 80%;
$font: Open Sans;
$weight: "bold";
$real_round: 2.2;
$real: 2.5;

body {
	background: rgb($red, $green, $blue);
}

section {
	background: rgba($red, $green, $blue, $alpha);
}

section div {
	background: 	lighten($color, $amount);
	background: 	darken($color, $amount);
	font-family:	quote($font);
	font-weight: 	unquote($weight);
	padding: 		str-length($weight);
	font-family: 	to-upper-case($weight);
	font-family: 	to-lower-case($weight);
	width: 			percentage(str-length($weight));
	margin: 		round($real_round);
	margin: 		ceil($real);
	margin: 		floor($real);
}

}
```

lighten 		- clarear
darken 			- escurecer
quote 			- receber string sem aspas e add aspas para ela.
unquote			- remover aspas da string
str-length 		- tamanho da string - ex: bold = 4 caracteres
percentage		- transforma em % - pergando o exe acima: como foi retornado 4 caratecres ele faria *100 = 400%
to-upper-case	- tudo para maiusculo
to-lower-case	- tudo para minusculo
round			- round arredondar o numero real - ex: 2.2 ele arredonda para 2.5
ceil			- joga numero para cima - arredonda para cima
floor			- joga o numero para baixa - arredonda para baixo


###Resultado

```
body {
  background: #64c864; }

section {
  background: rgba(100, 200, 100, 0.8); }

section div {
  background: white;
  background: black;
  font-family: "Open Sans";
  font-weight: bold;
  padding: 4;
  font-family: "BOLD";
  font-family: "bold";
  width: 400%;
  margin: 2;
  margin: 3;
  margin: 2; }


```


###Exemplo2
```
@function calc-fluid($target, $container) {
	$result:($target/$container) * 100%;
	@return $result; 
}


div {
	width: calc-fluid(500, 1000);
}
```


###Resultado

```
div {
  width: 50%; }

```

####Mixins X Functions

Mixins - ele pode ser comparado a uma rotina ele faz mas não tem um return

Functions - executa muitas coisas porém no fim sempre ter um return


##PlaceHolders

diferenças entre:

Mixins: são esperados que sejam utilizados para blocos dinamicos.

e

Placeholders: esperados que sejam utilizados para blocos estáticos.

####Placeholders agrupam
```
%center {
	display:block;
	margin:0 auto;
}

div {
	@extend %center;
}

p {
	@extend %center;
}

```
###Resultado

```
div, p {
  display: block;
  margin: 0 auto; }

```




####Mixin não agrupa
```
@mixin center{
	display: block;
	margin: 0 auto;
}

section {
	@include center;
}

p {
	@include center;
}

```

###Resultado
```
section {
  display: block;
  margin: 0 auto; }

p {
  display: block;
  margin: 0 auto; }
```




### Control Directives - diretivas de controle
// if
```
$template: dark;

header{
	@if($template == dark) {
		color: #000;
	} @else if ($template == light){
		color: #FFF;
	} @else {
		color: #ccc;	
	}	
}
```

###Resultado
```
header {
  color: #000; }
```


// for
// poderia alterar Through por To
// Through - até que o valor seja igual a 3

// To - até que o valor seja menor que 3

```
@for $i from 1 through 3 {
	H#{$i} = {font-size: 4rem - $i}
}
```

###Resultado
```
H1 {
  font-size: 3rem; }

H2 {
  font-size: 2rem; }

H3 {
  font-size: 1rem; }
```




```
// Each

@each $social in facebook, linkedin, Github {
	.#{$social}-icon {
		background-image:url('/images/#{social}.png'); 
	}
}
```

###Resultado
```
.facebook-icon {
  background-image: url("/images/social.png"); }

.linkedin-icon {
  background-image: url("/images/social.png"); }

.Github-icon {
  background-image: url("/images/social.png"); }
```

```
$animals: dog, wolves, lions;

@each $animal in $animals {
	.#{$animal}-icon {
		background-image:url('/images/#{animal}.png'); 
	}
}

```
###Resultado
```
.dog-icon {
  background-image: url("/images/animal.png"); }

.wolves-icon {
  background-image: url("/images/animal.png"); }

.lions-icon {
  background-image: url("/images/animal.png"); }

```



// While
```
$i: 4;

@while $i > 0 {
	.item-#{$i} {
		width: 2em * $i;
	}

	$i: $i - 2;
}
```

###Resultado
```
.item-4 {
  width: 8em; }

.item-2 {
  width: 4em; }

```