# LIP-Parser
Parser de Lenguaje Imperativo Simple implementado en Haskell con la libreria [**Parsec**](https://hackage.haskell.org/package/parsec).
Proyecto realizado con [**Stack**](https://docs.haskellstack.org/).

# Especificación
Gramática y sintáxis en `Especificación.pdf`

# Como utilizar el programa
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
# Info sobre estructuras utilizadas
En el archiov AST.hs estan definidas las estructuras utilizadas.
Se utilizo _Exp_ para definir las expresiones enteras y booleanas y _Comm_ para definir los comandos.

# Evaluadores
- 1 El primer evaluador recibe una secuencia de comandos y los va ejecutando. Le deja el manejo de errores a Haskell.
- 2 El segundo evaluador es igual que el primero solo que con manejo de errores interno. Los errores que maneja son UndefVar y DivByZero.
- 3 El tercer evaluador es igual al segundo, y además dentro del estado va llevando el _trabajo_ del programa

## Referencias
[1] - https://docs.haskellstack.org/en/stable/README/#how-to-install

[2] - https://downloads.haskell.org/~ghc/6.6/docs/html/users_guide/gadt.html

[3] - https://en.wikipedia.org/wiki/Generalized_algebraic_data_type

[4] - http://dev.stephendiehl.com/hask/#gadts

[5] - https://hackage.haskell.org/package/containers-0.6.3.1/docs/Data-Map-Strict.html

[6] - http://hackage.haskell.org/package/strict-0.4/docs/Data-Strict-Tuple.html

[7] - https://ghc.gitlab.haskell.org/ghc/doc/users_guide/exts/pattern_synonyms.html
