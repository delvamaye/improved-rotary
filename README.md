# Clasificación de Sellers
### Versión 1.0 - 03 de junio de 2022

#### Caso a desarrollar
El equipo comercial quiere realizar estrategias focalizadas para los sellers, pero en este momento no existe una clasificación que permita identificar a aquellos que tienen un buen perfil y son relevantes para el negocio. 

Para desarrollar el caso se consideró crear un modelo de clasificación basado en el algoritmo kmeans, con información extraída de la api de Mercado Libre del país Colombia y de la categoría de Celulares y Teléfonos.

#### Conociendo los datos
En esta sección exploramos las variables en la documentación de la api, logrando entender que existían algunas variables que no nos proporcionaba información relevante para el modelo, debido a que tenían:
- Un sólo valor distinto.
- Valores nulos.
- No se necesitaba para el modelo.
- Duplicados.
- No se encontró explicación en la documentación.

Con lo obtenido anteriormente, se pudo refinar la selección de las variables que se usarían en el modelo.

#### Exploratorios 
- Encontramos que la variable 'price' tiene una distribución sesgada a la derecha, con una cola larga, dado que se encontraron valores pequeños (desde 4990 COP), al revisar la categoría, se identificó que, a pesar de que la categoría se llama Celulares y Teléfono (se espera montos elevados por entenderse que sólo hay equipos) existen accesorios o partes de celulares, lo que hace ver esos valores tan bajos.
- En cuanto a correlaciones con las variables numéricas tenidas en cuenta ('price','available_quantity', 'sold_quantity','installments.quantity', 'installments.amount') no presentan altas correclaciones (excepto 'price' y 'installments.amount' (correlación positiva mayor a 0.6).
- El 45% de los vendedores ha vendido más de 1 artículo, siendo la cantidad más alta de 39 artículos.
- De los vendedores con más de 1 artículo vendido, la rate_quant está entre 0 y 0.25.
- En cuanto a las direcciones del artículo y del vendedor tienen la misma distribución, siendo liderado el estado de Bogotá con el 64% de participación.

#### Transformaciones
Dado que la solución planteada está en funcion del algoritmo kmeans, se debe realizar un tratamiento especial para que el modelo no arroje resultados distorsionados. Para ello, se procedió a normalizar las variables que, finalmente entrarán al modelo.

#### Modelo
Como se mencionó anteriormente, el algoritmo escogido es kmeans (con distancia euclideana) dado que es un algoritmo:
- Fácil de implementar.
- Eficiente en la optimización para obtener los clústers.
- No consume altos volúmenes de recursos computacionales.

El mayor inconveniente de este algoritmo es la escogencia del número de clústers, para esto nos apalancamos en el uso del 'silhouette_score' y con la visual del gráfico 'Elbow Curve', para determinar dicho parámetro. Al ejecutar ambas metodologías, encontramos dos posibles soluciones de número de clústers. Para seleccionar el número adecuado, fue en base de la cantidad de vendedores en cada uno de los grupos generados, encontrando que es mejor escoger 3 grupos, dado que al utilizar 5 clústers generaba 2 grupos con pocos elementos, indicandonos que posiblemente hay outliers y que no nos da información suficiente de las características de dichos grupos.

Finalmente, con los tres grupos se obtuvieron los centroides permitiendo caracterizar cada grupo (en función del precio promedio de venta).

- Grupo 0 (Sellers Bronce): Sellers con bajos installments en cantidad y montos, bajo promedio de venta y bajas tasas de vendido/disponible. Corresponde al 58.3% de los sellers.

- Grupo 1 (Sellers Plata): Sellers installments amount medio, bajo installments quantity, promedio de venta intermedio y rate quant alto. Corresponde al 7.5% de los sellers.

- Grupo 2 (Sellers Oro): Sellers con mayores valores en installments amount, quantity y precio promedio vendido, mientras que la rate es baja. Corresponde al 34.1% de los sellers.

#### Conclusiones
Con la técnica utilizada de escoger las variables más relevantes, que en este caso fueron 4, y utilizar el algoritmo kmeans logramos obtener resultados coherentes para la cantidad de datos que se tenian.

Adicionalmente, la solución planteada da una clasificación de los sellers de forma tal que, el equipo comercial pueda generar estrategias en función del grupo, como por ejemplo: incrementar ventas con el grupo de vendedores que más precio promedio de venta tiene y realizar incentivos dado ese crecimiento, así como también hacer estrategias por la rotación de los artículos, entre otras posibles estrategias que sean relevantes para el negocio.

#### Siguientes Pasos
- Probar con otras variables.
- Agregar iteraciones con otros modelos de clusterización. 
- Aplicar a otras categorías. 
- Aplicar a otros países.
- Desarrollar herramientas que nos permita realizar un seguimiento a las estrategias que el equipo comercial vaya a plantear, de tal manera que, se pueda evidenciar si dicha segmentación permite lograr las metas planteadas.





