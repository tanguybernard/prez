

## Avec des mesures (Kotlin)

```kotlin
sealed class MeasUnit
object MileUnit: MeasUnit()
object MeterUnit: MeasUnit()

class MeasureValue<out T: MeasUnit>(val i: Int){
}

data class Mile(val m: MeasureValue<MileUnit>)
data class Meter(val m: MeasureValue<MeterUnit>)

fun main() {
    val first = Mile(m= MeasureValue(2))
    val sec = Meter(m= MeasureValue(2))
    if(first.m == sec.m){//Compilation failed
        println("do something")
    }
}
```

## Avec des roles (Typescript)

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



## Avec des dates (Typescript)


```typescript
declare const phantom: unique symbol;

//Création de type avec un attribut caché
type Utc = {[phantom]: "UTC"};
type TzEuropeParis = {[phantom]: "Eutope/Paris"};

//Phantom Type
type DateTime<PHANTOM> = {value: string} & PHANTOM;

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

## Avec des roles (Swift)

```swift
struct Employee<Role>: Equatable {
var name: String
}

enum Sales { }
enum Programmer { }

let zoe1 = Employee<Programmer>(name: "Zoe")
let zoe2 = Employee<Sales>(name: "Zoe")

print(zoe1 == zoe2)
```


source https://www.hackingwithswift.com/plus/advanced-swift/how-to-use-phantom-types-in-swift


## Avec des états (Elm vs Typescript)

Elm:

https://sporto.github.io/elm-patterns/advanced/flow-phantom-types.html
    
Typescript:

    declare const phantom: unique symbol;
    
    
    type Step<PHANTOM>
    = {model: {total: number, quantity:number}} & PHANTOM;
    
    type Start = {[phantom]: "Start"};

    type OrderWithTotal =  {[phantom]: "OrderWithTotal"};

    type OrderWithQuantity=  {[phantom]: "OrderWithQuantity"};
    
    type Done=  {[phantom]: "Done"};
    
    const priceEach = 5;
    
    
    //setQuantity : Int -> Step Start -> Step OrderWithQuantity
    function setQuantity(v: number) {
        const a: unknown = function() {
            return {model: {quantity: v}} as unknown as Step<Start>
        }
        return a as () => Step<OrderWithQuantity>
    }
    //setTotal : Int -> Step Start -> Step OrderWithTotal
    function setTotal(v: number) {
        const a: unknown = function() {
            return {model: {total: v}} as Step<Start>
        }
        return a as () => Step<OrderWithTotal>
    }
    
    //adjustTotalFromQuantity : Step OrderWithQuantity -> Step Done
    const adjustTotalFromQuantity = (step: Step<OrderWithQuantity>): Step<Done> => {
        return {model: {...step.model, total: step.model.quantity*priceEach}} as Step<Done>
    }
    
    const adjustQuantityFromTotal = (step: Step<OrderWithTotal>): Step<Done> => {
        return {model: {...step.model, quantity: step.model.quantity/priceEach}} as Step<Done>
    }
    
    const init = setQuantity(5)();
    
    console.log(init.model);

    adjustQuantityFromTotal(init)
