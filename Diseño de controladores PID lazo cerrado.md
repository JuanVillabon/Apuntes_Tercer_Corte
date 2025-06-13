# Diseño de controladores PID en lazo cerrado

El diseño de controladores PID (Proporcional-Integral-Derivativo) en lazo cerrado se utiliza para regular variables de proceso como temperatura, presión, nivel, velocidad, entre otras, manteniéndolas lo más cerca posible del valor deseado (setpoint), aun ante perturbaciones o cambios en el sistema.

## Lazo Cerrado

Un sistema de control en lazo cerrado es aquel donde la señal de salida es retroalimentada y comparada con la señal de referencia (setpoint) para generar un error. Este error es procesado por el controlador PID para ajustar la señal de control y minimizar la diferencia entre la salida real y la deseada.

![image](https://github.com/user-attachments/assets/2b8ba37e-b579-4e15-b50f-f9e062621bc0)


- Ventajas del lazo cerrado:

  1. Corrige perturbaciones automáticamente.

  2. Mayor precisión en el control.

  3. Capacidad de adaptación a cambios en la dinámica del sistema.
 
## Método de Ziegler & Nichols (Ciclo Último)

El diseño de controladores PID en lazo cerrado es fundamental para lograr un control eficiente en sistemas dinámicos donde se requiere precisión y estabilidad. Uno de los métodos más utilizados para la sintonización de estos controladores es el método empírico propuesto por Ziegler y Nichols, conocido como 'ciclo último'. Este método permite ajustar los parámetros del PID sin necesidad de conocer el modelo matemático del sistema, lo que lo hace especialmente útil en aplicaciones industriales. A continuación, explicaré los pasos de este método, cómo obtener la ganancia última y el periodo de oscilación, y cómo utilizar estos valores para calcular las constantes del controlador PID.

### Pasos del método

**1. Se configuran las ganancias del controlador como:**

  - $K_{i} = 0$ (Acción integral) 

  - $K_{d} = 0$ (Acción derivativa)

Solo se activa la acción proporcioanl.

**2. Variar (aumentar) la ganancia proporcional $K_{p}$:**

  -  Se incrementa gradualmente la ganancia $K_{p}$ hasta que el sistema alcance una oscilación sostenida sin que se amortigüe ni crezca.
  -  En este punto, el sistema se considera marginalmente estable.
  -  Precaución: este paso se debe hacer con cuidado para evitar dañar el sistema si es real.

**3. Medir el periodo de oscilación obtenido:**

  - A este periodo se le denomina periodo último $P_{u}$.
  - Se mide el tiempo entre dos picos consecutivos de la oscilación sostenida.

**4. Registrar la ganancia proporcional en ese punto:**

  - Esta ganancia se llama ganancia última $K_{u}$.
  - Es la mayor ganancia para la cual el sistema aún no entra en inestabilidad.

***Fórmulas de ajuste para controlares Ziegler & Nichols***

| Tipo de Controlador | $K_p$            | $T_i$ (seg) | $T_d$ (seg) |
| ------------------- | ---------------- | ----------- | ----------- |
| P                   | $0.5 \cdot K_u$  | —           | —           |
| PI                  | $0.45 \cdot K_u$ | $P_u / 1.2$ | —           |
| PID                 | $0.6 \cdot K_u$  | $P_u / 2$   | $P_u / 8$   |


***Ventajas Ziegler & Nichols***
Una de las principales ventajas de este método es que no requiere conocer el modelo matemático del sistema, lo que lo hace ideal para plantas reales donde este modelo puede ser complejo o desconocido. Su aplicación es directa y práctica, ya que se basa únicamente en observar la respuesta del sistema ante variaciones en la ganancia proporcional.

Otra ventaja importante es que permite obtener una sintonización inicial rápida y efectiva para controladores PID. Aunque no necesariamente es la configuración más fina, sí proporciona un buen punto de partida que luego puede ajustarse si es necesario. Además, es fácil de aplicar en sistemas industriales con herramientas básicas de monitoreo.

***Desventajas Ziegler & Nichols***
A pesar de su simplicidad, este método presenta algunas limitaciones. La principal es que puede inducir oscilaciones fuertes durante el proceso de ajuste, ya que se lleva al sistema al borde de la inestabilidad para determinar los parámetros. Esto puede ser riesgoso en sistemas delicados o costosos.

Además, la sintonización obtenida suele ser agresiva, con sobreimpulsos altos y tiempos de establecimiento relativamente largos. Por esta razón, en aplicaciones donde se requiere una respuesta muy precisa y suave, es común que se utilicen métodos de ajuste más avanzados o que se realice una optimización posterior sobre los valores iniciales obtenidos con Ziegler & Nichols.

***Solución analítica***

$$ G = \frac{1}{s^{3}+6s^{2}+11s+6} $$

- Lazo cerrado;

$$ G_{o} = \frac{K_{p}\frac{1}{s^{3}+6s^{2}+11s+6}}{1+K_{p}\frac{1}{s^{3}+6s^{2}+11s+6}} $$

$$ = \frac{K_{p}}{s^{3}+6s^{2}+11s+6+K_{p}} $$

**Análisis de estabilidad marginal mediante la función de transferencia**

Cuando se desea encontrar la ganancia proporcional $K_{p}$ ue hace que un sistema sea marginalmente estable (es decir, que oscile de forma sostenida sin crecer ni amortiguarse), se puede hacer de forma analítica usando la función de transferencia.

- Paso 1: Asumir condición de oscilación pura

Se parte de la condición de oscilación sostenida, lo que implica que el sistema tiene polos en el eje imaginario puro, por lo que se usa:

$$ s = jw $$

La función de transferencia general se expresa como:

$$ G_{o}(s) = \frac{K_{p}}{s^{3}+6s^{2}+11s+6+K_{p}} $$

Sustituyendo $s = jw$

$$ G_{o}(jw) = \frac{K_{p}}{jw^{3}+6jw^{2}+11jw+6+K_{p}} $$

- Paso 2: Separar parte real e imaginaria del denominador

Desarrollamos cada término:

1. $(kw)^{3} = j^{3}w^{3} = -jw^{3}$
2. $(kw)^{2} = j^{2}w^{2} = -w^{2}$
3. $jw$ queda igual.

Sustituyendo:

$$ G_{o}(jw) = \frac{K_{p}}{-jw^{3}+6(-w^{2})+11jw+6+K_{p}} $$

Agrupamos por parte real e imaginaria:

- Parte imaginaria:

$$ j(-w^{3}+11w) $$

- Parte real:

$$ -6w^{2}+6+K_{p} $$

Entonces el denominador queda:

$$ j(w^{3}-11w) + (6+K_{p}-6w^{2}) $$

- Paso 3: Establecer condición de marginalmente estable

Para que el sistema sea marginalmente estable, se necesita que el denominador tenga parte real e imaginaria iguales a cero. Entonces:

Parte real = 0:

$$ 6+K_{p}-6w^{2} = 0 => K_{p} = 6w^{2}-6 $$

Parte imaginaria = 0:

$$ w^{3} - 11w = 0 => w(w^{2} - 11) = 0 => w = 0 o w = 11 $$

Se descarta w = 0 (no produce oscilación), entonces:

$$ w = 11 $$

Sustituimos este valor en la ecuación de $K_{p}$:

$$ K_{p} = 6(11)^{2} - 6 = 6(11) - 6 = 66 - 6 = 60 $$

- Resultado:

Para que el sistema sea marginalmente estable, la ganancia proporcional debe ser:

$$ K_{p} = 60 $$

## Método del Relé

El método del relé es una alternativa práctica y mejorada al método de Ziegler & Nichols en lazo cerrado. Su principal ventaja es que permite generar oscilaciones sostenidas en el sistema sin necesidad de aumentar excesivamente la ganancia proporcional, lo cual reduce el riesgo de dañar el proceso o la planta bajo control.

Además, permite una mayor manipulación y control de la prueba, ya que el comportamiento del sistema puede ser ajustado directamente a través de la amplitud y la histéresis del relé. Esto facilita obtener oscilaciones más limpias y estables, mejorando la precisión del cálculo de los parámetros del controlador.

### Metodología

El proceso general para aplicar este método consiste en los siguientes pasos:

1. Medir el tiempo en lazo abierto necesario para que el sistema alcance su estado estacionario, lo que permite establecer un punto de partida confiable para el ensayo.

2. Cerrar el lazo de control, sustituyendo temporalmente el PID por un relé con histéresis. Este relé actuará como controlador, generando una señal binaria que excita al sistema de manera periódica.

3. Capturar la salida del sistema, que idealmente debe ser una oscilación sostenida. Esta señal resultante es clave para determinar los parámetros del controlador.

4. Medir el periodo de oscilación (Pu) y la amplitud del ciclo (Au), ya que estos datos son fundamentales para calcular la ganancia equivalente.

5. Determinar la ganancia crítica $K_{c}$ que se calcula generalmente con una fórmula como:

$$ K_{c} = \frac{4d}{piA} $$

Donde:

- d es la amplitud del relé
- A es la amplitud de la salida oscilatoria

6. Determinar la ganancia estática, necesaria en algunos casos para ajustar con mayor precisión los parámetros del controlador final (PID o PI).

### Sintonización PI a partir del método del Relé

Una vez obtenidos los parámetros $K_{c}$ (Ganancia crítica) y $P_{u}$ (Periodo último) usando el método del relé, es posible ajustar un controlador PI (Proporcional-Integral) para el sistema. La tabla que aparece en la diapositiva presenta una forma ajustada de las fórmulas clásicas de sintonización, orientadas a garantizar un desempeño aceptable, por ejemplo, con un sobreimpulso menor al 10 %.

![image](https://github.com/user-attachments/assets/46bbc28f-6443-44a0-902e-844229d64480)

***Nota:*** Es muy común que se sigan usando las fórmulas de Ziegler & Nichols para lazo cerrado incluso cuando se emplea el método del relé, debido a que ambos buscan generar una oscilación sostenida como base para el ajuste. El método del relé simplemente evita los riesgos de forzar manualmente la ganancia proporcional hasta alcanzar ese punto.

## Fenómeno de Wind-up (Integral Wind-up)

El Wind-up ocurre cuando la acción integral del PID acumula un valor excesivo (saturación), especialmente cuando el actuador llega a su límite (por ejemplo, una válvula completamente abierta o cerrada) y el error persiste.

Consecuencias:

- Sobresalto excesivo al volver el sistema a la zona de control.

- Retardo en la recuperación del sistema.

- Oscilaciones no deseadas.
