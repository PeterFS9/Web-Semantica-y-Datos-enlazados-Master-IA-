# Transformación de Bienes de Interés Cultural (BIC) de Castilla y León a Linked Data

## 1. Introducción
El objetivo de este proyecto es la generación de un conjunto de datos enlazados (Linked Data) a partir del registro de Bienes de Interés Cultural (BIC) inmuebles ubicados en la Comunidad Autónoma de Castilla y León.

La gestión del patrimonio histórico genera una gran cantidad de información que, habitualmente, se encuentra aislada en silos de datos o formatos no interoperables. Mediante la transformación de estos datos a RDF y su publicación siguiendo los principios de Linked Data, se pretende enriquecer la información original enlazándola con fuentes externas como DBpedia y Wikidata, permitiendo así consultas complejas (e.g., "¿Qué monumentos góticos existen en la provincia de Salamanca?") y su explotación mediante aplicaciones de visualización geoespacial.

## 2. Proceso de Transformación

### 2.1. Selección de la fuente de datos
Para este trabajo se ha seleccionado el conjunto de datos oficial de **"Bienes de Interés Cultural"** proporcionado por el Portal de Datos Abiertos de la Junta de Castilla y León.

* **Origen:** [Datos Abiertos JCyL - Bienes inmuebles de interés cultural](https://datosabiertos.jcyl.es/web/jcyl/set/es/cultura-ocio/bienes-inmuebles/1284872768044)
* **Responsables del contenido:** 
   * Dirección General de Vivienda, Arquitectura, Ordenación del Territorio y Urbanismo (Consejería de Medio Ambiente, Vivienda y Ordenación del Territorio).
    * Dirección General de Patrimonio Cultural (Consejería de Cultura, Turismo y Deporte).
* **Dataset original:** Bienes de interés cultural (inmuebles).
* **Cobertura temporal:** 
    * Inicio de publicación: 1 de octubre de 2012.
    * Última actualización: 1 de mayo de 2019.
* **Ámbito geográfico:** Castilla y León (España).

### 2.2. Análisis del formato y Preprocesamiento
El conjunto de datos original se distribuye en formato **ESRI Shapefile (.shp)**, un estándar para Sistemas de Información Geográfica (GIS). El paquete de descarga incluye los siguientes ficheros:

* `ps.pacu_cyl_bic_inmu_vw.shp`: Geometría de los objetos.
* `ps.pacu_cyl_bic_inmu_vw.shx`: Índice de la geometría.
* `ps.pacu_cyl_bic_inmu_vw.dbf`: Base de datos de atributos (formato dBase).
* `ps.pacu_cyl_bic_inmu_vw.prj`: Información de la proyección (sistema de coordenadas).
* `ps.pacu_cyl_bic_inmu_vw.xml`: Metadatos en formato XML.

**Desafíos de interoperabilidad detectados:**
Para la transformación semántica, la información relevante reside en el fichero de atributos **.dbf**. Sin embargo, se han encontrado dificultades técnicas para la ingesta directa de este formato en la herramienta OpenRefine.

**Solución (Preprocesamiento):**
1. **Conversión de formato:** Para extraer la información en forma de tabla, lo que he hecho es convertir, mediante un conversor online, el fichero `.dbf` a `.csv`.
2. **Problemas de codificación:** Después de esta conversión he visto que se han generado problemas en algunos caracteres, por ejemplo `CARDE├æA` en lugar de `CARDEÑA`.
3. **Estrategia de limpieza:** Estos errores de codificación, así como la normalización de fechas y tipos, se corregirán manualmente durante la fase de limpieza en **OpenRefine**, aplicando filtros y transformaciones GREL (Google Refine Expression Language).

### 2.3. Estructura de los datos
Las columnas principales del dataset (una vez convertido a CSV) identificadas para el modelado semántico son:

* `d_denomina`: Nombre oficial del bien (Mapeo a `rdfs:label`).
* `d_categori`: Categoría administrativa (ej. "Monumento", "Conjunto Histórico"). Se usará para definir el tipo de instancia (`rdf:type`).
* `c_bien_id`: Identificador único que se utilizará para la generación de la URI del recurso.
* `f_protecci`: Fecha de declaración del bien. Requiere transformación de formato a `xsd:date` (ISO 8601).
* `url_pweb`: Enlace a la ficha descriptiva en el portal de patrimonio (Mapeo a `rdfs:seeAlso`).

**Georreferenciación:**
El archivo de atributos textuales (.dbf/.csv) **no incluye coordenadas explícitas** (Latitud/Longitud), ya que estas residían en la geometría del Shapefile.
* *Estrategia:* Se utilizarán servicios de **reconciliación** en OpenRefine (contra Wikidata) para recuperar las coordenadas geográficas (`geo:lat`, `geo:long`) basándose en el nombre del monumento y su municipio.

### 2.4. Licencia
Los datos originales se publican bajo la **Licencia IGCYL-NC** (Uso no comercial), disponible en: [https://www.jcyl.es/licencia-IGCYL-NC](https://www.jcyl.es/licencia-IGCYL-NC).

En consecuencia, y para respetar los términos de reutilización, el dataset transformado resultante se publicará bajo una licencia **CC-BY-NC 4.0** (Creative Commons Attribution-NonCommercial), permitiendo su reutilización siempre que se cite la fuente y no se persigan fines comerciales.