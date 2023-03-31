# RELAZIONE ESERCIZIO 3

## REQUISITI

Si implementi una libreria che realizza la struttura dati Heap Minimo. La struttura dati deve:
* rappresentare internamente lo heap tramite un vettore (è possibile usare anche altre strutture interne di supporto, se necessarie);
* consentire un numero qualunque e non noto a priori di elementi dello heap;
* essere generica per quanto riguarda il tipo degli elementi dello heap;
* essere generica per quanto riguarda il criterio di confronto fra elementi dello heap.

Essa deve, inoltre, offrire (almeno) le seguenti operazioni (accanto a ogni operazione è specificata la
complessità richiesta, in cui n indica il numero di elementi dello heap):
* creazione di uno heap minimo vuoto - O(1);
* inserimento di un elemento - O(log n);
* restituzione della dimensione dello heap - O(1);
* restituzione del genitore di un elemento - O(1);
* restituzione del figlio sinistro di un elemento - O(1);
* restituzione del figlio destro di un elemento - O(1);
* estrazione dell'elemento con valore minimo - O(1);
* diminuzione del valore di un elemento - O(log n).


---

## IMPLEMENTAZIONE

Per l'implementazione dell'esercizio 3 sono state sviluppate le seguenti funzioni e una classe interna di supporto per l'eventuale sviluppo del metodo di Dijkstra:


* **parent_value:** valore del genitore di Heap[i]
* **left_child_value:** valore del figlio sinistro di Heap[i]
* **right_child_value:** valore del figlio destro di Heap[i]
* **moveDown:** metodo che preserva condizione e struttura dell'heap minimo. Rimuove un elemento dalla testa e lo sostituisce con l'ultimo, preservandone le priorità spostando di conseguenza gli elementi
* **moveUp** metodo che preserva condizione e struttura dell'heap minimo. Aggiunge un elemento in fondo, preservando le priorità e spostando di conseguenza gli elementi
* **size:** ritorna il numero di elementi presenti nell'heap
* **isEmpty:** restituisce *true* se l'heap è vuoto
* **insert:** aggiunge l'elemento specificato nell'heap nella posizione corretta
* **rialloca:** ridimensiona la grandezza dell'Heap minimo.
* **decreasePriority:** restituisce il valore all'indice 0 e conserva la condizione dell'heap
* **getFirst:** restituisce l'elemento con la più alta priorità ovvero quello in radice.
* **remove:** rimuove l'elemento passato da parametro e richiamo moveDown per preservare la caratteristica dell'Heap minimo.
* **extractfirst:** rimuove e restituisce un elemento con la priorità più alta (quindi presente alla radice). restituisce *null* se la cosa è vuota


---

## COMANDI PER LA COMPILAZIONE E PER L'ESECUZIONE

***COMPILAZIONE***

Posizionarsi fuori dalla cartella ***Exercise3***

Digitare:

    javac -classpath .;Resources/Java/JUnit/hamcrest-core-1.3.jar.;Resources/Java/JUnit/junit-4.12.jar Exercise3/HeapPriorityQueueTest.java

Digitare:

    javac -classpath .;Resources/Java/JUnit/hamcrest-core-1.3.jar.;Resources/Java/JUnit/junit-4.12.jar Exercise3/HeapTestRunner.java

***ESECUZIONE***

Digitare:

    java -classpath .;Resources/Java/JUnit/hamcrest-core-1.3.jar.;Resources/Java/JUnit/junit-4.12.jar Exercise3/HeapTestRunner.java
