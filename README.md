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







