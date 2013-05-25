Sass Lang
=========

Sass es una Gema Ruby la cual permite pre-procesar CSS incluyendo: funciones (mixin), variables, creacion de cascada de manera dinamica (selectores anidados), herencias y entre otras cosas.

## Sintaxis CSS

Sass maneja los mismos selectores y sintaxis por defecto de CSS, pero tambien permite usar sintaxis que no necesita los parentesis ni los ";" al final de cada linea, solo necesita indentacion y salto de lineas. Esta seleccion de sintaxis se hace por medio de la terminacion del archivo fuente Sass, si el archivo tiene como terminacion .scss la sintaxis sera la similar a la de CSS; Si la terminacion es .sass se usara la sintaxis simplificada (tipo python).

## Reglas CSS

Este ejemplo colocaremos una entrada de un archivo Sass y su respectiva salida salida en CSS.

### Sintaxis basica Sass

```sass
  // Selector de id
  #indentificador {
    propiedad: valor;
  }
  
  // Selector de class
  .clase {
    propiedad: valor;
  }
  
  // Selector anidado
  .clase_superior {
    propiedad: valor;
    .clase_interna {
      propiedad: valor;
    } 
  }
```

>NOTA: no existe en css ninguna propiedad llamada propiedad ni ningun valor llamado valor, eso hace referencia a cualquier propiedad css y a cualquier valor posible para dicha propiedad.
  
### Salida CSS al ejemplo anterior

```css

  #indentificador {
    propiedad: valor;
  }
  .clase {
    propiedad: valor;
  }
  .clase_superior {
    propiedad: valor;
  }
  .clase_superior .clase_inferior {
    propiedad: valor;
  }
  
```
## Variables

### Declaracion de variables

```sass
  $nombre_variable_1: valor1;
  $nombre_variable_2: valor2;

  #identificador {
      propiedad: $nombre_variable_1;
      propiedad: $nombre_variable_2;
  }

  etiqueta {
    propiedad: $nombre_variable_1;
  }
```

### Ejemplo en Sass

```sass
    $amarillo: #FEFF00; // Amarillo
    $margen-default: 20px; // margen que se usa por defecto

    .contenido {
    border-color: $amarillo;
    color: darken($amarillo, 9%);
    }

    .borde {
    padding: $margen-default / 2;
    margin: $margen-default / 2;
    border-color: $amarillo;
    }
```

### Salida en CSS 

```css
  .contenido {
  border-color: #FEFF00;
  color: #d0d100;
  }

  .border {
  padding: 10px;
  margin: 10px;
  border-color: #FEFF00;
   }
```


## Funciones

### Inicializacion de funciones

```sass
  // "@mixin" Palabra reservada para inicializador de las funciones
  
  //Funcion sin parametros 
  @mixin nombre_funcion {
    propiedad: valor;
    propiedad: valor;
  }

  //Funcion con parametros  
  @mixin nombre_funcion ($parametro){
    propiedad: $parametro;
    propiedad: $parametro;
  }
```
### Llamada de funciones

```sass
  //"@include" Palabra reservada para llamar a la funcion creada 

  // Funcion sin parametros
  .clase {
    @include nombre_funcion
    propiedad: valor;
  }
  
  //Funcion con parametros
  .clase {
    @include nombre_funcion ($parametro)
    propiedad: valor;
  }
```
> Para mayor información de las funciones de `SASS` puedes visitar este [link](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html) 
### Ejemplo en Sass

```sass
  $alto:100px;
  $ancho:200px;

  @mixin transicion ($tipo, $tiempo, $funcion) {
    -webkit-transition: $tipo $tiempo $funcion;
    -moz-transition: $tipo $tiempo $funcion;
    -ms-transition: $tipo $tiempo $funcion;
    -o-transition: $tipo $tiempo $funcion;
    transition: $tipo $tiempo $funcion;
  }

  .caja {
    heigth: $alto;
    width: $ancho;
    @include transicion(height,500ms,ease);
    &:hover {
      height: $alto * 2;
    }
  }
```

### Salida en CSS

```css
  .caja{
    height: 100px
    width: 200px
    -webkit-transition: height 500ms ease;
    -moz-transition: height 500ms ease;
    -ms-transition: height 500ms ease;
    -o-transition: height 500ms ease;
    transition: height 500ms ease;
    }

  .caja:hover{
    height: 200px;
  }
```
## Ciclos y Control de flujo en Sass

Las condiciones pueden ser de: igualdad (==), diferencia (!=), mayor que (>), menor que (<). Y pueden se varias condiciones usando las operaciones buleanas and, or, not.

```sass
    @for $i from $variable numero through $variable {
      .propiedad#{$i}: valor;
    }

    @if $variable == parametro1 {      
      .propiedad: valor;
    } @else if $variable == parametro2 {
      .propiedad: $variable;
    } @else {
      .propiedad: valor;
    }
```
### Ejemplo en Sass

```sass
    @for $i from 1 through $column_number {
      .grid#{$i} { @include column-calc($i); }
      .offset#{$i} { @include offset-calc($i);}
    }

      ...

    @mixin border-radius ($topL , $topR:"false" , $bottomR:"false" , $bottomL:"false") {
      @if $topR == "false" and $bottomR == "false" and $bottomL =="false" {
        -webkit-border-radius: $topL;
        -moz-border-radius: $topL;
        -ms-border-radius: $topL;
        -o-border-radius: $topL;
        border-radius: $topL;
      } 
      @else if $topL != "false" and $bottomR == "false" and $bottomL =="false" {
        -webkit-border-radius: $topL $topL $topR $topR;
        -moz-border-radius: $topL $topL $topR $topR;
        -ms-border-radius: $topL $topL $topR $topR;
         border-radius: $topL $topL $topR $topR;  
      } 
      @else if $topL != "false" and $bottomR != "false" and $bottomL =="false" {
        -webkit-border-radius: $topL  $topR  $bottomR $topR;
        -moz-border-radius: $topL $topR $bottomR $topR;
        -ms-border-radius: $topL $topR $bottomR $topR;
        -o-border-radius: $topL $topR $bottomR $topR;
        border-radius: $topL $topR $bottomR $topR;  
      } 
      @else {
        -webkit-border-radius: $topL  $topR  $bottomR $bottomL;
        -moz-border-radius: $topL $topR $bottomR $bottomL;
        -ms-border-radius: $topL $topR $bottomR $bottomL;
        -o-border-radius: $topL $topR $bottomR $bottomL;
        border-radius: $topL $topR $bottomR $bottomL; 
     }
    }
```
### Salida en CSS

```css
    .grid1 {
      width: 60px; }
    .offset1 {
      margin-left: 80px; }
    .grid2 {
      width: 140px; }
    .offset2 {
      margin-left: 160px; }
    .grid3 {
      width: 220px; }
    .offset3 {
      margin-left: 240px; }

      ...

      form input, form select {
        -webkit-border-radius: 5px;
        -moz-border-radius: 5px;
        -ms-border-radius: 5px;
        -o-border-radius: 5px;
        border-radius: 5px;
      }
```

## Operaciones Matemáticas

### Ejemplo en Sass

```sass
    $column_width : 60px;
    $column_number: 12;
    $column_gutter: 20px;

    .container {
      width: ($column_width * $column_number) + ($column_gutter * $column_number) - $column_gutter;      
    }
```

### Salida en CSS

```css
    .container {
      width: 940px;
       }
```