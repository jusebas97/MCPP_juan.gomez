# Juan Sebastián Gómez
## Proyecto Final


# ¿Qué investigamos en Ciencia Política? tendencias y evolución en los últimos 15 años



## Descripción y motivación

¿Qué investiga la Ciencia Política en Colombia?, normalmente esta pregunta ha girado en torno al objeto de estudio de la disciplina, pero se vuelve interesante ver los fenómenos que estudia esta disciplina en Colombia, ver cómo han evolucionado estos mismos, y cómo han respondido a la coyuntura nacional. 

Esta es una pregunta interesante para una disciplina que se ha nutrido de diferentes escuelas de pensamiento, por lo que será interesante responder a ella, no de una forma taxonómica, sino para identificar temas dominantes de esta disciplina en los últimos años. 

Para hacer este proyecto exploratorio, se scrapearon 4 repositorios, obteniendo información de titulos y fechas de 3242 trabajos de grado que se encuentran en repositorios universitarios de 4 universidades de Colombia (U. Nacional, U del Rosario, U. Javeriana, U de los Andes), las cuales tienen el programa de Ciencia Política con más de 15 años de trayectoria.

 
El estudio de estos 4 repositorios tiene 2 ventajas claras: 

- Estos repositorios tienen trabajos de grado y tesis disponibles desde alrededor de mitad de la década del 2000, lo que nos permite tener una muestra amplia en años para poder observar cambios temáticos (de haberlos). Por ello, se excluyen los repositorios de la Universidad Externado y la universidad de la Sabana.

- Al comparar la producción académica (trabajos de grado), de diferentes universidades, podremos ver si hay diferencias en los enfoques temáticos de cada universidad, e identificar patrones en la investigación en ciencia política, y decir cuáles han sido, y cómo han cambiado.
 
## Métodos empleados

1. Scraping
    - Los repositorios universitarios se encuentran disponibles de forma online en las siguientes url:
        - Universidad javeriana (964 trabajos de grado): 'https://repository.javeriana.edu.co/handle/10554/10014/recent-submissions'
        - Universidad del rosario (775 trabajos de grado): 'https://repository.urosario.edu.co/handle/10336/622/recent-submissions'
        - Universidad Nacional (1347 trabajos de grado): 'https://repositorio.unal.edu.co/browse?type=subject&value=32+Ciencia+pol%C3%ADtica+%2F+Political+science'
        - Universidad de los Andes (420 trabajos de grado): 'https://repositorio.uniandes.edu.co/handle/1992/29/browse?type=organization&value=Departamento+de+Ciencia+Pol%C3%ADtica'
    - Para obtener la información de estos repositorios usé las librerías de 'Selenium' y webdriver con chrome, junto con la búsqueda de los elementos de interés mediante XPATH. 
    - Se creó una función "next_page()" para poder iterar sobre las múltiples páginas de cada repositorio de manera automática.
    - El código de python con el cual se crearon las funciones para escrapear las páginas se encuentra [aquí](https://github.com/jusebas97/MCPP_juan.gomez/blob/master/Proyecto%20Final/functions.ipynb)

2. limpieza y almacenamiento de datos

    - Se scrapeo cada repositorio por separado, mpleando una función main que creé, la cual retorna una lista de diccionarios, por lo cual la convertí a un Dataframe usando la librería Pandas para cada repositorio, cuyo código puede ser encontrado [aquí](https://github.com/jusebas97/MCPP_juan.gomez/tree/master/Proyecto%20Final/Extracci%C3%B3n%20de%20datos). 
    - Creé una función "clean_date()" para limpiar la columna de fechas y convertir los strings con caracteres a solo los años como integrers, usando la librería 're' para usar expresiones regulares y hacer el filtrado. 
    - Para limpiar cada título cree una función "clean_titulo()" que usando las libreria de NLTK me ayudaba a eliminar signos de puntiación, poner todas las palabras en minúscula, tokenizar los títulos, y eliminar las stopwords en espeñol, usando NLTK y una lista que yo definí.
    - Finalmente, cada Data Frame se almacena como un archivo pickle, que luego permitió unir todos los Data frames para crear un archivo general. Los archivos se encuentran en esta [carpeta](https://github.com/jusebas97/MCPP_juan.gomez/tree/master/Proyecto%20Final/Archivos%20repositorios).




3. Resultados principales
### Nota: para mayor claridad, hacer click en las imagenes mismas
- Se evidenció que todas las Universidades, excepto la universidad de los Andes incrementó su producción de trabajos de gradoal rededor del 2011 - 2012.

![Tesis por año general](https://github.com/jusebas97/MCPP_juan.gomez/blob/master/Proyecto%20Final/graficos%20principal/Graficos%204%20repos%20unidos/txa_global.png)

![Andes_tesis](https://github.com/jusebas97/MCPP_juan.gomez/blob/master/Proyecto%20Final/Anl%C3%A1lisis%20de%20tesis/graficos%20andes/txa_andes.png)

- La producción académica se concentra en el estudio de las políticas públicas, y se ven en los gráficos de frecuencia de uso de palabras por años y general, que el foco de estudio principal son políticas públicas. 


![Frecuencia bigramas total](https://github.com/jusebas97/MCPP_juan.gomez/blob/master/Proyecto%20Final/graficos%20principal/Graficos%204%20repos%20unidos/Freq_bigramas_total.png)

- Se ve que hay una respuesta a fenómenos coyunturales, por lo que se evidencia el cambio claro en las temáticas tratadas en el año 2009 al 2016. 
    - En 2009 predominó el conflicto armado, el ex presidente Álvaro Uribe, reforma política debido al acto legislativo 001 de ese año, impulsado por el mismo presidente.
    - En 2016 predominó el estudio del conflicto armado, la construcción de paz, el tema de los acuerdos sobre participación política, víctimas y reparación, precisamente por la finalización de dialogos de la habana y el plebiscito. 
    - Es relevante resaltar que (Como se puede ver en las gráficas del [periodo 2006 - 2011](https://github.com/jusebas97/MCPP_juan.gomez/tree/master/Proyecto%20Final/Anl%C3%A1lisis%20de%20tesis)), Álvaro Uribe apareció constantemente, cosa que no sucedió con santos (tal vez, por la forma en que cada quien enfocó su gobienro).
    
![Bigrama 2016 general](https://github.com/jusebas97/MCPP_juan.gomez/blob/master/Proyecto%20Final/graficos%20principal/Graficos%204%20repos%20unidos/bigramtotal_2016.png)
![W 2016 general](https://github.com/jusebas97/MCPP_juan.gomez/blob/master/Proyecto%20Final/graficos%20principal/Graficos%204%20repos%20unidos/top10gen_2016.png)


![Bigrama_2009 general](https://github.com/jusebas97/MCPP_juan.gomez/blob/master/Proyecto%20Final/graficos%20principal/Graficos%204%20repos%20unidos/bigramtotal_2009.png)
![W 2009 general](https://github.com/jusebas97/MCPP_juan.gomez/blob/master/Proyecto%20Final/graficos%20principal/Graficos%204%20repos%20unidos/top10gen_2009.png)
    
    


## License
[MIT](https://choosealicense.com/licenses/mit/)
