# Name of Project - back-end

> Description of project

> Docs version x.y.z
## Requirements

- openjdk 11.0.8
- Gradle 6.7
- GNU Make 4.3
- Docker & Docker Compose
- Other requirements of project

## Run

```bash
make run
make down
```

## Organization

| Recurso         | Descripción                     | Ruta                              |
| --------------- | ------------------------------- | --------------------------------- |
| Módulo          | Código del módulo asignado      | src/main/java/../sadeb/*modulo-asignado* |
| Variables de entorno | Definición de variables de entorno y variables por defecto (dev), separar por módulo | .env |
| Configuraciones | Configuraciones de componentes personalizados | src/main/../sadeb/*config*/*
Componente*Config src/main/resources/application.yml |
| Clientes http   | Mapeo y pruebas de los endpoints | /client/*módulo-asignado*         |
| Scripts SQL | Contiene estructura, data, views, etc. precargados | sql_files/**.sql |

## Backend

1. Estructura de Carpetas

```
|   .env
|   dev.env
|   docker-compose.yml
|   Dockerfile
|   Makefile
|   settings.gradle
+---.github
|   \---workflows
|           postgre.yml
|           spring-boot.yml         
|           
+---sql_files
|       +
|
\---src
    +---main
    |   +---java
    |   |   \---com
    |   |       \---vallegrande
    |   |           \---sadeb
    |   |               |   
    |   |               +---common
    |   |               |   +---exception
    |   |               |   +---model
    |   |               |           
    |   |               +---config
    |   |               |       
    |   |               \---module x
    |   |                   +---controller
    |   |                   |       
    |   |                   +---dao
    |   |                   |   |
    |   |                   |   +---impl
    |   |                   |       |    
    |   |                   |       +---query    
    |   |                   +---dto
    |   |                   +---exception
    |   |                   +---mapper
    |   |                   +---service
    |   |                   +---validator
    |   |                       |
    |   |                       +---impl
    |   +---resources
    |    
    +---test
        +--- *same as src with what will be tested* 
```

2. Nomenclatura

**_Nota:_** Para todas las aplicaciones de nomenclatura utilizar el lenguaje del negocio y en idioma inglés.

- Paquetes
    * Por defecto todos los paquetes se escribirán en minúsculas y sin utilizar caracteres especiales.
    * El paquete base queda definido como _com.vallegrande.sadeb_, en este paquete no se definirá ninguna clase.

      **_Nota:_** Si existiera una parte común a varios de estos módulos, el nombre de los paquetes comenzarán por: _
      com.vallegrande.sadeb.common_

- Clases e Interfaces
    * Los nombres de clases deben ser mezclas de mayúsculas y minúsculas, con la primera letra de cada palabra interna
      en mayúsculas (CamelCase).
    * Debemos intentar mantener los nombres de clases simples y descriptivos.
    * Debemos usar palabras completas y evitar acrónimos y abreviaturas (se permiten DAO, DTO, etc.).
    * Si la clase cumpliese algún patrón determinado o tuviese una funcionalidad específica es recomendable definirlo en
      el nombre.

- Versionado Utilizaremos  [Versionado Semántico](https://semver.org/lang/es/), esto es a nivel de toda la aplicación,
  definiéndose en el archivo _build.gradle_, en la propiedad version con la siguiente nomenclatura:

```
		version = X.Y.Z
```

_Donde:_

```     
        X, Y, y Z son enteros no negativos
        
        X es la versión “major”
        
        Y es la versión “minor”
        
        Z es la versión “patch”
```

_Cada elemento DEBE incrementarse numéricamente en incrementos de 1._

**_Nota:_** El versionado de la aplicación será el tag de la versión de la imagen del contenedor y del package de
GitHub.

- Métodos
    * Los métodos deberán ser verbos (en infinitivo), en mayúsculas y minúsculas con la primera letra del nombre en
      minúsculas, y con la primera letra de cada palabra interna en mayúsculas (lowerCamelCase).
    * No se permiten caracteres especiales.
    * El nombre ha de ser lo suficientemente descriptivo, no importando a priori la longitud del mismo.

- Entornos

Se manejará los entornos de desarrollo y producción, los archivos serán:

dev.env y .env respectivamente.

* Ambos entornos deben tener las mismas propiedades.
* El nombre de la propiedad debe estar en mayúsculas y no debe contener caracteres especiales y con las palabras
  separadas por "_".
* No debe contener ningún comentario. Documentarlas en el propio proyecto.

- Atributos y parámetros
    * Reciben el mismo tratamiento que para los métodos, con la salvedad de que aquí sí importa más la relación entre la
      regla mnemónica y la longitud del nombre_._
    * Se evitará en la medida de lo posible la utilización de caracteres especiales, así como nombre sin ningún tipo de
      significado funcional.
    * Los nombres de constantes de clases deberían escribirse todo en mayúsculas con las palabras separadas por "_".
      Todas serán declaradas como _public static final_.

  **_Nota:_**  Aplica también para lambdas.

- Controllers

    - Las anotaciones de la clase del controller deben respetar el siguiente formato

```java

@RestController
@RequestMapping("/v1/nombreModulo")
@CrossOrigin
public class ModuloController {

}
```

- Nombrar los recursos con Sustantivos en lugar de Verbos

| RECURSO   | POST                      | GET                         | PUT                              | DELETE                   |
| --------- | ------------------------- | --------------------------- | -------------------------------- | ------------------------ |
| /autos    | Crea un nuevo auto        | Devuelve la lista de autos  | Actualización en bloque de autos | Borrar todos los autos   |
| /autos/71 | Método no permitido (405) | Devuelve un auto específico | Actualiza un auto específico     | Borra un auto específico |

* Usar nombres en plural
    * Evitaremos mezclar nombres en singular con nombres en plural.
    * Hacerlo simple y mantener los nombres en plural.

```
/autos
/autos/<id>

En caso haya acceso multiple
/autos/id/<id>
autos/color/<color>
```

* Proveer filtrado, ordenación, selección de campos y paginación para colecciones.
* Manejar [códigos de estado HTTP](https://www.talend.com/http-status-map/).

3. Documentación

Como norma es obligatorio proporcionar un comentario de documentación por cada _clase/interface_, método, propiedad o
constante creado.

Son obligatorios los siguientes comentarios de documentación:

* Comentario de la clase / interface:
* Prescripción genérica de la clase y su responsabilidad.
* Autor.

Reglas generales a la hora de escribir comentarios de documentación.

* Siempre se escribe en tercera persona.
  [comment]: <> (*   Los caracteres especiales tales como tildes y eñes se han de codificar con su código HTML
  correspondiente.)
* Las descripciones siempre deberían empezar por un verbo.

En cuanto a los tags utilizados el orden de los mismos es el siguiente:

```java
/**
 * @param Nombre del parámetro e indentada la descripción del mismo. usualmente esta descripción será una frase corta que comienza definiendo el tipo del parámetro.
 * @return Se comporta como el tag anterior a excepción de los void.
 * @throws Descripción breve de la posible causa de la excepción, sólo cuando haya una.
 * @link Sólo cuando la referencia sea necesaria
 */
```

*Adicionalmente:*
Para los controllers se usará *@Api*

```java

@Api(value = "Module REST Endpoint", description = "Description")
public class ModuleController {

}
```

Para los DTO *@ApiModelProperty*

```java
public class DemoDTO {
    @ApiModelProperty(notes = "name of the user")
    private String userName;
    @ApiModelProperty(notes = "salary of the user")
    private Integer salary;
    @ApiModelProperty(allowableValues = "active, inactive, banned")
    private String status;
}
```

**Nota:** Para el orden de los parámetros de las anotaciones en los *controllers* y *DTO* se usará el que viene por
defecto en la librería.

## Tests

- La estructura de paquetes será la misma que main.
- Se usará el sufijo Test para la clase y método a testear.
- Se debe respetar el siguiente orden:

```java
public class DemoTest {

    @InjectMocks
    private DemoService demoService;
    @Mock
    private DemoDAO DemoDAO;


    //DTO estáticos


    @BeforeAll
    public static void beforeAllDemo() {
    }
    
    @BeforeEach
    public void beforeEachDemo() {
    }

    @Test
    @DisplayName("Description of use case")
    void demoServiceTest() {
    }
    
    //More tests
    
    @AfterEach
    public void afterEachDemo() {
    }

    @AfterAll
    public static void afterAllDemo() {
    }
}
```

## Security Risks Preventions
- SQL Injection
- XSS
- ...

## Best practices

- [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
- More best practices for project

## Resources

- [Working With Relational Database Using R2dbc DatabaseClient](https://medium.com/swlh/working-with-relational-database-using-r2dbc-databaseclient-d61a60ebc67f)
- [R2DBC - Reactive Relational Database Connectivity](https://r2dbc.io/spec/0.8.0.RELEASE/spec/html/)
- [r2dbc-postgresql](https://github.com/pgjdbc/r2dbc-postgresql)
- More documentation of technologies of project