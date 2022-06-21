---
module:         B-INN-000
title:          Introduction au Java
subtitle:		Programmation Orienté Objet

language:		java
compilation: 	javac, gradle, automated compilation with IDE
build:			gradle

noFormalities:	false
noCleanRepo:	false
noBonusDir:		true
noErrorMess:	true

author:			Alwyn
version:		1.0
---

# Découverte du Java

## Introduction

- Qu'est-ce que le Java ?
    - Java est un langage de programmation orienté objet, typé, "compilé" qui fonctionne grâce à une **J**ava **V**irtual **M**achine (**JVM**)

- Qu'est-ce que la **JVM** ?
    - La JVM est une machine virtuelle qui permet l'interprétation du code java compilé (**.class**), et aussi des archives java (**.jar**)

    - C'est l'un des avantages du Java ! Grâce à la **JVM** le code est très portable, il peut être exécuté partout tant qu'une **JVM** est présente !

    - D'autres langages peuvent aussi fonctionner sur la **JVM** c'est le cas du **Scala** et du **Kotlin**

## Pré-requis

Si vous n'avez pas déjà installé les outils nécessaires à ce workshop suivez les instructions situées ici : #br
[https://github.com/alwyn974/workshop-java/blob/master/REQUIREMENTS.md](https://github.com/alwyn974/workshop-java/blob/master/REQUIREMENTS.md)

#newpage

## Le Java ! La théorie

### Les modifieurs de visibilité et d'accès

En java, on peut changer la visibilité d'une variable, d'une classe, d'une fonction, pour cela il faut utiliser des **keyword** spécifique

- Les modifieurs de visibilité
  - `private` personne ne peut modifier/accéder à cette variable à part la classe actuelle
  - `protected` uniquement les classes enfants ou appartenant au même package peuvent modifier/accéder à cette variable
  - `public` tout le monde peut modifier/accéder à cette variable

#hint(Par défaut une variable, classe ou fonction déclarée sans modifieur de visibilité est en privé)

- Les modifieurs d'accessibilité
  - `static` une variable ou une fonction statique peut être accédée sans instancier la classe, elle est aussi unique à cette classe
  - `final` pour faire simple, c'est l'équivalent du `const` en C/C++
  - `super` bon techniquement, ce n'est pas un modifieur d'accessibilité, au contraire il permet d'accéder à des méthodes/variables de la classe parente, il permet surtout d'appeler le constructeur de la classe parente

#warn(Les variables statiques sont toutes les mêmes peu importe l'instance de la classe)

#hint(Le keyword **super** est pratique lorsque l'on veut utiliser la méthode de la classe parente et y ajouter quelque chose, ou bien pour modifier une variable de la classe parente à la place d'une variable déclaré dans la classe enfant)

#newpage
### Les types

Vu que le Java est basé sur le C++ et donc le C, les types restent à peu près les mêmes, pour certains ils sont améliorés ou ajoutés#br

#### Variable

- `boolean` permet de stocker les états `true` et `false` (comme bool en C/C++)
- `byte` permet de manipuler des entiers codés sur 1 octet (comme char)
- `double`, `int`, `long`, `float`, `short` restent les mêmes
- Vos objets à vous

#warn(Pour `double`, `int`, `long`, `float`, `short` se sont des types primitifs, et non pas des objets. 
Ils possèdent donc leur équivalent en tant d'objet `Double`, `Integer`, `Long`, `Float`, `Short`)

#### Classes

- `enum` les enums en java sont beaucoup plus complet que ceux en C/C++, vu que ce sont des objets, on peut y assigner plus qu'un simple Integer comme valeur
- `interface` permet de créer une interface
- `abstract class` permet de créer une classe abstraite
- `class` permet de créer une classe normale

#newpage

### Le polymorphisme - L'héritage

L'héritage en java fonctionne comme en C++ à quelques différences près.
On ne peut hériter que d'une seule classe, néanmoins on peut hériter de plusieurs interfaces

Exemple:
```java
public class Animal {
    public void eat() {
        System.out.prinln("Animal can't eat");
    }
}

public interface ILiveable {
  void live();
}

public interface IMovable {
    void move(int x, int y);
}

public class Cat extends Animal implements ILiveable, IMovable {
    
    private final String name;
    
    public Cat(String name) {
        this.name = name;
    }

    //Overriden function from interface IMovable
    @Override
    public void move(int x, int y) {
        System.out.println("X: " + x + " Y:" + y);
    }

    //Overriden function from interface IMovable
    @Override
    public void live() {
        System.err.println("I'm dead bruh");
    }

    //Overriden method from Animal class
    @Override
    public void eat() {
        System.out.println("I'm hungry !!!");
    }
    
}
```

#hint(@Override est une annotation, elle permet de préciser qu'une méthode est override, cette annotation spécifique n'est pas obligatoire.
On peut créer nos propres annotations aussi. Les annotations seront très utiles dans les prochains workshop)

### Le polymorphisme - La surcharge

Comme en C++ on peut surcharger une méthode avec différents types de paramètre tout en ayant le même nom

Exemple:
```java
public class Main {

    public static void main(String[] args) {
        System.out.println("coucou"); //type of parameter is String
        System.out.println(1); //type of parameter is Integer
        System.out.println(0.0); //type of parameter is Double
        System.out.println(0.0f); //type of parameter is Float
        System.out.println(5 < 0); //type of parameter is Boolean
        System.out.println(new Object()); //type of parameter is Object, print an Object call the method toString() of the object
    }
    
}
```
### Le polymorphisme - La redéfinition

Comme en C++, si l'on hérite d'une classe, d'une interface ou d'une classe abstraite, on peut surcharger les méthodes présentes dans la classe parente sauf si les méthodes ont le modifieur `private` ou `final`

#hint(Contrairement au C++ on ne peut pas hériter de toutes les variables/méthodes d'une classe, uniquement des méthodes et variables `public` et `protected`)

### Instancier un objet

C'est presque comme en C++, sauf qu'il faut utiliser new partout. #br
En java, on ne s'occupe pas de la gestion mémoire, c'est le Garbage Collector (**GC**) de la JVM qui s'en occupe automatiquement

#warn(Il faut quand même penser à faire un code un minimum optimisé)

Exemple:
```java
public class Main {

    public static void main(String[] args) {
        Object object = new Object(); //create object variable with Object type
        String str = new String("Hey"); //create str variable with String type
        String string = "toto"; //the good way to create a String
        int[] array = new int[42]; //create array with int[] type
    }

}
```

### Structure d'un projet java

Les projets Java sont principalement généré par des builds tools, comme `gradle` qu'on va utiliser dans ce workshop.
La structure reste plutôt basique un dossier `src` où l'on mettra tout notre code, néanmoins en utilisant gradle dans ce dossier vous aurez un dossier `test` et un dossier `main`.
Le dossier `test` est pour les tests unitaires et le dossier `main` pour mettre votre code.

### Qu'est-ce qu'un package ?

En Java pour organiser votre code, on va créer ce qu'on appelle des `packages`, ce sont juste des sous dossiers qui seront dans `src/main`. Cela permet d'avoir un code organisé selon des catégories. #br
Généralement un package se construit sous la forme d'un ndd (nom de domaine) inversé + le nom du projet et différents sous packages.

Exemple: 
```
re.alwyn974.monsuperworkshop
re.alwyn974.monsuperworkshop.subpackage
re.alwyn974.monsuperworkshop.epitech.workshop
```

#warn(Il y a une convention de nommage pour les packages, ils doivent être en minuscules. On n'est pas obligé de respecter cette convention, mais c'est mieux)

### Qu'est-ce qu'un import

En java si vous voulez avoir accès à d'autres classes, il vous faut utiliser les `import`, l'import est l'équivalent d'un include de header contenant les prototypes en C/C++.

Exemple: 
```java
import re.alwyn974.monsuperworkshop.Marvin;
import re.alwyn974.monsuperworkshop.*;
import static re.alwyn974.monsuperworkshop.Marvin.sayHello;
import static re.alwyn974.monsuperworkshop.Marvin.*;
```

Il existe 2 types d'import :
- L'import static, permet d'accéder à des variables et méthodes **statiques** sans préciser le nom de la classe
- L'import normal, permet d'accéder à une classe et ses méthodes qui se trouvent dans un autre package

L'import avec wildcard `*` permet d'importer toutes les classes d'un package ou toutes les méthodes/variables d'une classe avec l'import static.

#hint(En utilisant Intellij Idea et l'autocomplétion la plupart des imports se feront automatiquement, sauf en cas de conflits là il faudra choisir l'import spécifique.
Les classes contenues dans le même package sont accessibles directement)

#newpage
### Création d'un nouvel objet

En Java tout code doit être dans une classe/interface/enum. On ne peut pas déclarer une méthode hors d'une classe comme en C/C++.

Pour créer une classe/interface/enum, il y a une structure à suivre :

- On commence par `public` ou rien (dans ce cas la classe sera en privée)
- Ensuite on précise le type d'objet que l'on crée (`class`, `interface`, `enum`, `abstract class`)
- On précise le nom de l'objet
- Si on veut faire de l'héritage, on utilise `extends` et/ou `implements` pour les interfaces et on précise le nom de la classe parente
- Et après on ouvre des accolades

Exemple :

```java
public class Marvin {
    //TODO: add code here
}

class ImNotAccessible {
    //TODO: add code here
}

public interface ITakeALotOfSpace {
    //TODO: add code here
}

public abstract class AbstractChooseAName {
    //TODO: add code here
}

public enum EnumTest {
    //TODO: add code here
}
```

#warn(Comme pour les packages, les noms d'objets doivent respecter une convention de nommage, pour les objets, on suit le PascalCase, qui consiste à mettre en majuscule la première lettre de chaque mot.)

#warn(Le nom d'un objet doit être aussi le même que le fichier Java correspondant)

#newpage
### Création d'un constructeur

Comme en C++ on peut ajouter un constructeur à une classe. Par contre, il n'y a pas de destructeur.
Pour créer un constructeur il y a une structure à suivre :

- On commence par un modifieur de visibilité (`public`, `private`, `protected`) ou rien (dans ce cas le constructeur sera en privé)
- On précise le nom de la classe
- On précise les paramètres du constructeur
- Et enfin on ouvre des accolades

Exemple:
```java
public class Marvin {
    public Marvin(String name) {

    }
}

public class PrivateConstructor {
    private PrivateConstructor() {

    }
}

public class ProtectedConstructor {
    protected ProtectedConstructor() {

    }
}

public class ClassWithFinalVariable {
    final String toto;
    
    public ClassWithFinalVariable(String toto) {
        this.toto = toto;
    }
}
```

#warn(Si vous avez déclaré des variables `final` dans votre objet, sans les initialiser, il faudra les initialiser dans le constructeur)

#newpage
### Création d'une variable ou une méthode

Pour créer une variable ou une méthode, il faut quelle soit dans une classe/interface/enum/abstract class.
Il y a aussi certaines structures à suivre :

#### Variable
- On commence par un modifieur de visibilité (`public`, `private`, `protected`) ou rien (dans ce cas la variable sera en privée)
- On précise le type de la variable (String, int, boolean, etc.)
- On précise le nom de la variable
- On peut assigner la variable à une valeur ou non

#### Méthode
- On commence par un modifieur de visibilité (`public`, `private`, `protected`) ou rien (dans ce cas la méthode sera en privée)
- On précise le type de retour de la méthode (String, int, boolean, etc.)
- On précise le nom de la méthode
- On précise les paramètres de la méthode

Exemples:

```java
public class Main {
    private static final String NAME = "Marvin";
    private boolean isMarvin = true;
    private int age = 42;
    
    private void method() {
        
    }
    
    private String getName() {
        return NAME;
    }
    
    private boolea isMarvin() {
        return isMarvin;
    }
}
```

#warn(Ici on suit la convention de nommage du `camelCase` qui consiste à mettre en minuscule la première lettre du mot et en mettre une majuscule à chaque mot suivant.)

#warn(Une petite spécification pour les variables `static final` on les écrit en `SCREAMING_SNAKE_CASE`)

#newpage
## Le Java ! La pratique :3

### Création d'un projet avec gradle

Si vous venez d'installer Intellij Idea, cliquez sur `New Project` sinon aller dans `File > New > Project`

#imageLeft(new_project.png, 200px, 9)
Choisissez le nom du projet (ex : `WorkshopJava`)
Sélectionnez `Java`
Sélectionnez `Gradle`
Sélectionnez la version du JDK (11 si vous êtes sur le dump)
Dans `Advanced Settings` mettez votre package dans `GroupID` (ex : `com.github.username.workshop`)
Dans `ArtifactId` mettez le nom du jar (ex : `WorkshopJava`)
Il faudra alors attendre la fin de la création du projet gradle (Quand le dossier `src` apparait, c'est fini)

<br>
<br>
<br>
<br>
<br>
<br>

### Lancement d'un projet

Pour lancer un projet Java, à coter du `main` vous aurez un petit logo de lancement, il suffit de cliquer dessus et c'est parti !
Cela va créer une configuration sur Intellij pour lancer le programme avec ce `main` précisément, car en Java on peut avoir plusieurs mains et en choisir un en lançant un `.jar`

#newpage

### Exercice 1

- Créez votre propre package (ex: `com.github.username.workshop`)
- Dans ce package créez une classe `HelloWorld.java`
- Créez une méthode main en `public static` et en prenant en argument un `String... args`
- Trouvez comment print un `Hello World !\n`

#terminal(Lancement avec intellij parce que build c'est long
Hello World!)

### Exercice 2

Créez-le sous package life

Créez une classe Entity elle devra posséder :

- Un constructeur qui initialisera les variables ci-dessous
- `String name` accessible uniquement via getter/setter 
- `double x, y, z` accessible uniquement via la classe enfant (ou package) et par getter/setter

### Exercice 3

Créez une classe `EntityLiving` qui héritera de la classe `Entity`, elle devra posséder :

- `double life` accessible uniquement via getter/setter
- `boolean isAlive()` une fonction publique pour dire si l'entitée est en vie (life > 0)
- `String sentence` une variable publique (créer les getter/setter quand même)
- `void displaySentence()` une fonction qui affichera la sentence

### Exercice 4

### Exercice 5

Différenciez une classe depuis une liste d'objet.

#hint(Regardez comment utiliser le **keyword** `instanceof`)

### Exercice 6

### Exercice 7

### Exercice 8

### Exercice 9

### Exercice 10

### Tests unitaires

Comme tout langage le Java dispose de plusieurs libraries pour faire des tests unitaires, on va utiliser la plus connue: `JUnit`

#newpage
# Pour approfondir votre apprentissage

Beaucoup de site propose des cours sur le Java, en voici quelques un :
- [Jmdoudoux.fr](http://www.jmdoudoux.fr/accueil_java.htm)
- [Koor.fr](https://koor.fr/Java/Index.wp)