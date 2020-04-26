# Clean Code

## Capítulo 1: Código limpio

- Ejecuta todas las pruebas
- No tiene duplicados
- Expresa todos los conceptos de diseño del sistema
- Minimiza el número de entidades como clases, métodos, funciones y similares.
- Dar importancia al código

> La regla del Boy Scout: "Dejar el campamento más limpio de lo que se ha encontrado"

> Ley de LeBlanc: "Después es igual a nunca"

## Capítulo 2: Nombres con sentido

### Reglas básicas para nombres correctos

#### Usar nombres que revelen las intenciones

- Debe revelar nuestras intenciones
- Debe indicar por qué existe, qué hace y cómo se usa

```c#
public List<int[]> getThem(){
    List<int[]> list1 = new ArrayList<int[]>();
    for(int[] x : theList)
        if(x == 4)
            list1.add(x);
    return list1;
}
```



```c#
public List<Cell> getFlaggedCells(){
    List<Cell> flaggedCells = new ArrayList<Cell>();
    for(Cell cell : gameBoard)
        if(cell.IsFlagged())
            flaggedCells.add(cell);
    return flaggedCells;
}
```

#### Evitar la desinformación

- No demos información falsa, poner nombre de variable **accountList** cuando no es una List, mejor utilizar **accounts**
- Evitar nombres con variaciones mínimas

#### Realizar distinciones con sentido

- No utilizar el mismo nombre para hacer referencia a dos elementos distintos en el mismo ámbito.
- Si los nombres tienen que ser distintos, también deben tener un significado diferente.
- Las palabras adicionales son otra distinción sin sentido. Imagine que tiene la clase **Product**. Si tiene otra clase con el nombre **ProductInfo** y **ProductData**, habrá creado nombres distintos pero con el mismo significado.

#### Usar nombres que se puedan pronunciar

Compare:

```c#
class DtaRcrd102 {
    private Date genymdhms;
    private Date modymdhms;
    private final String pszqint = "102";
}
```

```c#
class Customer {
    private Date generationTimeStamp;
    private Date modificationTimeStamp;
    private final String recordId = "102";
}
```

#### Usar nombres que se puedan buscar

- Los nombres de una letra y las constantes numéricas tienen un problema: no son fáciles de localizar en el texto.

  ```c#
  for(int j = 0; j < 34 ; j++){
      s += (t[j] * 4) / 5;
  }
  ```

  ```c#
  int realDaysPerIdealDay = 4;
  const int WORK_DAYS_PER_WEEK = 5;
  int sum = 0;
  for(int j=0; j < NUMBER_OF_TASKS; j++){
      int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
      int realTaskWeeks = realTaskDays / WORK_DAYS_PER_WEEK;
      sum += realTaskWeeks;
  }
  ```

#### Evitar codificaciones

- Los nombres codificados resultan impronunciables y  suelen escribirse de forma incorrecta.

#### Prefijos de miembros

- No es necesario añadir m_ como prefijo a los nombres de variables.

```c#
public class Part {
    private String m_dsc; //La descripción textual
    void setName(String name){
        m_dsc = name;
    }
}
```

```c#
public class Part {
    String description;
    void setDescription(String description){
        this.description = description;
    }
}
```

#### Interfaces e implementaciones

Existe un caso especial para usar codificaciones. Imagine por ejemplo que crea un Abstract Factory para crear formas. Está Factory será una interfaz y se implementará por medio de una clase concreta. ¿Qué nombres debe asignar? ¿IShapeFactory y ShapeFactory? Prefiero las interfaces sin adornos. La **I** inicial, tan habitual en los archivos de legado actuales es, en el mejor de los casos, una distracción, y en el peor, un exceso de información. No quiero que mis usuarios sepan que se trata  de una interfaz, solamente que se trata de ShapeFactory. Si tengo que codificar la interfaz o la implementación, opto por ésta última. Es mejor usar ShapeFactoryImp o incluso CShapeFactory, que codificar la interfaz.

#### Evitar asignaciones mentales

- Este problema suele aparecer al elegir entre no usar términos de dominio de problemas o de soluciones.
- Es un problema de los nombres de variables de una sola letra. Utilizar i, j, k para un bucle.

#### Nombres de clases

- El nombre de una clase no debe ser un verbo.
- Evitar nombres como Manager, Processor, Data o Info.

#### Nombres de métodos 

- Los métodos deben tener nombres de verbos o frases verbales.
- Los métodos de acceso, modificación y los predicados deben tener como nombre su valor y usar como prefijo get, set e is.

``` C#
String name = employee.getName();
customer.setName("mike");
if(paycheck.isPosted())
```

Al sobrecargar constructores, use static factory methods con nombres que describan los argumentos. Por ejemplo:

```C#
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
```

Es mejor que:

```C#
Complex fulcrumPoint = Complex(23.0);
```

Considere forzar su uso haciendo que los constructores correspondientes sean privados.

#### No se exceda con el atractivo

- No utilizar bromas en los nombres.

#### Una palabra por concepto

- Elija una palabra por cada concepto abstracto y manténgalo. Por ejemplo: resulta confuso usar fetch, retrieve y get como métodos equivalentes de clases distintas.
- Del mismo modo **Manager** y **Controller** ¿Por qué no son dos Controllers o dos Managers? El nombre hace que espere que dos objetos tengan un tipo diferente y clases diferentes.

#### No haga juegos de palabras

- Evite usar la misma palabra para dos fines distintos.
- Nuestro objetivo, como autores, es facilitar la comprensión del código.
- Imagine que hay varias clases en las que **add** creo un nuevo valor sumando o concatenando dos valores existentes. Imagine ahora que crea una nueva clase con un método que añada su parámetro a una colección. ¿Este método debe tener el método **add**? No, en este caso hay una diferencia semántica,  de modo que debemos usar un nombre como insert o append.

#### Usar nombres de dominios de soluciones

- Recuerde que los lectores de su código serán programadores.
- Entonces, utilice términos informáticos, algoritmos, nombres de patrones, términos matemáticos y demás.

### Usar nombres de dominios de problemas

- Cuando no exista un término de programación para lo que esté haciendo, use el nombre del dominio de problemas.

### Añadir contexto con sentido

- La mayoría de los nombres no tiene significado por si mismo, es por ello que debe incluirlos en un contexto, en clases, funciones y namespaces con nombres adecuados.
- Cuando todo esto falle, pueden usarse prefijos como último recurso, pero seguramente será mejor crear algo que le de contexto como una clase.

Variables en un contexto ambiguo

``` C#
private void printGuesstStatistics(char candidate, int count){
    String number;
    String verb;
    String pluralModifier;
    
    if(count == 0){
        number = "no";
        verb = "are";
        pluralModifier = "s";
    } else if(count == 1){
        number = 1;
        verb = "is";
        pluraModifier = "";
    } else {
        number = Integer.toString(count);
        verb = "are";
        pluralModifier = "s";
    }
    
    String guessMessage = String.format(
    	"There %s %s %s%s", verb, number, candidate, pluralModifier
    );
    print(guessMessage);
}
```

- La función es demasiado extensa y las variables aparecen por todas partes.
- Para dividir la función en fragmentos más reducidos necesitamos crear una clase GuessStatisticsMessage y convertir a las tres variables en campos de la misma. De este modo contamos con un contexto más obvio para las tres variables. 

Variables con un contexto

``` C#
public class GuessStatisticsMessage {
    String number;
    String verb;
    String pluralModifier;
    
    public String make(char candidate, int count){
        createPluralDependtMessageParts(count);
        return String.format(
        	"There %s %s %s%s",
            verb, number, candidate, pluralModifier);
    }
    
    private void createPluralDependtMessageParts(int count){
        if(count == 0){
            thereAreNoLetters();
        } else if (count == 1) {
            thereIsOneLetter();
        } else {
            thereAreManyLetters();
        }
    }
    
    private void thereAreManyLetters(){
        number = Integer.toString(count);
        verb = "are";
        pluralModifier = "s";
    }
    
    private void thereIsOneLetter(){
        number = 1;
        verb = "is";
        pluraModifier = "";
    }
    
    private void thereAreNoLetters(){
        number = "no";
        verb = "are";
        pluralModifier = "s";
    }
}
```

### No añadir contextos innecesarios

- Los nombres **accountAddress** y **customerAddress** son perfectos para instancias de la clase **Address** pero no sirven como nombres de clase. **Address** sirve como nombre de clase.

## Capítulo 3: Funciones

[3-1]

```java
public static String testableHtml(
    PageData pageData,
    boolean includeSuiteSetup
) throws Exception {
    WikiPage wikiPage = pageData.getWikiPage();
    StringBuffer buffer = new StringBuffer();
    if (pageData.hasAttribute("Test")) {
        if (includeSuiteSetup) {
            WikiPage suiteSetup =
                PageCrawlerImpl.getInheritedPage(
                    SuiteResponder.SUITE_SETUP_NAME, wikiPage
                );
            if (suiteSetup != null) {
                WikiPagePath pagePath =
                    suiteSetup.getPageCrawler().getFullPath(suiteSetup);
                String pagePathName = PathParser.render(pagePath);
                buffer.append("!include -setup .")
                    .append(pagePathName)
                    .append("\n");
            }
        }
        WikiPage setup =
            PageCrawlerImpl.getInheritedPage("SetUp", wikiPage);
        if (setup != null) {
            WikiPagePath setupPath =
                wikiPage.getPageCrawler().getFullPath(setup);
            String setupPathName = PathParser.render(setupPath);
            buffer.append("!include -setup .")
                .append(setupPathName)
                .append("\n");
        }
    }
    buffer.append(pageData.getContent());
    if (pageData.hasAttribute("Test")) {
        WikiPage teardown =
            PageCrawlerImpl.getInheritedPage("TearDown", wikiPage);
        if (teardown != null) {
            WikiPagePath tearDownPath =
                wikiPage.getPageCrawler().getFullPath(teardown);
            String tearDownPathName = PathParser.render(tearDownPath);
            buffer.append("\n")
                .append("!include -teardown .")
                .append(tearDownPathName)
                .append("\n");
            if (includeSuiteSetup) {
                WikiPage suiteTeardown =
                    PageCrawlerImpl.getInheritedPage(
                        SuiteResponder.SUITE_TEARDOWN_NAME,
                        wikiPage
                    );
                if (suiteTeardown != null) {
                    WikiPagePath pagePath =
                        suiteTeardown.getPageCrawler().getFullPath(suiteTeardown);
                    String pagePathName = PathParser.render(pagePath);
                    buffer.append("!include -teardown .")
                        .append(pagePathName)
                        .append("\n");
                }
            }
        }
        pageData.setContent(buffer.toString());
        return pageData.getHtml();
    }
```

[3-2]

``` java
public static String renderPageWithSetupsAndTeardowns(
    PageData pageData, boolean isSuite
) throws Exception {
    boolean isTestPage = pageData.hasAttribute("Test");
    if (isTestPage) {
        WikiPage testPage = pageData.getWikiPage();
        StringBuffer newPageContent = new StringBuffer();
        includeSetupPages(testPage, newPageContent, isSuite);
        newPageContent.append(pageData.getContent());
        includeTeardownPages(testPage, newPageContent, isSuite);
        pageData.setContent(newPageContent.toString());
    }
    return pageData.getHtml();
}
```

### Tamaño reducido

- La primera regla de las funciones es que debe ser de tamaño reducido.
- La segunda es que debe ser todavía más reducida.
- Las funciones deben tener una longitud aproximada de 20 líneas.
- Deberían tener el tamaño de 3-3

[3-3]

``` Java
public static String renderPageWithSetupsAndTeardowns(
    PageData pageData, boolean isSuite) throws Exception {
    if (isTestPage(pageData))
        includeSetupAndTeardownPages(pageData, isSuite);
    return pageData.getHtml();
}
```

### Bloques y Sangrado

- En los bloques de instrucción **if**, **else**, **while** y similares deben tener una línea de longitud que, seguramente, sea la invocación a una función.
- De esta forma se reduce el tamaño y añade valor documental, ya que la función tendrá un nombre descriptivo.
- El nivel de sangrado de una función no debe ser mayor de uno o dos.

### Hacer una cosa

- Es evidente que [3-1] hace más de una cosa, crea búfers, obtiene páginas, busca páginas heredades, añade cadenas antiguas y genera HTML.
- **Las funciones solo deben hacer una cosa. Deben hacerlo bien y debe ser lo único que hagan.**
- El problema de esta afirmación es saber qué es una cosa. ¿El fragmento [3-3] hace una cosa? Se podría pensar que hace tres:
  - Determinar si la página. es una página de test.
  - En caso afirmativo, incluir configuraciones y detalles.
  - Representar la página en HTML.
- Los tres pasos de la función se encuentran en un nivel de abstracción por debajo del nombre de la función. Podemos describir la función como un breve párrafo **TO (Para)**.
- **Si una función solo realiza los pasos situados un nivel por debajo del nombre de la función, entonces hace una cosa.**
- **Creamos funciones para descomponer conceptos más amplios (el nombre de la función) en un conjunto de pasos en el siguiente nivel de abstracción.**

### Secciones en funciones

- Fíjese en [4-7] la función generatePrimes se divide en secciones como declaraciones, inicialización y filtros.  Es un síntoma evidente que hace más de una cosa.
- **Las funciones que hacen una sola cosa, no se pueden dividir en secciones.**

### Un nivel de abstracción por función

- Para que las funciones realicen **una sola cosa**, asegúrese de que las instrucciones de la función se encuentran en el mismo nivel de abstracción.
- La mezcla de niveles de abstracción en una función siempre resulta confusa. Los lectores no sabrán si una determinada expresión en un concepto esencial o un detalle.

### Leer código de arriba a abajo: La regla descendente

- Queremos que tras todas las funciones aparezcan las del siguiente nivel de abstracción para poder leer el programa, descendiendo un nivel de abstracción por vez mientras leemos la listas de funciones.
- Vea [3-7] utiliza este principio. Cada función presenta a la siguiente y se mantiene en un nivel de abstracción coherente.

### Instrucciones Switch

- Por naturaleza las funciones switch hacen N cosas.
- No siempre podemos evitarlas, pero podemos asegurarnos de incluirlas en una clase de nivel inferior y de no repetirlas. Para ello utilizaremos polimorfismo.

[3-4]

``` java
public Money calculatePay(Employee e)
throws InvalidEmployeeType {
    switch (e.type) {
        case COMMISSIONED:
            return calculateCommissionedPay(e);
        case HOURLY:
            return calculateHourlyPay(e);
        case SALARIED:
            return calculateSalariedPay(e);
        default:
            throw new InvalidEmployeeType(e.type);
    }
}
```

- Esta función tiene varios problemas. Es de gran tamaño y cuando se agreguen nuevos tipos de empleados, aumentará más.
- Hace más de una cosa.
- Incumple el principio SRP (*Single Responsibility Principle*), ya que tiene más de un motivo para cambiar.
- También incumple el principio OCP (*Open Closed Principle*), ya que debe cambiar cuando añadan nuevos tipos.
- **La solución al problema [3-5] consiste en ocultar la instrucción *switch* en una *ABSTRACT FACTORY* e impedir que nadie la vea. La FACTORY usa la instrucción *switch* para crear las instancias adecuadas de los derivados de Employee y las distintas funciones, como *calculatePay*, *isPayday* y *deliverPay*, se entregarán de forma polimórfica a través de la interfaz Employee.**

[3-5]

```java
public abstract class Employee {
    public abstract boolean isPayday();
    public abstract Money calculatePay();
    public abstract void deliverPay(Money pay);
}
-----------------
    public interface EmployeeFactory {
public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType;
}
-----------------
public class EmployeeFactoryImpl implements EmployeeFactory {
    public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType {
        switch (r.type) {
            case COMMISSIONED:
                return new CommissionedEmployee(r);
            case HOURLY:
                return new HourlyEmployee(r);
            case SALARIED:
                return new SalariedEmploye(r);
            default:
                throw new InvalidEmployeeType(r.type);
        }
    }
}
```

- Las instrucciones *switch* solo se toleran si aparecen una vez, se usan para crear objetos polimórficos y se ocultan tras una herencia para que el resto del sistema no las pueda ver.

### Usar nombres descriptivos

- Cuanto más reducida y concreta sea una función, más fácil va a ser elegir un nombre descriptivo.
- No tema a los nombres extensos.
- No tema dedicar tiempo a elegir un buen nombre. Es más, debería probar con varios nombres y leer el código con todos ellos.

### Argumentos de funciones

- El número ideal de argumentos para una función es cero. Después uno y dos.
- Evite utilizar tres argumentos, y más de ellos, requieren una justificación especial y no es muy habitual.
- El argumento se encuentra en un nivel de abstracción diferente que el nombre de la función y nos obliga a conocer un detalle que no es especialmente importante en ese momento.
- Los argumentos son todavía más complicados desde el punto de vista de pruebas.
- Con más de dos argumentos, probar cada combinación de valores adecuados es todo un reto.
- Los argumentos de salida son más difíciles de entender que lo de entrada. Al leer una función, estamos acostumbrados al concepto de información entrante por argumento y saliente por valor devuelto. 
- Los argumentos de salida suelen obligarnos a realizar una comprobación doble.

### Formas monádicas habituales

- Hay dos motivos principales para pasar un solo argumento a una función.
  - Puede que realice una pregunta sobre el argumento, como en fileExists("MyFile").
  - O que procese el argumento, lo transforme en otra cosa y lo devuelva, como fileOpen("MyFile")
- Una forma menos habitual pero muy útil para un argumento es un evento.
- Si una función va a transformar su valor de entrada, la transformación debe aparecer como valor devuelto.

### Argumentos de indicador

- Pasar un valor Booleano a una función es una practica totalmente desaconsejable.
- Indica que la función hace más de una cosa.

### Funciones diádicas

- 

### Triadas

- 

### Objetos de argumento

- Cuando una función parece necesitar dos o más argumentos , es probable que alguno de ellos se incluya en una clase propia.

### Listas de argumentos

- Si los argumentos variables se procesan de la misma forma, serán equivalentes a un único argumento del tipo List.

### Verbos y palabras clave

- 

### Sin efectos secundarios

- Su función promete hacer una cosa, pero en realidad también hace otras cosas ocultas.
- Ejemplo, [3-6], el efecto secundario es la invocación de Sessión.initialize()

[3-6]

``` java
public class UserValidator {
    private Cryptographer cryptographer;
    public boolean checkPassword(String userName, String password) {
        User user = UserGateway.findByName(userName);
        if (user != User.NULL) {
            String codedPhrase = user.getPhraseEncodedByPassword();
            String phrase = cryptographer.decrypt(codedPhrase, password);
            if ("Valid Password".equals(phrase)) {
                Session.initialize();
                return true;
            }
        }
        return false;
    }
}
```

### Argumentos de salida

- Obligan a comprobar la declaración de la función.
- Los argumentos de salida deben evitarse, si su función tiene que cambiar el estado de un elemento, haga que cambie el estado de su objeto contenedor.

### Command Query Sepatarion (CQS)

- La solución es separar el comando de la consulta para evitar la ambiguedad.

``` java
if (attributeExists("username")) {
	setAttribute("username", "unclebob");
	...
}
```

### Prefer exception to returning error codes

- Devolver códigos de error de funciones de comando es un sutil imcumplimiento de la separación de comandos de consulta (CQS).
- Genera estructuras anidadas.

``` java
if (deletePage(page) == E_OK) {
	if (registry.deleteReference(page.name) == E_OK) {
		if (configKeys.deleteKey(page.name.makeKey()) == E_OK){
			logger.log("page deleted");
		} else {
			logger.log("configKey not deleted");
        }
	} else {
		logger.log("deleteReference from registry failed");
	}
} else {
	logger.log("delete failed");
	return E_ERROR;
}
```

- Si usa excepciones en lugar de código de error.

``` java
try {
	deletePage(page);
	registry.deleteReference(page.name);
	configKeys.deleteKey(page.name.makeKey());
}
catch (Exception e) {
	logger.log(e.getMessage());
}
```

## Límites

### Explorar y aprender límites

- Pruebas que analicen nuestro entendimiento del codigo de terceros.
- Pruebas de aprendizaje según Jim Newkirk.
- Encapsular ese conocimiento en nuestra propia clase para que el resto de la aplicación se aisle de la interfaz de limite Ej: Log4Net.

### Las pruebas de aprendizaje son algo más que gratuitas.

- Las pruebas de aprendizaje son experimentos precisos que permiten aumentar nuestro conocimientos.
- Cuando aparezcan nuevas versiones del paquete de terceros, ejecutamos las pruebas de aprendizaje para comprobar si hay diferencias de comportamiento.
- Demuestran que los paquetes de terceros funcionan de la manera esperada.
- Si el paquete de terceros cambia de una forma incompatible con nuestras pruebas, lo sabremos al instante.
- Sin estas pruebas de límite para facilitar la transición, podríamos conservar la versión antigua más tiempo del necesario.

### Usar código que todavía no existe

- Básicamente propone utilizar un adaptar, y a su vez se puede utilizar un fake.

## Capítulo 9: Unit Test

### Las tres leyes de TDD

Todo sabemos que TDD nos pide que primero creemos las pruebas de unidad, antes que el código de producción.

#### Primera Ley

- No debe crear código de producción hasta que haya creado una prueba de unidad que falle.

#### Segunda Ley

- No debe crear más de una prueba de unidad que baste como fallida y no compilar se considera un fallo.

#### Tercera Ley

- No debe crear más código de producción que en necesario para superar la prueba de fallo actual.

### Keeping Test Clean

- El código de prueba es tan importante como el de producción.
- Sin una suite de pruebas no se puede asegurar que los cambios de una parte del sistema no afectan a otra.
- No se puede garantizar el funcionamiento esperado de los cambios en el código.

### Test Enable the -ilities

- El Unit Test es el que hace que el código sea flexible, se pueda mantener y reutilizar.

### Clean Test

