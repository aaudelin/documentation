# Mémoire : stack (pile) et heap (tas)

La pile est utilisée pour du stockage dit statique contrairement au tas qui lui propose un stockage plus dynamique. Les données sont conservées en RAM dans les 2 cas.

## Stack (pile)

Liée au thread, la pile permet de stocker la donnée de manière statique.

Ainsi, lors d'un appel d'une fonction un espace est aloué et est empilé sur la pile. Cet espace contient toutes les variables locales à la méthode.

La pile fontionne selon le principe FILO, ainsi plus l'emplacement créé est récent plus il sera supprimé rapidement. En outre, l'accès à la donnée est rapide.

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

### Garbage Collector

La garbage collector est lié au tas. Celui-ci parcourt les données du tas et supprime les objets qui ne sont plus référencés.

## Source



The stack is the memory set aside as scratch space for a thread of execution.  When a function is called, a block is reserved on the top of the stack for local variables and some bookkeeping data.  When that function returns, the block becomes unused and can be used the next time a function is called.  The stack is always reserved in a LIFO (last in first out) order; the most recently reserved block is always the next block to be freed.  This makes it really simple to keep track of the stack; freeing a block from the stack is nothing more than adjusting one pointer.

The heap is memory set aside for dynamic allocation.  Unlike the stack, there's no enforced pattern to the allocation and deallocation of blocks from the heap; you can allocate a block at any time and free it at any time.  This makes it much more complex to keep track of which parts of the heap are allocated or free at any given time; there are many custom heap allocators available to tune heap performance for different usage patterns.

Each thread gets a stack, while there's typically only one heap for the application (although it isn't uncommon to have multiple heaps for different types of allocation).

To answer your questions directly:  

> _To what extent are they controlled by the OS or language runtime?_

The OS allocates the stack for each system-level thread when the thread is created.  Typically the OS is called by the language runtime to allocate the heap for the application.

> _What is their scope?_

The stack is attached to a thread, so when the thread exits the stack is reclaimed.  The heap is typically allocated at application startup by the runtime, and is reclaimed when the application (technically process) exits.

> _What determines the size of each of them?_  

The size of the stack is set when a thread is created.  The size of the heap is set on application startup, but can grow as space is needed (the allocator requests more memory from the operating system).

> _What makes one faster?_
  
The stack is faster because the access pattern makes it trivial to allocate and deallocate memory from it (a pointer/integer is simply incremented or decremented), while the heap has much more complex bookkeeping involved in an allocation or deallocation.  Also, each byte in the stack tends to be reused very frequently which means it tends to be mapped to the processor's cache, making it very fast. Another performance hit for the heap is that the heap, being mostly a global resource, typically has to be multi-threading safe, i.e. each allocation and deallocation needs to be - typically - synchronized with "all" other heap accesses in the program.

A clear demonstration:
![][1]
Image source: [vikashazrati.wordpress.com](http://vikashazrati.wordpress.com/2007/10/01/quicktip-java-basics-stack-and-heap/)

  [1]: https://vikashazrati.files.wordpress.com/2007/10/stacknheap.png

## Autres liens

* [Lien stack overflow](https://stackoverflow.com/questions/79923/what-and-where-are-the-stack-and-heap)
* [Vidéo tutoriel java](https://www.youtube.com/watch?v=UcPuWY0wn3w)
* [Vidéo imagée java](https://www.youtube.com/watch?v=ckYwv4_Qtmo)