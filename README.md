# lemonbar - Barra ligera con aroma a limón

## SINOPSIS

**lemonbar** [-h | -g *ancho*x*alto*+*x*+*y* | -b | -d | -f *fuente* | -p | -n *nombre* | -u *píxel* | -B *color* | -F *color* | -U *color* | -o *desplazamiento*]

## DESCRIPCIÓN

**lemonbar** (anteriormente conocido como **bar**) es una barra ligera basada completamente en XCB. Proporciona soporte completo para UTF-8, formato básico, soporte para RandR y Xinerama, y cumplimiento con EWMH sin desperdiciar tu valiosa memoria.

## OPCIONES

- **-h**: Muestra la ayuda y sale.
- **-g** *ancho*x*alto*+*x*+*y*: Establece la geometría de la ventana. Si un parámetro se omite, se rellena con el valor predeterminado. Si el parámetro *y* se especifica junto con la opción **-b**, entonces la posición es relativa al fondo de la pantalla.
- **-b**: Acopla la barra en la parte inferior de la pantalla.
- **-d**: Fuerza el acoplamiento sin preguntar al gestor de ventanas. Esto es necesario si el gestor de ventanas no cumple con EWMH.
- **-f** *fuente*: Define la fuente para cargar en una de las cinco ranuras (el número de ranuras está codificado y se puede ajustar cambiando el parámetro **MAX_FONT_COUNT** en el código fuente). Esta versión admite especificadores de fuente de fontconfig y fuentes antialiasing.
- **-a** *número*: Establece el número de áreas cliqueables (el valor predeterminado es 10).
- **-p**: Hace que la barra sea permanente, no se cierra después de que se cierre la entrada estándar.
- **-n** *nombre*: Establece el valor del átomo **WM_NAME** para la barra.
- **-u** *píxel*: Establece el ancho de la línea subrayada en píxeles. El valor predeterminado es 1.
- **-B** *color*: Establece el color de fondo de la barra. El parámetro *color* debe especificarse en formato hexadecimal (#aarrggbb, #rrggbb, #rgb). Si no se está ejecutando un compositor como compton o xcompmgr, se ignora silenciosamente el canal alfa.
- **-F** *color*: Establece el color del primer plano de la barra. Acepta los mismos formatos de color que **-B**.
- **-o** *desplazamiento*: Agrega un desplazamiento vertical al texto. *desplazamiento* debe ser un número y puede ser negativo. **-o -3** desplazará el texto 3 píxeles hacia arriba.
- **-U** *color*: Establece el color de subrayado del texto. Acepta los mismos formatos de color que **-B**.

## FORMATEO

lemonbar proporciona una sintaxis de formato inspirada en screenrc para permitir la personalización completa en tiempo de ejecución. Cada bloque de formato se abre con **%{** y se cierra con **}** y admite los siguientes comandos; el analizador intenta manejar de la mejor manera la entrada mal formada. Usa **%%** para obtener un signo de porcentaje literal (C<%>).

- **R**: Intercambia los colores de fondo y primer plano actuales.
- **l**: Alinea el texto siguiente al lado izquierdo de la pantalla.
- **c**: Alinea el texto siguiente al centro de la pantalla.
- **r**: Alinea el texto siguiente al lado derecho de la pantalla.
- **O** *ancho*: Desplaza la posición actual en *ancho* píxeles en la dirección de alineación.
- **B** *color*: Establece el color de fondo del texto. El parámetro *color* puede ser **-** o un color en uno de los formatos mencionados anteriormente. El valor especial **-** restablece el color al valor predeterminado.
- **F** *color*: Establece el color del primer plano del texto. El parámetro *color* puede ser **-** o un color en uno de los formatos mencionados anteriormente. El valor especial **-** restablece el color al valor predeterminado.
- **T** *índice*: Establece la fuente que se usará para dibujar el texto siguiente. El parámetro *índice* puede ser **-** o el índice basado en 1 de la ranura que contiene la fuente deseada. Si el parámetro es **-**, lemonbar vuelve al comportamiento normal (coincidiendo con la primera fuente que se puede usar para el carácter). Si la fuente seleccionada no se puede usar para dibujar un carácter, lemonbar volverá al comportamiento normal para ese carácter.
- **U** *color*: Establece el color del subrayado del texto. El parámetro *color* puede ser **-** o un color en uno de los formatos mencionados anteriormente. El valor especial **-** restablece el color al valor predeterminado.
- **A** *botón*:I<comando>:
  Crea un área cliqueable que comienza desde la posición actual; cuando se hace clic en el área, se imprime *comando* en la salida estándar. El área se cierra cuando se encuentra un token **A** que no va seguido de **:**.

  Ej. **%{A:reboot:} Haz clic aquí para reiniciar %{A}**

  El campo *botón* es opcional; el valor predeterminado es el botón izquierdo, y es un número del 0 al 5 que se asigna a las acciones de pasar el mouse por encima, clic izquierdo, clic del medio, clic derecho, desplazamiento hacia arriba y desplazamiento hacia abajo. Tu experiencia puede variar.

  NOTA: Usar la opción de pasar el mouse por encima generará la salida para cada movimiento del mouse sobre un área.

  Las áreas cliqueables anidadas pueden activar comandos diferentes.

  Ej. **%{A:reboot:}%{A3:halt:} Haz clic izquierdo para reiniciar, clic derecho para apagar %{A}%{A}**

- **S** *dir*:
  Cambia el monitor en el que se renderiza la barra. *dir* puede ser:

  - **+**/**-**: Monitor siguiente/anterior.
  - **f**/**l**: Primer/último monitor.
  - *0-9*: N-ésimo monitor.

## MODIFICADORES DE ATRIBUTOS

- **+** *atributo*: Establece el atributo *atributo* para el texto siguiente.
- **-** *atributo*: Desactiva el atributo *atributo* para el texto siguiente.
- **!** *atributo*: Alterna el atributo *atributo* para el texto siguiente.

Donde *atributo* es uno de los siguientes:

- **o**: Dibuja una línea sobre el texto.
- **u**: Dibuja una línea bajo el texto.

## SALIDA

Al hacer clic en un área, lemonbar imprime el comando en la salida estándar, seguido de un salto de línea, lo que permite al usuario redirigirlo a un script, ejecutarlo o simplemente ignorarlo. Simple y poderoso, eso es todo.

## ENLACES

[Repositorio de Git](https://github.com/LemonBoy/bar)

## AUTOR

2012-2015 (C) The Lemon Man

2023 (C) Alyssa

El soporte Xinerama fue amablemente contribuido por Stebalien

El soporte RandR fue amablemente contribuido por jvvv

El soporte para áreas cliqueables se basó en gran medida en la contribución de u-ra
