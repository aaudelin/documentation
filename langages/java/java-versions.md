# Java : suivi des versions

## Java 9

### Jigsaw : la modularité

Objectifs :

1. Réduire la taille des applications
    * IoT ou Cloud même si le stockage coute de moins en moins cher il faut minimiser la taille des projets installés sur les devices
    * N'embarque que les dépendances nécessaires
2. Renforcer la sécurité
    * Moins il y a de dépendances et moins de riques d'avoir une faille
    * Une faille donne accès à moins contenu
    * Possible de définir quels packages exporter
3. Rénover le classpath
    * Recherche de classe avec ClassPath est linéaire, pas très performant si beaucoup de dépendances (100 en moyenne)
    * Module path sous forme d'arbre

Contraintes :

1. Plus d’accès par défaut aux classes publiques d’un module
2. Plus d’introspection par défaut sur les classes d’un module
3. Plus de split packages
4. Plus de dépendances circulaires
5. Définir les dépendances dans les module-info et les outils de build

Implémentation : créer un fichier module-info.java à la racine de fr.myPackage

```java
Module fr.myPackage {
   requires spring.boot;
   exports fr.myPackage.packageToExport;
}
```

Les sources doivent être dans `src/fr.myPackage/fr/myPackage`

### Try with resources

Possible de déclarer des variables `Closeable` en dehors du try et de les utiliser dans le try. Possible uniquement si les variables sont finales ou effectivement finales.

```java
BufferedReader reader1 = getNewReader();
BufferedReader reader2 = new BufferedReader(new FileReader("fichier2.txt"));
BufferedReader reader3 = new BufferedReader(new FileReader("fichier3.txt"));
try (reader1; reader2; reader3) {
    System.out.println(reader1.readLine());
    System.out.println(reader2.readLine());
    System.out.println(reader3.readLine());
}
```

### Méthodes private dans les interfaces

Après static et default en java 8, le private permet :

* Permet de factoriser du code (répond partiellement au problème de l'héritage simple)
* Gérer l'encapsulation

### Création de collections

Permet de créer des collections immuables :

* `List.of()`
* `Set.of()`
* `Map.of()`

### Class process

1. Identifier plus facilement les process enfants
2. Avoir le PID du process
3. Snapshot des informations du process
4. Notif asynchrone : completable future

### VarHandle 

Permet d'avoir accès à des variables même sur des objets private 

```java
private static class Arbre {
    float taille;
}
static final VarHandle VH_ARBRE_FIELD_TAILLE;
static {
    try {
        VH_ARBRE_FIELD_TAILLE = MethodHandles.lookup()
                                             .in(Arbre.class)
                                             .findVarHandle(Arbre.class, "taille", float.class);
    } catch (Exception e) {
        throw new Error(e);
    }

// Utilisation
Arbre arbre = new Arbre();
arbre.taille = 3.4f;
System.out.println(VH_ARBRE_FIELD_TAILLE.get(arbre));
VH_ARBRE_FIELD_TAILLE.set(arbre, 4.0f);
System.out.println(VH_ARBRE_FIELD_TAILLE.get(arbre));
```

### Autres

* Opérateur diamant dans les classes anonymes internes
* `@SafeVarargs` utilisable sur les intances privées
* Amélioration API Stream
  * `takeWhile` -> conserve les éléments tant que la condition est respectée puis supprime toute la suite
  * `dropWhile` -> supprime les éléments tant que la conditions est respectée puis collecte toute la suite
  * `ofNullable` -> stream vide
  * `iterate` -> équivaut au for de i = X..Y
* API flow pour mise en place du pattern Reactive (publisher, subscriber, subscription, processor)
* Outils
  * JShell : ligne de commannde pour exécuter de code Java simplifiée
  * Jlink : ligne de commande pour créer une JRE allégée avec que les modules nécessaires
  * Jdeprscan : vérification de l'utilisation d'API dépréciées

## Java 10

### Inférence de type

Les variables locales peuvent être déclarées avec la mot clé `var`. Le type sera alors inféré.

Exemple : `List<String> myList = new ... => var myList = new ...`

Quelques contraintes :

```java
var valeur; || var valeur = null; // Impossible, il faut initialiser
var a="a", b="b"; // Impossible de déclarer plusieurs var
var tableau = {"a", "b"} // Impossible, il faut typer explicitement
var lambda = {a, b} -> a*b // Impossible, les lambdas nécessitent un type explicite
var refMethode =  String::charAt // Impossible, il faut un type explicite
var myInt = 15; ... myInt = "myInt"; // Impossible on ne peut pas changer le type d'une var 
```

NB : les types inférés ne peuvent pas être des super types ou abstractions (Ex pour une liste on infère ArrayList et non List)

### Autres

* Méthode `orElseThrow` sur le type `Optional`, l'exception retournée est `NoSuchElementException`
* `copyOf(collection)` sur List, Set ou Map -> la copie est immuable
* Ajout sur les `Collectors`
  * `toUnmodifiableList`
  * `toUnmodifiableSet`
  * `toUnmodifiableMap`

## Java 11 (LTS)

Java 11 est une version LTS, celles-ci seront disponibles tous les 3 ans. Sachant que Java sort une version tous les 6 mois.

## Java 12

## Java 13

## Sources

* [Lien blog Xebia Java 8 à 11][1]
* [Lien blog invivoo Java 9][2.9]
* [Lien blog invivoo Java 10][2.10]
* [Lien blog invivoo Java 11][2.11]
* [Devoxx JM Doudoux][3]

[1]: https://blog.xebia.fr/2018/09/25/de-java-8-a-11-nouveautes-et-conseils-pour-migrer/
[2.9]: https://blog.invivoo.com/java-9-les-nouveautes/
[2.10]: https://blog.invivoo.com/les-nouveautes-de-java-10-episode-3/
[2.11]: https://blog.invivoo.com/les-9-nouveautes-de-java-11/
[3]: https://www.youtube.com/watch?v=dYubeLiObqY
[4.10]: https://openjdk.java.net/projects/jdk/10/
[4.11]: https://openjdk.java.net/projects/jdk/11/
[4.12]: https://openjdk.java.net/projects/jdk/12/
[4.13]: https://openjdk.java.net/projects/jdk/13/
