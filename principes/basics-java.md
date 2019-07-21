# Basics Java et POO

## Field vs Property vs Variable

### Field

Il s'agit d'une données membre de la classe, elle peut être manipulée librement en fonction de sa visibilité.
Le terme attribute peut aussi être employé mais désigne généralement un field public.

### Property

Il s'agit d'une caractéristique de la classe, souvent privée elle est manipulée par des methodes (getter ou setter)

### Variable

Permet d'indentifier une valeur ou une allocation mémoire grâce à un nom. Elle possède un scope et peut évoluer au cours de l'exécution du traiement.

### Exemple

```java

public class Variables { 
  
    // Constant 
    public final static String name = "robot"; 
  
    // Value 
    final String dontChange = "India"; 
  
    // Field 
    protected String rever = "GANGA"; 
  
    // Property 
    private String age; 
  
    // Still the property 
    public String getAge() 
    { 
        return this.age; 
    } 
  
    // And now the setter 
    public void setAge(String age) 
    { 
        this.age = age; 
    } 
} 
```

## Liens

* [Glossaire Oracle][1]

[1]: https://docs.oracle.com/javase/tutorial/information/glossary.html
