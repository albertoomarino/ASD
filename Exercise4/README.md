# RELAZIONE ESERCIZIO 4

## REQUISITI

Si implementi una libreria che realizza la struttura dati Grafo in modo che **sia ottimale per dati sparsi**
(IMPORTANTE: le scelte implementative che farete dovranno essere giustificate in relazione alle nozioni presentate
durante le lezioni in aula). La struttura deve consentire di rappresentare sia grafi diretti che grafi non diretti
(suggerimento:  un grafo non diretto può essere rappresentato usando un'implementazione per grafi diretti modificata
per garantire che, per ogni arco (a,b), etichettato w, presente nel grafo, sia presente nel grafo anche l'arco (b,a),
etichettato w. Ovviamente, il grafo dovrà mantenere l'informazione che specifica se esso è un grafo diretto o non diretto.).

L'implementazione deve essere generica sia per quanto riguarda il tipo dei nodi, sia per quanto riguarda le etichette
degli archi.

La struttura dati implementata dovrà offrire (almeno) le seguenti operazioni (accanto a ogni operazione è specificata la
complessità richiesta; n può indicare il numero di nodi o il numero di archi, a seconda del contesto):

* Creazione di un grafo vuoto – O(1)
* Aggiunta di un nodo – O(1)
* Aggiunta di un arco – O(1)
* Verifica se il grafo è diretto – O(1)
* Verifica se il grafo contiene un dato nodo – O(1)
* Verifica se il grafo contiene un dato arco – O(1)  (*)
* Cancellazione di un nodo – O(n)
* Cancellazione di un arco – O(1)  (*)
* Determinazione del numero di nodi – O(1)
* Determinazione del numero di archi – O(n)
* Recupero dei nodi del grafo – O(n)
* Recupero degli archi del grafo – O(n)
* Recupero nodi adiacenti di un dato nodo – O(1)  (*)
* Recupero etichetta associata a una coppia di nodi – O(1) (*)

(*) quando il grafo è veramente sparso, assumendo che l'operazione venga effettuata su un nodo la cui lista di adiacenza ha una lunghezza in O(1).


---

## IMPLEMENTAZIONE

Per l'implementazione dell'esercizio 4 sono state sviluppate le seguenti funzioni:

* **add_vertex :** inserisce un nuovo vertice ì, se non ancora esistente e lo aggiunge alla HashMap; 
* **add_arch :** crea un nuovo arco dalla sorgente alla destinazione passati come paramentri , se il grafo è bidirezionale viene creata una copia nell'altro senso .
* **is_bidirect :** ritorna true se il grafo è non orientato e false altrimenti .
* **has_already_Vertex :**  funzione di appoggio per controllare se un vertice è gia presente nel grafo
* **has_already_Arch :** funzione di appoggio per controllare se un'arco è gia presente nel grafo
* **remove_vertex :** rimuove un vertice passato da parametro
* **remove_arch :** rimuove un arco avente destinazione e partenza come quelle pasate da paramentri
* **get_number_vertex :** restituisce il numero di vertici all'interno del grafo
* **get_number_arch :** restituisce il numero di archi all'interno del grafo
* **get_vertex :** restituisce la lista dei vertici presenti nel grafo 
* **get_arch :** restituisce la lista degli archi presenti nel grafo
* **adj_list_of :** restituisce una lista di vertici adiacenti al nodo passato come parametro
* **get_w_btw:** ritorna il peso di due archi aventi destinazione e partenza uguali a quelle passate come paremtro .
* **minPath:** applica l'algoritmo di dijkstra su un grafo individuando il cammino minimo per quest'ultimo sfruttando la struttura dati implementata nell'esercizio 3.


---

## COMANDI PER LA COMPILAZIONE E PER L'ESECUZIONE

***COMPILAZIONE***

Posizionarsi fuori dalla cartella ***Exercise4***

Digitare:

    javac -classpath .;Resources/Java/JUnit/hamcrest-core-1.3.jar.;Resources/Java/JUnit/junit-4.12.jar Exercise4/Graph_unit_test.java

Digitare:

    javac -classpath .;Resources/Java/JUnit/hamcrest-core-1.3.jar.;Resources/Java/JUnit/junit-4.12.jar Exercise4/Graph_test_run.java

***ESECUZIONE***

Digitare:

    java -classpath .;Resources/Java/JUnit/hamcrest-core-1.3.jar.;Resources/Java/JUnit/junit-4.12.jar Exercise4/Graph_test_run.java

***ESECUZIONE DEL MAIN***

Digitare:

    javac -classpath .;Resources/Java/JUnit/hamcrest-core-1.3.jar.;Resources/Java/JUnit/junit-4.12.jar Exercise4/Main.java

Digitare:

    java -classpath .;Resources/Java/JUnit/hamcrest-core-1.3.jar.;Resources/Java/JUnit/junit-4.12.jar Exercise4/Main
