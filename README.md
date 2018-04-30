## Arrows
```javascript
let add = (x, y) => x + y
let square = x => x * x
let three = () => 3
let substract = (x, y) => {
    return x - y
}

// add(3,5) = 8
// square(3) = 9
// three() = 3
// substract(5,3) = 2
```

## Arrow functions
```javascript
let numbers = [1,2,3,4]

let sum = 0
numbers.forEach(n => sum += n)
// sum = 10

let doubled = numbers.map(n => n * 2)
// doubled = [2,4,6,8] 
```

## Iterators for in/of
```javascript
let sum = 0
let numbers = [1,2,3,4]
for(let i in numbers) {
    sum += numbers[i]
}
// sum = 10

let sum = 0
let numbers = [1,2,3,4]
for(let n of numbers) {
    sum += n
}
// sum = 10
```

## Generators
```javascript
let numbers = function*() {
    yield 1
    yield 2
    yield 3
    yield 4
}
// numbers = [1, 2, 3, 4]

let employees = function*() {
    yield [for (n of ["Tim", "Sue", "Joy", "Tom"]) if(n == "Joy") n * n]
}
// employees = ["Joy"]

let employees = function*() {
    yield* [for (n of ["Tim", "Sue", "Joy", "Tom"]) if(n == "Joy") n * n]
    // Greedy. Looping through ["Tim", "Sue", "Joy", "Tom"]
}
// employees = "Joy"

let employees = function*() {
    yield* (for (n of ["Tim", "Sue", "Joy", "Tom"]) if(n == "Joy") n * n)
    // Lazy (generator). Looping through ["Tim", "Sue", "Joy"]
}
// employees = "Joy"
```

## Comprehensions
```javascript
let numbers = [for (n of [1,2,3]) n * n]
// numbers = [2,4,9]

let numbers = [for (n of [1,2,3]) if(n < 3) n * n] 
// Greedy. looping through [1,2,3].
// numbers = [2,4]

let numbers = (for (n of [1,2,3]) if(n < 3) n * n)
// Lazy (generator). Looping through [1,2] 
// numbers = [4,9]

```

## Classes
```javascript
class Employee {
    
    constructor(name) {
        this._name = name
        // Alt: this.name(name)
    }
    
    doWork() {
        return "complete!"
    }

    getName() {
        return this._name
    }

    get name() {
        return this._name.toUpperCase()
    }

    set name(name) {
        if(name)
            this._name = name
    }
}

let e1 = New Employee("Scott")
let e2 = New Employee("Alex")

let work = e1.doWork()
// work =  = "complete!"

let name1 = e1.getName()
let name2 = e2.getName()
// name1 = "Scott"
// name2 = "Alex"


let name1 = e1.name
e2.name = "Bob"
let name2 = e2.name
// name1 = "SCOTT"
// name2 = "BOB"
```

## Numbers
```javascript
let hex = 0xa
let oct = 0o12
let bin = 0b1010
let dec = Number(hex)
// dec = 10


let int = Number.parseInt(3)
let float = Number.parseFloat(2.5)
// int = 3
// int = 2.5


let nan1 = isNaN("NaN")
let nan2 = Number.isNaN("NaN")
// nan1 = true
// nan2 = false


let int1 = Number.isInteger(1)
let int2 = Number.isInteger(1.0)
let int3 = Number.isInteger(1.5)
// int1 = true
// int2 = true
// int3 = false
```

## Array
```javascript
var match = [1,5,10].find(item => item > 8)
// match = 10


var match = [1,5,10].findIndex(item => item > 4)
// match = 1
```

## Set
```javascript
let set = new Set()
set.add("foo")
let size = set.size
// size = 1

let key = {}
set.add(key)
set.add(key)
let hasKey = set.has(key)
let size = set.size
// hasKey = true
// size = 1
set.clear()
// set.size = 0


let set = new Set([1,2,3])
let hasKey = set.has(1)
// hasKey = true
set.delete(3)
// set.size = 2


let set = new Set()
set.add("Tom")
set.add("Dick")
set.add("Harry")
let names = []
set.forEach(item => {
    names.push(item)
})
// names = ["Tom", "Dick", "Harry"]
let set2 = new Set(set.values())
// set2.size = 3
```

## Map (key value pairs)
```javascript
let map = new Map()
map.set("age", 35)
// map.size = 1

let age = map.get("age")
// age = 35


let map = new Map([ ["name": "Bob"], ["age", 25], ["gender": "Male"] ])
// map.size = 3

let hasKey = map.has("age")
// hasKey = true

let values = ""
map.forEach((v, k) => {
    values += `${v} `
})
// values = "Bob 25 Male"

let values = ""
for(let [k, v] of map) {
    values += `${v} `
}
// values = "Bob 25 Male"

let map2 = new Map(map.entries())
// map2.size = 3
```


## Promise
```javascript

let getOrder = orderId => Promise.resolve({userId: 35})
let getUser = userId => Promise.resolve({companyId: 18})
let getCompany = companyId => Promise.resolve({name: "Pluralsight"})

let someFunction = (done) => {
    getOrder(3)
        .then(order => {
            return getUser(order.userId)
        })
        .then(user => {
            return getCompany(user.companyId)
        })
        .then(company => {
            // some logic here
            // company.name = "Pluralsight"
            done()
        })
        .catch(error => {
            // handle error
        })
}


let getCourse = courseId => {
    let courses = {
        1: {name: "Introduction to Cobol"},
        2: {name: "Yet Another C# Course"},
        3: {name: "How to make billions by blogging"},
    }
    return Promise.resolve(courses[courseId])
}

let someRandomFunction = (done) => {
    let courseIds = [1,2,3]
    let promises = []
    
    courseIds.forEach(v => {
        promises.push(getCourse(v))
    })

    Promise.all(promises)
        .then(v => {
            // v.length = 3
            // v[1].name = "Yet Another C# Course"
            done()
        })
}

```



