# DOCUMENTAZIONE TEORICA - SPRING E SPRING BOOT

## BUILD AUTOMATION E MAVEN

### BUILD AUTOMATION
Pratica fondamentale nello sviluppo software che consiste nell'**automazione di tutti i compiti necessari** per **trasformare il codice sorgente scritto dagli sviluppatori in un prodotto software eseguibile** e pronto per l'uso.

In pratica, la build automation **gestisce una serie di operazioni che tradizionalmente sarebbero state eseguite manualmente**, tra cui:

- **Compilazione del codice sorgente**
- **Risoluzione delle dipendenze**
- **Esecuzione di test**
- **Packaging**: Impacchettare il codice compilato e le risorse necessarie in un formato distribuibile (es. file .jar, .zip, immagini Docker, installer).
- **Generazione di documentazione**: Creare automaticamente documentazione, report o note di rilascio.
- **Deployment (o distribuzione)**: Preparare il software per essere installato o rilasciato in diversi ambienti (sviluppo, test, produzione).

### BUILD AUTOMATION TOOL
I **Build Automation Tools** sono software progettati per automatizzare le varie fasi del processo di "costruzione" di un software, quindi software che applicano la **build automation**.

#### Esempi di Build Automation Tools:

**Generici / Multi-linguaggio / CI/CD Servers**:

- **Jenkins**: Uno dei più popolari server di automazione open-source, estremamente flessibile e con un vastissimo ecosistema di plugin. Permette di creare pipeline di build, test e deployment molto complesse.
- **AWS CodeBuild / Google Cloud Build / Azure DevOps**: Servizi di build gestiti offerti dai principali provider cloud, integrati con i rispettivi ecosistemi.

**Specifici per Linguaggio/Ecosistema**:

- **Apache Maven (Java)**: Uno strumento molto diffuso per progetti Java, basato sul concetto di "convention over configuration". Gestisce la compilazione, il testing, il packaging e la gestione delle dipendenze.
- **Gradle (Java, Kotlin, Android, altri)**: Più moderno e flessibile di Maven, usa un DSL (Domain Specific Language) basato su Groovy o Kotlin per le configurazioni, offrendo maggiore programmabilità. Molto usato nello sviluppo Android.
- **Make / CMake / GNU Make (C/C++)**: Strumenti tradizionali per compilare codice C/C++, specialmente in ambienti Unix-like. Richiedono la scrittura di "Makefile".
- **MSBuild (.NET/C#)**: Il sistema di build di Microsoft per progetti .NET, basato su file XML.
- **NPM / Yarn (JavaScript/Node.js)**: Sebbene siano primariamente gestori di pacchetti, includono anche funzionalità per definire e eseguire script di build (es. npm run build).
- **Pip (Python)**: Principalmente un gestore di pacchetti, ma in Python la "build" è spesso più semplice e può coinvolgere script Python stessi o setuptools.


### MAVEN

Maven è uno **strumento open source di build automation** realizzato dalla Apache Software Foundation, utilizzato principalmente per **gestire progetti Java**.

#### FILE POM

è un file XML che contiene tutte le informazioni del progetto (definizione, dipendenze , test).
Gli elementi indispensabili di un POM sono:
- groupId
- artifactId
- version
Sono tutti campi obbligatori.

I tre campi insieme consentono di identificare univocamente un progetto in un repository

#### Dependency

Una delle principali funzionalità di Maven è la gestione delle dipendenze di un progetto, cioè le librerie di cui necessita il nostro progetto per funzionare correttamente (ad es. log4j, apache commons,...)

Se una risorsa è esterna (ad es. log4j), Maven la scarica in automatico dai repository che abbiamo configurato e le utilizza durante la build del progetto. Se la risorsa richiesta ha bisogno di altre risorse (dipendenza transitiva), Maven le scarica in autonomia e le utilizza durante la build.

#### Plugin
sono la caratteristica centrale di Maven e consentono l’esecuzione di una serie di operazioni (ad
es. compilazione, deploy , packaging, test.


## SPRING

### COSA E'

Spring (più precisamente Spring Framework) è un **framework open-source per lo sviluppo di applicazioni su piattaforma Java**. È diventato uno degli strumenti più popolari e ampiamente utilizzati nel mondo Java, in particolare per la creazione di **applicazioni enterprise, microservizi e applicazioni web**.

Le caratteristiche principali di Spring sono l'**inversion of Control**, la **Dependency Injection** e la **programmazione orietata agli aspetti (AOP)**.

Alcuni tendono a considerare il framework Spring e Java EE in concorrenza. Tuttavia possiamo affermare che: **Spring è complementare a Java EE**.

Il framework Spring **non utilizza le specifiche Java EE** ma **si integra con alcune di esse**, in particolare:
- **Servlet API (JSR 340)**
- **WebSocket API (JSR 356)**
- **Concurrency Utilities (JSR 236)**
- **JSON Binding API (JSR 367)**
- **Bean Validation (JSR)**
- **JPA (JSR)**
- **JMS (JSR 914)**

Spring supporta anche queste due specifiche che lo sviluppatore può utilizzare al posto dei meccanismi forniti dal
framework Spring:

- **Dependency Injection (JSR 330)**
- **Common Annotations (JSR 250)**

### COME FUNZIONA

#### MODULI

L’ecosistema Spring è costituito da tanti **moduli** , ognuno dei quali assolve a determinate funzioni.
Un modulo Spring è semplicemente un **file JAR** che contiene una **serie di classi ed interface che definiscono
ed implementano le funzionalità del modulo**.
Per utilizzare una determinata funzione (ad esempio le interfacce di connessione ad DB), è sufficiente **importare
nella nostra applicazione il modulo che la implementa**.

<img width="720" height="540" alt="spring-overview" src="https://github.com/user-attachments/assets/8952b861-4803-4d5d-89ad-92c997ad0dd8" />

- **spring-core**: È il **modulo principale che ogni applicazione Spring deve includere**.
Il modulo **contiene tutte le classi condivise dagli altri moduli Spring** (ad es. le classi per accedere ai file di
configurazione). Il modulo contiene anche una **serie di classi di utility utilizzate nei moduli Spring** e che possiamo utilizzare anche nella tua applicazione (ad es. la classe NumberUtils che tra le altre cose consente di fare il parsing di
una string in un numero mediante il metodo statico parseNumber String text, Class<T> targetClass)).

- **spring-oap**: Questo modulo contiene le **classi necessarie per utilizzare le funzionalità AOP di Spring** (modularizzare le preoccupazioni trasversali (come la registrazione, la sicurezza, le transazioni) separandole dal codice dell'applicazione principale).
Questo modulo va importato anche se è necessario utilizzare altre funzionalità in Spring che utilizzano AOP (ad esempio il modulo per la gestione delle transizioni).

- **spring-beans**: Questo modulo contiene le classi per gestire i bean Spring.

- **spring-context**: Il modulo contiene le classi che forniscono molte estensioni al modulo core. Ad esempio, tutte le classi utilizzano la funzionalità ApplicationContext di Spring. Il modulo contiene anche le classi per l'integrazione Enterprise JavaBeans (EJB), Java Naming and Directory Interface (JNDI) e Java Management Extensions (JMX).

- **spring-jdbc**: Il modulo contiene leclassi per il supporto JDBC ed è necessario per le applicazioni che richiedono l'accesso al database.

- **spring-orm**: Il modulo estende le funzionalità del modulo spring jdbc implementando il supporto ai pi ù diffusi strumenti ORM Hibernate , JDO, JPA e iBATIS). Questo modulo utilizza molte classi implementate nel modulo spring jdbc.

- **spring-web**: Il modulo contiene le classi principali per l'utilizzo di Spring nelle applicazioni Web, tra cui le classi per gestire l’upload di file, elaborare la query string , ecc

- **spring-webflux**: Questo modulo contiene le classi da necessarie per implementare applicazioni web con Spring Web Reactive.

- **spring-webmvc**: Il modulo contiene le classi per utilizzare il framework MVC di Spring.

### DEPENDENCY (DIPENDENZE)

Nel contesto di Spring, una `dipendenza` è **un oggetto (o "bean") di cui un altro oggetto ha bisogno per svolgere le proprie funzionalità**.

```java
// La "dipendenza": l'oggetto di cui Lettore ha bisogno
class File {
    String getContent() {
        return "Contenuto del file.";
    }
}

// L'oggetto che ha la dipendenza
class Lettore {
    private File file; // <--- Il "File" è la dipendenza del "Lettore"

    public Lettore() {
        this.file = new File(); // Il Lettore crea e gestisce la sua dipendenza
    }

    public void leggi() {
        System.out.println(file.getContent());
    }

    public static void main(String[] args) {
        Lettore lettore = new Lettore();
        lettore.leggi(); // Output: Contenuto del file.
    }
}
```

In questo esempio, la classe `Lettore` dipende dalla classe `File` per poter eseguire il suo compito di lettura. Senza un `File`, il `Lettore` non può funzionare.

### INVERTION OF CONTROL (IoC)

L'Inversion of Control (IoC) in Spring è un principio di progettazione fondamentale che ribalta il modo tradizionale in cui gli oggetti gestiscono le proprie dipendenze, **trasferendo il controllo di oggetti o porzioni di programma al conteiner o al framework**.

In particolare, invece che un oggetto **crei direttamente le sue dipendenze** (cioè gli altri oggetti o servizi di cui ha bisogno), è **il container IoC di Spring a farsi carico di questo compito**. Il container si occupa di **instanziare gli oggetti, configurarli e iniettare le dipendenze necessarie**, liberando l'oggetto dalla responsabilità di cercarle o crearle autonomamente. Questo porta a un **disaccoppiamento maggiore tra le classi**, rendendole **più modulari, riutilizzabili e facili da testare**. 


L'invertion of Control può essere ottenuta utilizzando vari design pattern:
- **Service Locator pattern**
- **Factory pattern**
- **Dependency Injection pattern (DI)**

Il modo più comune in cui Spring implementa l'IoC è tramite la Dependency Injection (DI).


- **Programmazione Tradizionale (Senza IoC/DI)**

```java
// Interfaccia del motore di stampa
interface PrinterEngine {
    void print(String document);
}

// Implementazione concreta del motore di stampa laser
class LaserPrinterEngine implements PrinterEngine {
    @Override
    public void print(String document) {
        System.out.println("Stampa LASER del documento: '" + document + "'");
    }
}

// Classe che stampa documenti - Tradizionale
class DocumentPrinterTraditional {
    private PrinterEngine engine; // La dipendenza

    public DocumentPrinterTraditional() {
        // Il controllo della creazione dell'oggetto è QUI, all'interno della classe
        this.engine = new LaserPrinterEngine(); // Accoppiamento forte!
    }

    public void printDocument(String document) {
        engine.print(document);
    }

    public static void main(String[] args) {
        DocumentPrinterTraditional printer = new DocumentPrinterTraditional();
        printer.printDocument("Report Finanziario 2024");
    }
}
```
- **Inversion of Control (Tramite Spring e Dependency Injection)**

```java
// Uguale a prima
interface PrinterEngine {
  void print(String doc);
}
class LaserPrinterEngine implements PrinterEngine {
    @Override
    public void print(String doc) {
      System.out.println("Stampa LASER (via IoC): " + doc);
    }
}
class InkjetPrinterEngine implements PrinterEngine { // Una scelta alternativa
    @Override
    public void print(String doc) {
      System.out.println("Stampa INKJET (via IoC): " + doc);
    }
}

class DocumentPrinterIoC {
    private PrinterEngine engine; // Solo dichiarazione della dipendenza

    public DocumentPrinterIoC(PrinterEngine engine) {
        this.engine = engine; // **Controllo invertito**: la dipendenza viene iniettata
    }
    public void printDocument(String doc) {
      engine.print(doc);
    }
}

@Configuration // Configurazione per Spring
class SpringConfig {
    @Bean // Spring userà questo metodo per creare l'istanza di PrinterEngine
    public PrinterEngine getPrinterEngine() {
        return new LaserPrinterEngine(); // Qui si decide quale implementazione usare
        // return new InkjetPrinterEngine(); // Per cambiare, basta modificare questa riga!
    }
    @Bean
    public DocumentPrinterIoC documentPrinter(PrinterEngine engine) { // Spring inietta il PrinterEngine
        return new DocumentPrinterIoC(engine);
    }
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(SpringConfig.class);
        DocumentPrinterIoC printer = context.getBean(DocumentPrinterIoC.class);
        printer.printDocument("Report B");
    }
}
```

### Dependency Injection

Il pattern Dependecy Injection è un design pattern utilizzato per implementare l'IoC. Esso **consente la creazione e l'associazione degli oggetti fuori dalla classe che li utilizza**. 

Il pattern DI può essere implementato in tre modi:
- **Constructor Injection**
```java
public class Biblioteca {
    private BibliotecaService service;

    // Questa è la Constructor Injection: la dipendenza 'service' viene fornita dall'esterno come argomento
    public Biblioteca(BibliotecaService serv) {
        super();
        service = serv;
    }

    public List<Libro> getLibriDisponibili() {
        return service.getLibriDisponibili();
    }
}

public class BibliotecaFactory {
    public static Biblioteca getBiblioteca() {
        // Qui la factory crea la dipendenza (BibliotecaServiceImpl) e la inietta nel costruttore di Biblioteca
        Biblioteca b = new Biblioteca(new BibliotecaServiceImpl());
        return b;
    }
}

public class Main {
    public static void main (String[] args){
        BibliotecaFactory.getBiblioteca().getLibriDisponibili();
    }
}
```
- **Setter Injection**
```java
public class Biblioteca {
    private BibliotecaService service;

    public Biblioteca() {
        super();
    }

    // Questa è la Setter Injection: la dipendenza 'service' viene iniettata tramite un metodo setter pubblico.
    public void setService(BibliotecaService service) {
        this.service = service;
    }

    public List<Libro> getLibriDisponibili() {
        return service.getLibriDisponibili();
    }
}

public class BibliotecaFactory {
    public static Biblioteca getBiblioteca() {
        Biblioteca b = new Biblioteca();
        b.setService(new BibliotecaServiceImpl());
        return b;
    }
}

public class Main {
    public static void main (String[] args){
        BibliotecaFactory.getBiblioteca().getLibriDisponibili();
    }
}
```

Esiste anche la **Interface Injection**, ma Spring implementa solo Constructor e Setter Injection.

### IoC e DI in Spring

I moduli che contengono le classi e le intefacce **necessarie per implementare l'IoC** in Spring sono:

- **spring-beans**
- **spring-core**

La componente Spring che si occupa di creare istanze e configurare gli oggetti si chiama **IoC container**.

Gli oggetti creati dall’IoC Container sono chiamati **beans** e sono configurati utilizzando metadati che possono essere file XML, Java annotations o codice Java. Il container si occupa di iniettare le dipendenze quando crea il bean.

L’interfaccia BeanFactory mette a disposizione un meccanismo efficace di configurazione che consente di
gestire oggetti Java di qualsiasi tipo. 

Il modulo **spring-context**, basato sul modulo **spring-beans**, contiene sia l'interfaccia **BeanFactory** che l’interfaccia **ApplicationContext**, la quale eredita le funzionalità della BeanFactory e ne aggiunge altre.

Poiché l’interfaccia ApplicationContext include tutte le funzionalità di BeanFactory, è consigliato utilizzare
classi che implementano ApplicationContext.

Possiamo quindi concludere che i moduli necessari per realizzare l’IoC in Spring e che non devono mai mancare in un progetto Spring sono:

- **spring-beans**
- **spring-core**
- **spring-context**
