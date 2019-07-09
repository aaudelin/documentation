# Mémoire : stack (pile) et heap (tas)

Ces deux type de mémoire utilisent la RAM pour stocker la donnée. Lors du lancement de l'application un tas ainsi que plusieurs piles (1 par thread) sont allouées au contexte de l'application.

En java, on contrôle les dimensions de ces objets pour l'application grâce à :

* `'-Xmx'` : taille maximale du tas
* `'-Xms'` : taille initiale du tas
* `'-Xss'` : taille de la pile par thread
* `'-Xnoclassgc'` : désactive le garbage collector

## Stack (pile)

Liée au thread, la pile permet de stocker de la donnée relativement simple et liée à une fonction.

Ainsi, lors d'un appel d'une fonction un espace est aloué et est empilé sur la pile. Cet espace contient toutes les variables locales à la méthode.

La pile fontionne selon le principe FILO, ainsi plus l'emplacement créé est récent plus il sera supprimé rapidement. En outre, l'accès à la donnée est rapide.

Si la pile est surchargée, une erreur StackOverflow se produira. Cela peut être le cas pas exemple lors d'appels récursifs trop profonds ou de boucle infinie.

Exemple, dans le cas d'un programme java :

```java
public static void main(String[] args) {
    int var = 15;

    doSomething();
}

public void doSomething(String[] args) {
    long somethingVar = 26;
}
```

Description :

* Un emplacement est créé dans la pile lors de l'appel au `main()`
* Cet emplacement possède un espace réservé à `var`
* Lors de l'appel de `doSomething()` un nouvel emplacement est créé au sommet de la pile
* Ce dernier possède un espace réservé à `somethingVar`
* Lorsque l'appel à `doSomething()` est terminé, l'emplacement réservé à cette fonction est supprimé de la stack

## Heap (tas)

Le tas est un espace mémoire dynamique et est partagé entre les threads. Il est donc lié au contexte de l'application.

Le tas a un accès à la donnée un peu plus lent mais n'a de limite de taille que la capacité physique de la machine. Le tas contient donc la majeure partie des données de l'application notamment l'ensemble des objets dans le cas java.

Si trop d'objets sont créés ou bien que ceux-ci sont trop volumineux l'erreur OutOfMemory se produira.

Exemple, dans le cas d'un programme java :

```java
public static void main(String[] args) {
    int var = 15;

    doSomething();
}

public void doSomething(String[] args) {
    Employee employeeVar = new Employee(35);
}

class Employee {
    int age;

    public Employee(int pAge) {
        this.age = pAge;
    }
}
```

Description :

* Un emplacement est créé dans la pile lors de l'appel au `main()`
* Cet emplacement possède un espace réservé à la variable `var`
* Lors de l'appel de `doSomething()` un nouvel emplacement est créé au sommet de la pile
* Ce dernier possède un espace réservé à la variable `employeeVar`, cependant la valeur n'y est pas conservée il s'agit simplement d'une référence vers l'objet disponible dans le tas
* Une instance de la classe `Employee` est créée dans le tas et est référencée par `employeeVar`
* Cette instance possède une variable d'instance `age` valorisée à '35' dans le tas

## Garbage Collector

La garbage collector est lié au tas. Celui-ci parcourt les données du tas et supprime les objets qui ne sont plus référencés.

## Taille par défaut en Java

```bash
# Connaître les dimensions par défaut de la Stack
java -XX:+PrintFlagsFinal -version | grep -i 'StackSize'

# Connaître les dimensions par défaut de la Heap
java -XX:+PrintFlagsFinal -version | grep -i 'HeapSize'
```

## FAQ

Source : [Lien stack overflow][3]

> _To what extent are they controlled by the OS or language runtime?_

The OS allocates the stack for each system-level thread when the thread is created.  Typically the OS is called by the language runtime to allocate the heap for the application.

> _What is their scope?_

The stack is attached to a thread, so when the thread exits the stack is reclaimed.  The heap is typically allocated at application startup by the runtime, and is reclaimed when the application (technically process) exits.

> _What determines the size of each of them?_  

The size of the stack is set when a thread is created.  The size of the heap is set on application startup, but can grow as space is needed (the allocator requests more memory from the operating system).

> _What makes one faster?_
  
The stack is faster because the access pattern makes it trivial to allocate and deallocate memory from it (a pointer/integer is simply incremented or decremented), while the heap has much more complex bookkeeping involved in an allocation or deallocation.  Also, each byte in the stack tends to be reused very frequently which means it tends to be mapped to the processor's cache, making it very fast. Another performance hit for the heap is that the heap, being mostly a global resource, typically has to be multi-threading safe, i.e. each allocation and deallocation needs to be - typically - synchronized with "all" other heap accesses in the program.

A clear demonstration:
![Images of memory sockage][1]
Image source: [vikashazrati.wordpress.com](http://vikashazrati.wordpress.com/2007/10/01/quicktip-java-basics-stack-and-heap/)

## Sources

* [Lien stack overflow][3]
* [Vidéo tutoriel java][2]
* [Vidéo imagée java][4]
* [Image du stockage mémoire][1]

[1]: https://vikashazrati.files.wordpress.com/2007/10/stacknheap.png
[2]: https://www.youtube.com/watch?v=UcPuWY0wn3w
[3]: https://stackoverflow.com/questions/79923/what-and-where-are-the-stack-and-heap
[4]: https://www.youtube.com/watch?v=ckYwv4_Qtmo
