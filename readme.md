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