## 👉 Metodos Algebráicos

Los métodos algebraicos representan una estrategia analítica para el diseño de controladores en lazo cerrado, que se basa en el uso de herramientas matemáticas formales para moldear la respuesta del sistema a partir de una función de transferencia deseada. A diferencia de métodos empíricos como Ziegler & Nichols, los métodos algebraicos no requieren pruebas experimentales, sino que parten del modelo matemático del sistema.

Su principio fundamental es ajustar la función de transferencia en lazo cerrado hasta que adquiera una forma previamente definida, que refleje las características dinámicas deseadas, como el tiempo de asentamiento, sobreimpulso o rapidez de respuesta.

Existen dos enfoques principales:

- Igualación de modelo: Consiste en forzar que la función de transferencia del sistema controlado sea igual a una función de referencia.

- Igualación de coeficientes: Se igualan los coeficientes del polinomio del sistema real con los del sistema deseado, obteniendo así las ganancias del controlador.

Este método es especialmente útil cuando se dispone de un modelo preciso del proceso a controlar y se desea lograr un comportamiento específico y bien definido, siendo muy común en aplicaciones académicas y de diseño detallado.

## 👉 Igualación de modelo por métodos algebráicos

La igualación de modelo es uno de los enfoques algebraicos más utilizados para el diseño de controladores en lazo cerrado. Su objetivo principal es forzar que la función de transferencia del sistema real controlado sea igual a una función de transferencia deseada o de referencia, que representa el comportamiento dinámico ideal que se quiere lograr (como una respuesta rápida, sin sobreimpulso, o con determinado tiempo de asentamiento).

### 🤚 Funciónamiento

1. Se parte del modelo matemático del sistema en lazo abierto (función de transferencia del proceso).

2. Se define una función de transferencia deseada, que representa el comportamiento objetivo (por ejemplo, una respuesta tipo segundo orden con sobreamortiguamiento).

3. Se plantea la estructura del controlador (por ejemplo un PID, PI, o una forma general).

4. Se forma la ecuación del sistema en lazo cerrado, combinando el proceso y el controlador.

5. Finalmente, se igualan las funciones de transferencia del sistema real y del modelo deseado. De esta comparación se obtienen las ganancias o parámetros del controlador.

### 🤚 Ventajas

1. Precisión en la respuesta deseada:
Permite diseñar el controlador con una función de transferencia exacta, adaptada a un comportamiento deseado (por ejemplo: rapidez, amortiguamiento, ausencia de sobreimpulso).

2. Basado en teoría sólida:
Se apoya completamente en el análisis matemático del sistema, lo cual lo hace riguroso y predecible si el modelo del proceso es confiable.

3. No requiere experimentación:
A diferencia de métodos empíricos, este enfoque no necesita hacer pruebas físicas con el sistema, lo cual es útil cuando no se puede intervenir el proceso.

4. Aplicabilidad a diferentes estructuras:
Se puede usar para diseñar controladores PI, PID, de avance/atraso o de estructura más compleja.

### 🤚 Desventajas

1. Alta dependencia del modelo matemático:
Si el modelo del sistema no es exacto o presenta incertidumbres, el controlador diseñado podría ser ineficaz o inestable.

2. Complejidad algebraica:
A medida que aumenta el orden del sistema, la resolución de las ecuaciones se vuelve más compleja, lo que puede dificultar el diseño práctico.

3. No considera limitaciones físicas:
El diseño puramente algebraico no contempla saturaciones, no linealidades ni retardos que sí están presentes en sistemas reales.

4. Poca robustez ante perturbaciones o variaciones del proceso:
Un cambio en los parámetros del sistema puede hacer que el controlador deje de cumplir su objetivo.

### 🤚 Conlusión 

El método de igualación de modelo es una herramienta poderosa y precisa para el diseño de controladores en lazo cerrado, especialmente en entornos donde se dispone de un modelo matemático confiable y se requiere una respuesta muy específica. Sin embargo, su aplicación en sistemas reales debe hacerse con precaución, debido a su sensibilidad a errores de modelado y a su limitada robustez ante incertidumbre o variabilidad. Por ello, en la práctica, suele complementarse con simulaciones y validaciones experimentales para asegurar un desempeño efectivo del sistema controlado.

## 👉 Igualación de coeficientes

La igualación de coeficientes es un enfoque algebraico que consiste en comparar los coeficientes de la función de transferencia del sistema en lazo cerrado con los de una función de transferencia deseada (modelo de referencia). El objetivo es diseñar un controlador (como un PI o PID) que modifique el comportamiento del sistema para que coincida con las especificaciones de rendimiento deseadas.

### 🤚 Funciónamiento

1. Se parte del modelo del sistema en lazo abierto

2. Se elige un tipo de controlador (PI, PD, PID, etc.)

3. Se obtiene la función de transferencia en lazo cerrado

4. Se plantea un modelo deseado

5. Se igualan los denominadores y/o numeradores

6. Se resuelve el sistema de ecuaciones

### 🤚 Ventajas 

1. Aplicación directa al modelo del sistema:
Permite obtener las constantes del controlador al comparar coeficientes de la función de transferencia del sistema deseado con la del sistema real en lazo cerrado.

2. Método sistemático y estructurado:
Al establecer una correspondencia entre coeficientes del numerador y denominador, se obtiene un proceso lógico y reproducible.

3. Útil para controladores estándar:
Es especialmente práctico para diseñar controladores tipo PI, PID o en compensadores cuando se conocen las especificaciones de tiempo de establecimiento, sobreimpulso y error en estado estacionario.

4. Fácil de automatizar en software:
Puede programarse fácilmente en MATLAB, Python u otras plataformas de cálculo simbólico para encontrar las ganancias de control.

### 🤚 Desventajas

1. Depende completamente del modelo matemático:
Si el modelo del sistema no representa bien el comportamiento real, el controlador diseñado puede ser inadecuado.

2. Puede generar soluciones no físicas o inviables:
En algunos casos, los coeficientes pueden dar lugar a valores negativos o no realizables de ganancia, tiempo de integración o derivación.

3. Limitado a sistemas lineales:
Tiene dificultades para tratar sistemas con no linealidades, retardos o variaciones dinámicas.

4. No considera restricciones del sistema real:
No incorpora directamente saturaciones, ruidos ni limitaciones de los actuadores o sensores.

### 🤚 Conclusión

El método de igualación de coeficientes es una herramienta poderosa para el diseño de controladores cuando se desea lograr una coincidencia precisa entre la función de transferencia del sistema real y un modelo de comportamiento deseado. Su enfoque algebraico sistemático lo hace ideal para fines educativos y para procesos con modelos bien definidos. Sin embargo, en sistemas reales es recomendable combinarlo con pruebas prácticas o técnicas de validación debido a su falta de robustez ante incertidumbre o variabilidad en el proceso.
