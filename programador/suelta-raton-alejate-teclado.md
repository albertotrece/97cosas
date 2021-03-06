---
layout: programador
title: Suelta el ratón y aléjate del teclado
overview: true
author: Cay Horstmann
translator: Espartaco Palma
original: http://programmer.97things.oreilly.com/wiki/index.php/Put_the_Mouse_Down_and_Step_Away_from_the_Keyboard
---

Te has enfocado por horas en algún raro problema y no hay solución a la vista. Así que te levantas para estirar las piernas, o para llegar a la máquina expendedora, y en el camino de vuelta la respuesta repentinamente se vuelve evidente.

¿Te suena familiar este escenario? ¿Alguna vez te preguntaste porqué sucede? El truco está en que mientras estás codificando, la parte lógica de tu cerebro está activa y el lado creativo se bloquea. No puede presentarte nada hasta que tu lado lógico tome un descanso.

Aquí está un ejemplo de la vida real: Estaba limpiando algún código heredado y me encontré con un método 'interesante'. Estaba diseñado para verificar que una cadena contenía una hora válida usando el formato hh:mm:ss xx, donde hh representa la hora, mm representa los minutos, ss representa segundos, y xx podría ser AM o PM.

El método utilizaba el siguiente código para convertir dos caracteres (representando la hora) en un número, y verificando que estuviera en el rango adecuado:

    try {
        Integer.parseInt(time.substring(0, 2));
    } catch (Exception x) {
        return false;
    }

    if (Integer.parseInt(time.substring(0, 2)) > 12) {
        return false;
    }


El mismo código aparecía dos veces más, con cambios apropiados para el caracter y el límite superior, para poner a prueba los minutos y segundos. El método terminaba con estas líneas para comprobar AM y PM.


    if (!time.substring(9, 11).equals("AM") &
        !time.substring(9, 11).equals("PM")) {
        return false;
    }


Si ninguna de esta serie de comparaciones fallaba, regresando `false`, el método regresaba `true`.

Si el código anterior se veía confuso y difícil de seguir, no te preocupes. Yo también lo creía -- lo que significaba que había encontrado algo digno de limpieza. Lo refactoricé y escribí unas cuantas pruebas unitarias, sólo para estar seguro que aún funcionaba.

Cuando terminé, me sentía satisfecho con el resultado. La nueva versión era fácil de leer, de la mitad del tamaño, y más preciso debido a que el código original sólo probaba los límites superiores de las horas, minutos y segundos.

Mientras me preparaba para trabajar al día siguiente, una idea surgió a mi cabeza: ¿Porqué no validad la cadena usando una expresión regular? Después de unos minutos escribiendo, tenía una implementación funcional de sólo una línea de código. Aquí está:


    public static boolean validateTime(String time) {
        return time.matches("(0[1-9]|1[0-2]):[0-5][0-9]:[0-5][0-9] ([AP]M)");
    }


El punto de esta historia no es que eventualmente reemplacé cerca de 30 líneas de código con sólo una. El punto es que hasta que me alejé de la computadora, pensaba que mi primer intento era la mejor solución al problema.

Así que la próxima vez que estés ante un problema desagradable, hazte un favor. Una vez que realmente entiendas el problema ve a hacer algo que involucre el lado creativo de tu cerebro -- esboza el problema, escucha algo de música, o sólo da un paseo al aire libre. A veces la mejor cosa que puedes hacer para resolver un problema es soltar el ratón y alejarte del teclado.

