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
- **ommon Annotations (JSR 250)**
