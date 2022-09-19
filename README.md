# LIP-Parser
Parser de Lenguaje Imperativo Simple implementado en Haskell con la libreria [**Parsec**](https://hackage.haskell.org/package/parsec).
Proyecto realizado con [**Stack**](https://docs.haskellstack.org/).

## Especificación
Sintáxis y semántica en `Especificacion.pdf`

## Como utilizar el programa
Stack se encarga de instalar la versión correcta de GHC, instalar los paquetes necesarios y compilar el proyecto. Para las primeras dos, basta con ejecutar
```
stack setup
```
dentro del proyecto.

Para compilar el programa, pararse en carpeta `code` y ejecutar el comando  
```
stack build
```
Una vez compilado el proyecto, se puede correr el ejecutable definido en `app/Main.hs` sobre un archivo `.lis` haciendo:
```
stack exec PARSER-exe -- PATH_TO_SOURCE [-OPT]
```
Las opciones disponibles son:
* `-p`: Imprimir el programa de entrada
* `-a`: Mostrar el AST del programa de entrada
* `-e N_EVALUADOR`: Elegir evaluador 1, 2 o 3 (1 por defecto)
* `-h`: Imprimir ayuda

Por ejemplo, para imprimir el programa `div.lis` del directorio `Ejemplos`, ejecutar
```
stack exec PARSER-exe -- Ejemplos/div.lis -p
```
Para correrlo con el evaluador de `Eval2.hs`
```
stack exec PARSER-exe -- Ejemplos/div.lis -e 2
```
Para imprimir el programa de entrada
```
stack exec PARSER-exe -- Ejemplos/div.lis -p
```
## Info sobre estructuras utilizadas
En el archiov AST.hs estan definidas las estructuras utilizadas.
Se utilizo la estructura ___Exp___ para definir las expresiones enteras y booleanas y ___Comm___ para definir los comandos.

## Evaluadores
Los tres evaluadores reciben una secuencia de comandos y un estado, y a medida que van ejecutando dichos comandos, van actualizando el estado.

- 1 Simplemente ejecuta los comando y le deja el manejo de errores a Haskell. El estado está definido como un Map(Var, Int), es decir, las ___keys___ son las variables, y los ___values___ su valor(entero).
- 2 El segundo evaluador es igual que el primero solo que con manejo de errores interno. Los errores que maneja son UndefVar y DivByZero. Además, el estado está definido igual que en el primer evaluador.
- 3 El tercer evaluador es igual al segundo, y además dentro del estado va llevando el _trabajo_ del programa. En este caso, el estado está definido como una tupla (Map(Var, Int), Int) donde la primer componente es el mapa anteriormente mencionado, y la segunda componente es el _trabajo_ del programa.

### Costos de trabajo de operaciones para tercer evaluador
- 1 W(e1 ___nop___ e2) = 3 + W(e1) + W(e2) donde ___nop___ in `{/, *}`
- 2 W(e1 ___bop___ e2) = 2 + W(e1) + W(e2) donde ___bop___ in `{+, -, And, Or, Lt, Gt, Eq, NEq}`
- 3 W(___op___ e) = 1 + W(e)               donde ___op___ in `{- unitario, Not}`

##
__Autores:__ [Caporalini Joaquin](https://github.com/JoaquinCaporalini) y Arroyo Joaquin
