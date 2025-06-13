# 👉 Diseño de controladores PID en lazo abierto

## 👉 Controladores PID

Los controladores PID son herramientas fundamentales en la ingeniería de control automático. Su propósito es regular variables en sistemas dinámicos para que sigan una referencia deseada, minimizando el error de forma eficiente y estable. La sigla PID proviene de los tres términos que lo componen:

- *Proporcional (P):* Reacciona al error presente entre la variable medida y el valor deseado. A mayor error, mayor corrección.

- *Integral (I):* Acumula el error a lo largo del tiempo, corrigiendo errores persistentes (offset).

- *Derivativo (D):* Anticipa la tendencia del error, actuando sobre la velocidad del cambio para amortiguar las oscilaciones.

### 🤚 Contexto histórico

Nicolás Minorsky, en 1922, fue uno de los pioneros en el análisis del comportamiento de sistemas controlados automáticamente. En su publicación sobre la "Estabilidad direccional de cuerpos dirigidos automáticamente", propuso el uso de un sistema de control de tres términos para regular el rumbo del buque “New Mexico”. Aunque no se llamaban PID aún, su análisis sentó las bases para lo que hoy entendemos como un controlador PID.

No fue sino hasta 1936, con la participación de la Taylor Instrument Company, que se comenzaron a implementar controladores PID de propósito general en la industria. Inicialmente, se usó una acción derivativa fija (preestablecida en fábrica), pero para 1939, se desarrolló una versión más avanzada con acción derivativa ajustable, lo cual permitió una mayor flexibilidad y precisión en el control.

### 🤚 Importancia actual

Los controladores PID siguen siendo ampliamente utilizados en la industria moderna por su simplicidad, eficiencia y robustez. Se aplican en sistemas de control de temperatura, velocidad, presión, flujo, entre otros. Incluso en la robótica, la automatización de procesos y la electrónica de consumo (como los drones o termostatos), los PID juegan un papel esencial.

*Nota:* Aunque los controladores PID son muy versátiles, no son adecuados para todos los sistemas, especialmente aquellos altamente no lineales, con grandes retardos o dinámicas complejas. En estos casos, puede ser necesario usar técnicas más avanzadas como controladores adaptativos, difusos, o redes neuronales. Además, una mala sintonización de los parámetros PID (Kp, Ki, Kd) puede llevar a inestabilidad, oscilaciones o bajo rendimiento del sistema, por lo que es crucial realizar un ajuste cuidadoso, ya sea manual, mediante métodos heurísticos (como Ziegler-Nichols), o con técnicas automáticas.

## 👉 Acciones de control

Los sistemas de control utilizan diferentes acciones para corregir el comportamiento de un proceso. En un controlador PID, se combinan tres tipos fundamentales de acciones: Proporcional (P), Integral (I) y Derivativa (D). Cada una tiene una función específica y aporta ventajas particulares.

- ***Acción proporcional (P)***

Función: Aplica una corrección proporcional al error actual (la diferencia entre la señal deseada y la medida).

Limitación: No elimina completamente el error en estado estacionario (puede quedar un pequeño error permanente).

$$ u(t) = K_{p} * e(t) $$

$$ U(s) = K_{p} * E(s) $$

- ***Acción Integral (I)***

Función: Acumula el error a lo largo del tiempo y genera una corrección basada en la suma de errores pasados.

Limitación: Puede causar oscilaciones si se usa en exceso, debido a que reacciona de forma más lenta.

![image](https://github.com/user-attachments/assets/b43a20bf-9d88-4a5c-9600-453e2d6d955c)

- ***Acción Derivativa (D)***

Función: Responde a la tasa de cambio del error, anticipándose a su evolución futura.

Limitación: Muy sensible al ruido en la señal, por lo que debe utilizarse con cuidado.

![image](https://github.com/user-attachments/assets/06b62050-8acd-4021-9767-307d468bff05)

## 👉 Arquitecturas PID

Las arquitecturas PID definen cómo se estructuran y combinan las tres acciones de control (Proporcional, Integral y Derivativa) dentro del controlador. Aunque todas buscan el mismo objetivo corregir el error de un sistema, la forma en que se ensamblan afecta la dinámica del controlador y su facilidad de ajuste.

***1. Arquitectura Paralela***

Forma matemática $G(s) = K_{p} + /frac{K_{i}}{s} + K_{d}^{s}$

- Características:
A. Las tres acciones se implementan por separado y luego se suman.
B. Es la forma más común en la teoría moderna y fácil de ajustar individualmente.
C. Permite un control más intuitivo sobre cada ganancia K_{p}, K_{i} y K_{d}.

- Ventajas
A. Ajuste directo y flexible de cada término.
B. Útil en simulación y diseño digital

![image](https://github.com/user-attachments/assets/05834fc5-366f-4919-9d69-d9d1662c8415)

***2. Arquitectura Ideal***

Forma matemática $G(s) = K (1 + /frac{1}{T_{i}s} + T_{d}^{s}$

- Características:
A. Factor común $K$ (ganancia global) multiplica a la combinación de acciones.
B. Los parámetros son: $K$ (ganancia general), $T_{i}$ (tiempo integral), $T_{d}$ (tiempo derivativo).
C. Muy usada en controladores industriales reales y lógica de control comercial.

- Ventajas:
A. Facilidad de implementación en controladores físicos.
B. Parámetros más interpretables en función del proceso.

![image](https://github.com/user-attachments/assets/ce69ea77-ce6d-455b-ab99-620556fde9e0)


***3. Arquitectura Serie***

Forma matemática: $G(s) = K*(1+/frac{1}{T_{i}^{s}})*(1+T_{d}^{s})$

- Características:
A. Se multiplican bloques PID, por lo que las acciones interactúan entre sí.
B. Más sensible a los ajustes, requiere mayor cuidado en la sintonización.
C. Cada acción modifica el efecto de las demás.

- Ventajas:
A. Puede ofrecer mejores resultados en algunos sistemas complejos.
B. Respuesta más agresiva y compensación más precisa en ciertos casos.

![image](https://github.com/user-attachments/assets/8229b61b-93a9-4a1f-8fff-593c69b17429)

***Nota:*** Es importante destacar que la elección de la arquitectura PID adecuada depende del tipo de sistema a controlar y del entorno en el que se implemente. Por ejemplo, la arquitectura paralela es muy utilizada en sistemas digitales y simulaciones debido a su claridad y facilidad para ajustar individualmente cada acción de control. En cambio, la arquitectura ideal es común en aplicaciones industriales, ya que muchos controladores comerciales están diseñados bajo este esquema, lo que facilita su implementación práctica. Por otro lado, aunque menos utilizada, la arquitectura en serie puede ofrecer beneficios en sistemas con dinámicas complejas donde las acciones de control necesitan interactuar de forma más integrada. Comprender estas diferencias permite seleccionar la configuración más efectiva según las necesidades del proceso y garantizar un rendimiento óptimo del sistema de control.

## 👉 Sintonización por prueba y error

Es una técnica empírica utilizada para ajustar las ganancias de un controlador PID sin necesidad de conocer con precisión el modelo matemático del sistema. Se basa en observar el comportamiento del sistema en respuesta a los cambios en las ganancias y ajustar en consecuencia hasta obtener un rendimiento aceptable.

- **Metodologia mas frecuente**

1. Ajustar a 0 las ganancias integral y derivativa
2. Aumentar la ganancia proporcional $(K_{p})$ hasta obtener un buen tiempo de establecimiento
3. Aumentar la ganancia integral $(K_{i})$ para corregir el sobreimpulso o eliminar el error en estado estacionario
4. Aumentar la ganancia derivativa $(K_{d})$ para reducir oscilaciones
5. Reajustar la ganancia proporcional si es necesario
6. Ajuste fino de todas las ganancias

Este método es simple y útil cuando no se tiene un modelo matemático claro del sistema. Sin embargo, puede ser lento y arriesgado, ya que requiere experimentar directamente con el sistema real. Si no se tiene cuidado, se puede llegar a dañar componentes o generar inestabilidad.

En sistemas complejos o sensibles, se recomienda usar métodos más sistemáticos como Ziegler-Nichols, optimización basada en simulaciones, o algoritmos automáticos de sintonización.

## Métodos de sintonización de lazo abierto

Los métodos de sintonización en lazo abierto consisten en ajustar los parámetros del controlador PID sin cerrar el lazo de control durante el proceso de ajuste. Es decir, el sistema no está operando bajo retroalimentación automática mientras se realiza la identificación de sus características.

Estos métodos suelen usar la respuesta del sistema ante un cambio brusco en la entrada (como un escalón), lo que permite estimar el comportamiento del proceso y calcular las ganancias del controlador PID con fórmulas empíricas.

***1. Método de Ziegler y Nichols***

El método fue desarrollado en la década de 1940 por John G. Ziegler y Nathaniel B. Nichols, ingenieros de la empresa Taylor Instrument Company. Su objetivo era encontrar una forma sistemática y rápida de ajustar los controladores PID sin necesidad de modelos matemáticos complejos del sistema.

En esa época, los controladores eran mayormente analógicos, y no se contaba con herramientas computacionales modernas para simulación o análisis. Por eso, Ziegler y Nichols idearon una manera práctica de estimar los parámetros del sistema observando su respuesta a un escalón (un cambio repentino en la entrada).

![image](https://github.com/user-attachments/assets/ff1d69ab-69f3-4883-9186-0cf1d1c80e68)

- Caida de $/frac{1}{4}$ de la respuesta

![image](https://github.com/user-attachments/assets/e3ef9b63-bf71-457b-b4be-2e3a48bd3b32)

![image](https://github.com/user-attachments/assets/469aaf48-784c-4f0d-a87c-40f0060e5d60)

***2. Método Cohen - Coon***

El método Cohen-Coon fue desarrollado en 1953 por los ingenieros Graham C. Cohen y George A. Coon, quienes trabajaban en el análisis y diseño de sistemas de control en procesos industriales. Fue presentado como una mejora al método de Ziegler-Nichols (lazo abierto), especialmente para sistemas de primer orden con retardo (FOPDT: First Order Plus Dead Time), los cuales son muy comunes en la industria.

A diferencia del método de Ziegler-Nichols, que busca una respuesta rápida aunque sea con sobreimpulso, el método de Cohen-Coon se enfoca en lograr un compromiso más equilibrado entre rapidez, estabilidad y precisión. Por eso, es preferido en procesos donde el control debe ser más fino o donde el sobreimpulso no es tolerable.

![image](https://github.com/user-attachments/assets/2e5b188c-a008-4f45-a049-a794d4589bc5)

- Criterios de desempeño
1. Decaimiento de $/frac{1}{4}$
2. Mínimo sobre de impulso posible
3. Mínima Área bajo la curva

***3. Método por coeficiente de ajustabilidad***

El método por coeficiente de ajustabilidad (tuning by adjustability coefficient) se originó como una alternativa práctica para estimar parámetros PID sin depender exclusivamente de métodos como Ziegler-Nichols o Cohen-Coon. Aunque no fue desarrollado por un autor específico como los anteriores, se basa en el análisis empírico de la respuesta del sistema a una perturbación o entrada tipo escalón.

Su enfoque se apoya en una relación entre el grado de ajustabilidad del sistema (es decir, qué tan fácil o difícil es modificar su comportamiento con un controlador) y los parámetros característicos del modelo de primer orden con retardo.

Es un método más directo y accesible para técnicos e ingenieros de planta que tienen datos reales del sistema pero no quieren realizar análisis complejos.

![image](https://github.com/user-attachments/assets/d13c25c9-3dac-4e91-a70b-f3d85a83bdb6)

- Criterios de desempeño
1. Mínimo ITAE
2. Mínimo error con respecto a factor de amortiguamiento

***4. Método Smith***

El método Smith fue desarrollado por Otto J. M. Smith en 1957, como una solución al problema de controlar procesos industriales que presentan un tiempo muerto considerable.

El tiempo muerto (L) representa un intervalo en el que el sistema no muestra ninguna respuesta ante un cambio en la entrada. Este retardo complica mucho el diseño del controlador, ya que el sistema parece “ciego” durante ese período.

Smith propuso una estructura de control que predice el comportamiento del proceso sin esperar a ver la respuesta real, de modo que el controlador actúe como si el retardo no existiera. Esto mejora significativamente el desempeño del sistema.

![image](https://github.com/user-attachments/assets/384a8972-2ecd-4483-bd43-cff05dbfb29b)

![image](https://github.com/user-attachments/assets/d0efd99f-5be6-41a6-b9a8-6027fa83cda9)

