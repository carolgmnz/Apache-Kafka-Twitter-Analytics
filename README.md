# Apache-Kafka-Twitter-Analytics
Producción y consumición de tweets en tiempo real utilizando la plataforma Apache Kafka. Para poder ejecutar este código es necesario crear una cuenta de desarrollador en la API de Twitter para obtener las credenciales o tokens que permiten recolectar los tweets. 
Los objetivos de este proyecto se han centrado en:
- Implementar un sistema con Apache Kafka, en primera instancia, con un único broker.
- Desplegar un productor y un consumidor y conectarlos con Twitter para poder extraer información en streaming.
- Mostrar de forma gráfica algunos resultados en tiempo real.
- Analizar una temática que afecte a la sociedad actual y que sea tendencia en Twitter.


INSTALACIÓN DE KAFKA
Para poder ejecutar este código es necesario instalar Apache Kafka en nuestro sistema operativo. Para ello, tan sólo es necesario buscar la página web de Apache kafka (https://kafka.apache.org) y descargar la última versión disponible. A continuación, se descomprime el fichero descargado en el directorio elegido y, en caso de windows, se debe crear una variable de entorno denominada KAFKA HOME, que haga referencia a la ruta/directorio de instalación.
Una vez instalado, se debe inicializar Zookeeper en una terminal y el servidor de Kafka en otra. Es esencial este paso, ya que Kafka requiere de Zookeeper activo para funcionar, pues es el encargado de manejar los brokers y ayudar en la elecci ́on de l ́ıderes para particiones.
Con la finalidad de que el código sea tolerante a fallos y tenga un buen rendimiento, se deberían crear varios brokers, sin embargo, como este proyecto será desplegado en local únicamente podremos contar con un broker.
En cuanto a los topics, se deben crear dos: en el primero se almacenarán los tweets “en crudo”, para ser posteriormente consumidos para procesarlos y guardar los datos de interés en un segundo topic.


DETALLES DEL CÓDIGO
Aparecen 4 scripts:
- Productor: recoge todos los tweets con el hashtag escogido y los produzca en el topic tweetsRaw.
- Consumidor-Productor: obtiene los tweets recogidos en el topic anterior, los procesa y los vuelve a reinsertar en un segundo topic (tweets- Processed). Utilizaremos este paso intermedio para sustituir ciertas palabras clave, como los @user de cada partido, por el nombre de los mismos, con el fin de hacer las comparaciones más equitativas.
- Consumidor Gráfico de Barras: lee los tweets procesados de tweetsProcessed y utiliza los datos para representarlos en tiempo real de dos formas: un gráfico de barras que muestre la suma acumulada de menciones para cada partido y una serie temporal que muestre el número de menciones a cada partido en distintas ventanas temporales.
- Consumidor Serie Temporal: también lee los tweets procesados y utiliza los datos para obtener una gráfica en tiempo real que muestra la evolución temporal del número de menciones por partido.
