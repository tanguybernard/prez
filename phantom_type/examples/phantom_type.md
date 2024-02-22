# Phantom Type

-----

## Data Type

Un type de donnée, ou simplement un type, définit la nature des valeurs que peut prendre une donnée, ainsi que les opérateurs qui peuvent lui être appliqués.



Note: This will only appear in the speaker notes window.

---

## Generic Type

C'est comme un data type, mais avec une déclaration de paramètre de type attachée.

```java
interface Collection<E>  {
    void add (E x);
    Iterator<E> iterator();
}
```

Ici, **E** est un paramètre de type.

---

## Parametryzed Type

Un type paramétré (Parametrized Type) est une instanciation d'un type générique avec des valeurs concrètes fournies pour tous ses paramètres de type.

```java
Collection<String> coll;
```

---

##  Type Parmeter vs Type Argument


Le
<span style="color:blue">`T`</span>
dans
<span style="color:blue">`Foo<T>`</span>
est un **type parameter** et le 
`String` dans 
`Foo<String> f` 
est un **type argument**.
---

## Phantom Type


Un type fantôme est simplement un type paramétré avec un paramètre de type inutilisé.

```haskell
newtype Const a b = Const { getConst :: a }
```

```typescript
type FormData<A> = string;
```

Note: Un type fantôme est un type paramétré dans lequel un ou plusieurs paramètres du côté gauche n'apparaissent pas dans le côté droit.

---

### Phantom Types

Ce sont des types qui apportent des infos au compilateur pour introduire des contraintes et lever des erreurs au plus tôt évitant ainsi les surprises au runtime.

-----





## A quoi ça sert ?

Les types fantômes peuvent être utilisés pour obtenir des garanties au moment de la compilation.

---

## Cas des Id's

```kotlin
data class User(val id: String)
data class Location(val id: String)

val user = User(id = "test id")
val location = Location(id = "test id")

fun main() {
    if (user.id == location.id) {
        println("Yes but NOOOOO !")
    }
}
```

Note: https://twitter.com/v_pradeilles/status/1715328789486383236?s=61&t=V7PID5JI7WpC7UFFTCWcSA


---

## Solution

```kotlin
@JvmInline value class Id<out T>(val value: String)
// Id<out T> in Kotlin is Id<? extends T> in Java
data class User(val id: Id<User>)
data class Location(val id: Id<Location>)

val user = User(id = Id("test id"))
val location = Location(id = Id("test id"))

fun main() {
    if (user.id == location.id) { // Compilation failed
        println("Yes but NOOOOO !")
    }
}
```

Note: https://twitter.com/v_pradeilles/status/1715328789486383236?s=61&t=V7PID5JI7WpC7UFFTCWcSA

---

## Avec des mesures

```kotlin
sealed class MeasUnit
object MileUnit: MeasUnit()
object MeterUnit: MeasUnit()

class MeasureValue<out T: MeasUnit>(val i: Int){
}

data class Mile(val m: MeasureValue<MileUnit>)
data class Meter(val m: MeasureValue<MeterUnit>)

fun main() {
    val first = Mile(m= MeasureValue(1))
    val sec = Meter(m= MeasureValue(2))
    if(first.m == sec.m){//Compilation failed
        println("do something")
    }
}
```
-----

## Type safety

La sécurité des types c'est une contrainte au moment de la compilation, mais aussi au moment de l'exécution.

---

## Type safety

Il y a deux problèmes principaux liés à la sécurité des types: 

- La mémoire
- Le type de données (avec les opérations correspondantes).


Note: https://stackoverflow.com/questions/260626/what-is-type-safe

-----


## Mon implémentation

```typescript
declare const phantom: unique symbol;

//Création de type avec un attribut caché
type Utc = {[phantom]: "UTC"};
type TzEuropeParis = {[phantom]: "Eutope/Paris"};

//Phantom Type
type DateTime<PHANTOM> = {value: string} & PHANTOM;

const t: DateTime<Utc> = {value: "2024-02-01 00:00:00 +00"} as  DateTime<Utc>;
console.log(t[phantom])//log: {value: "2024-02-01 00:00:00 +00"}

function createPeriod<T>(d1: DateTime<T>, d2: DateTime<T>)
{
//new Period(d1, d2)
}

//provide a way to create person that ignores the additional 'phantom' property:
const createUtcDate : (value: string) => DateTime<Utc> =
(value) => {
    return {value} as DateTime<Utc>
}

const createEuropeParisDate : (value: string) => DateTime<TzEuropeParis> =
(value) => {
    return {value} as DateTime<TzEuropeParis>
}

const utcDate1= createUtcDate("2024-02-01 00:00:00 +00");
const utcDate2= createUtcDate("2024-02-19 00:00:00 +00");
const europeParisDate1= createEuropeParisDate("2024-02-18T00:00:00 +01:00");


createPeriod(utcDate1, utcDate2)
createPeriod(utcDate1, europeParisDate1)//Error
```

-----

## Cas des guard


```typescript
type PersonWithRole = {firstNm: string, lastNm: string, role: string}

const john: PersonWithRole = {firstNm: "John", lastNm: "Doe", role: "Creator"}
const alice: PersonWithRole = {firstNm: "Alice", lastNm: "Wonderland", role: "Viewer"}

function coPostSomething(p1: PersonWithRole, p2: PersonWithRole) {
    if(p1.role === 'Creator' && p2.role ==='Creator') {
        console.log("Post something");
    }
}

coPostSomething(john, alice);
```

---

## Solution (merci le Duck Typing)



```typescript
class Person {
    constructor(public fstName: string, public lstName: string) {
    }
}

class PersonViewer extends Person {
    role;
    constructor(public fstName: string, public lstName: string) {
        super(fstName, lstName)
        this.role = 'Viewer'
    }
}

class PersonCreator extends Person {
    role;
    constructor(public fstName: string, public lstName: string) {
        super(fstName, lstName)
        this.role = 'Creator'    
    }
}

function coPostSomething(p1: PersonCreator, p2: PersonCreator) {
    console.log("Post something");
}

coPostSomething(new PersonCreator('A', 'A'), new PersonViewer('B', 'B'));// MERDE CA MARCHE
```

---

## Check de l'objet ou check du type !


![The Office Image](./examples/assets/theoffice.png)


---

## Solution

```typescript
declare const phantom: unique symbol;

type Viewer = {[phantom]: "Viewer"};
type Creator = {[phantom]: "Creator"};


type Person<PHANTOM> = 
    {firstNm: string, lastNm: string} & PHANTOM;

function coCreateSomething(p1: Person<Creator>, p2: Person<Creator>)
{
    console.log("Create something");
}

//provide a way to create person that ignores the additional 'phantom' property:
const createCreatorPerson : (fst: string, lst: string) => Person<Creator> = 
    (fst, lst) => {
    return {firstNm: fst, lastNm: lst} as Person<Creator>
}

const createViewerPerson : (fst: string, lst: string) => Person<Viewer> =
    (fst, lst) => {
return {firstNm: fst, lastNm: lst} as Person<Viewer>
}

const johnCreator= createCreatorPerson("John", "Doe");
const harleyCreator= createCreatorPerson("Harley", "Quinn");
const aliceViewer = createViewerPerson("Alice", "Wonderland");


coCreateSomething(johnCreator, harleyQuinnCreator)
coCreateSomething(johnCreator, aliceViewer)//Error
```


-----

## Cas des états

```typescript
type Open= 'open';
type Close= 'close';
type Door = Open | Close;

function closeDoor(door: Door) {
    if(door === 'open') {
        log("La porte s'ouvre")
    }
    else {
        error("La porte est déja fermé")
    }
}
```

---

## Solution

```typescript
declare const phantom: unique symbol;
type Open = {[phantom]: 'Open'};
type Close = {[phantom]: 'Close'};

type DoorState<T> = {id: never} & T;

type InitDoorClosed = (a: string) => DoorState<Close>;
type CloseDoor = (a: DoorState<Open>) => DoorState<Close>;
type OpenDoor = (a: DoorState<Close>) => DoorState<Open>;


const initDoorClosed: InitDoorClosed = id => {
    return { id } as DoorState<Close>;
};
export const openReally: OpenDoor = id => {
    return { id } as DoorState<Open>;
};

export const closeReally: CloseDoor = id => {
    return { id } as DoorState<Close>;
};

const initialData = initDoorClosed('123');

const openedDoor = openReally(initialData);
const closedDoor = closeReally(openedDoor);//ferme une porte ouverte

const closeADoorAlreadyClose = closeReally(closedDoor); //ERROR: ferme une porte deja ferme
```

---

## Bénéfices

- Evite les recherches de types au moment de l'exécution (on le voit direct a la compil)
- Rend les états explicites
- Porte une partie des informations au niveau du type plutot que dans des sous-classes


---

## Conclusion



---

## Test (Image)

![External Image](https://s3.amazonaws.com/static.slid.es/logo/v2/slides-symbol-512x512.png)

---

## Test (Math)

`\[ J(\theta_0,\theta_1) = \sum_{i=0} \]`

---


<!-- .slide: data-background="#ff0000" -->

## Test


<span style="color:blue">some *blue* text</span>

---

## Test 2

```js
console.log('Hello world!');
```
