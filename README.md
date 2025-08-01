# 🍕 Pizzeria
La pizzería necesita un sistema para gestionar sus productos (pizzas, panzarottis, bebidas, postres, adiciones), combos, ingredientes, pedidos y clientes.
Los pedidos pueden ser para comer en el lugar o para recoger, y los clientes pueden personalizar sus productos con adiciones.

## 🚀 INVESTIGACIÓN

### 📄 ¿Qué es una base de datos NoSQL?

Una Base de Datos no Relacional es una forma de almacenar datos de manera más flexible que las bases de datos relacionales.
En las bases de datos no relacionales, no se tiene tanta rigidez. Los datos pueden estar estructurados de una forma más flexible. Pueden organizarse en:

* **Documentos:** Los datos se almacenan como documentos (similares a los archivos JSON), donde cada documento puede tener diferentes propiedades.

* **Clave-valor:** Almacenan datos como pares de "clave" y "valor", como si fuera una caja donde la clave es el nombre de la caja y el valor es lo que hay dentro.

* **Grafos:** Los datos se almacenan en forma de grafos, donde los nodos están conectados entre sí por relaciones. Esto es útil para redes sociales o rutas de transporte.

* **Columnas:** Los datos se almacenan en columnas, lo cual es útil cuando se tienen muchos datos pero no siempre con las mismas características.

### 🌿 ¿Qué es MongoDB?

MongoDB es un DBMS no relacional (NoSQL)

Almacena datos en documentos flexibles similares a JSON , por lo que los campos pueden variar entre documentos y la estructura de datos puede cambiarse con el tiempo. Estos documentos pueden almacenar distintos tipos de datos y distribuirse en diferentes sistemas. MongoDB usa el formato BSON (JSON compilado) para guardar información, dando la libertad de manejar un esquema libre. Este motor de base de datos es uno de los mas conocidos y usados ya que simplifica la gestion de bases de datos para los desarrolladores y además crea un entorno altamente escalable para aplicaciones y servicios multiplataforma.

### 🌀 ¿Qué diferencia hay entre una base de datos relacional (como MySQL) y una base de datos documental como MongoDB?

La principal diferencia radica en su estructura, ademas encontramos diferencia en el modelo de sus datos y como manejan y almacenan la informacion. Las bases de datos relacionales manejan un esquema rigido mientras que las no relacionales tienen un esquema flexible. A continuación podemos observar sus diferencias mas destacables:


| Característica      | Base de datos relacional (MySQL) | Base de datos documental (MongoDB) |
| ------------------- | -------------------------------- | ---------------------------------- |
| **Modelo de datos** | Tablas con filas y columnas      | Documentos (JSON/BSON)             |
| **Esquema**         | Rígido                           | Flexible                           |
| **Relaciones**      | JOINs y claves foráneas          | Desnormalización (documentos)      |
| **Escalabilidad**   | Escalabilidad vertical           | Escalabilidad horizontal           |
| **Consultas**       | SQL                              | Consulta basada en documentos      |
| **Transacciones**   | ACID                             | Soporte limitado o reciente ACID   |
| **Rendimiento**     | Bueno con relaciones complejas   | Mejor con datos simples y grandes  |



Base de datos relacionales son ideales para aplicaciones que necesitan integridad de datos, relaciones complejas entre entidades, y consultas SQL robustas.
Base de datos no relacionales son mejores para aplicaciones con datos semi-estructurados o no estructurados, y cuando se requiere flexibilidad, escalabilidad horizontal, y alto rendimiento en lecturas.

### 📑 ¿Qué son documentos y colecciones en MongoDB?

En mongoDB un documento es una representación de un objeto de datos y esta basado en JSON, que mongo almacena en un formato binario llamado BSON. 
Los documentosa son estructuras que almacenan sus datos en pares "clave-valor", donde las claves son strings y los valores pueden ser cualquier tipo de datos. Los documentos pueden tener estructuras flexibles y cada documento puede tener campos diferentes lo que permite manejar datos semi-estructurados o no estructurados. 

LAs colecciones de3 datos en mongoDB son un conjunto de documentos que no tienen  esquema fijo ni restricciones de tipos de datos entre los documentos que contiene. Estads colecciones no tienen una estructura rigida como cada coleccion tiene un nombre y se puede tener multiples colecciones dentro de una base de datos. 

## 🧮 DISEÑO DE PROPUESTA

### Colecciones que tendriamos

* Clientes

* Productos

* Ingredientes 

* Combos 

* Pedidos 

* Promociones/Descuentos 

* Historial de Pedidos

### 🎒 ¿Qué información tendría un documento de pedido? ¿Y un producto?

Un pedido debe contener la información del cliente, los productos o combos pedidos, detalles de la modalidad (para llevar o comer en el lugar), estado del pedido, precios.

<img width="665" height="475" alt="image" src="https://github.com/user-attachments/assets/a2cefdb8-6056-4cd7-a672-8bdc97d010ef" />


Cada producto puede ser una pizza, bebida, postre, panzarotti, etc. Aquí también se incluyen los ingredientes y adiciones.

<img width="535" height="288" alt="image" src="https://github.com/user-attachments/assets/f3e50efd-5eac-4be7-9985-558b7556dfe5" />


### 📥 ¿Qué iría dentro del documento y qué se referenciaría?

Referencias:

* Los documentos de clientes contienen referencias a pedidos (IDs de pedidos).

* Los productos contienen referencias a ingredientes (si es necesario).

* Los pedidos contienen referencias al cliente y los productos o combos seleccionados.

* Los combos contienen referencias a productos.

  <img width="733" height="469" alt="image" src="https://github.com/user-attachments/assets/8034e03f-f947-410a-a941-c94e88bc692b" />


  ### ¿Qué campos serían listas, objetos u otros documentos incrustados?
  
* productos en un pedido → Lista de objetos.

* ingredientes en un producto → Lista de objetos.

* adiciones en un producto personalizado → Lista.

### Ejemplos de documentos JSON

- Un producto

  Ejemplo de producto "Panzeriti de quesitooo"
  
<img width="410" height="239" alt="image" src="https://github.com/user-attachments/assets/d28da198-049f-4fc1-8244-4a3c7059a17b" />
  
- Un combo

  Ejemplo de Combo Extraqueso

<img width="426" height="246" alt="image" src="https://github.com/user-attachments/assets/04d8777a-b0dc-4128-9109-d64ab8e4735f" />

  
- Un pedido con un cliente y varios productos 
  
  Este es un ejemplo de pedido donde el cliente pide el combo grande "Combo Extraqueso", donde el cliente pide un adicional de Tocineta y Queso extra en su Panzeroti
  
<img width="658" height="885" alt="image" src="https://github.com/user-attachments/assets/b3da0f09-b7a2-45dd-8f6c-a18355d4b0ea" />

  
## 🙋‍♀️ Reflexión

### 🧩 ¿Qué fue lo más difícil de imaginar sin tablas?

Lo más dificil fue imaginar como organizariamos las colecciones y su contenido. También el relacionamiento que tendrian estas en el formato JSON, debido a que en las bases de datos relacionales es mas facil identificar estas relaciones gracias a las llaves. Estabamos acostumbradas al relacionamiento con JOINS. 

### 🧩 ¿Qué les gustó del enfoque con documentos?

La flexibilidad que nos permite este enfoque, es mas fácil la creacòn de documentos y hacer exansiones en el mismo, esto lo vimos al crear la coleccion para pedido ya que podiamos agregar diferentes atributos a su estructura.

### 🧩 ¿Qué dudas les surgieron al pensar en este nuevo tipo de base de datos?

Teniamos dudas de como estructurar la base de datos para nuestra pizzeria, debido a que no era muy claro para nosotras como organizar la información.

  ## 🤼‍♀️ AUTORES

   * Michel Rodriguez
   * Karolain Reyes






