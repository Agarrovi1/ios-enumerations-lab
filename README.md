# Enumerations lab

Fork and clone this repo. On your fork, answer and commit the follow questions. When you are finished, submit the link to your repo on Canvas.


## Question 1

a) Define an enumeration called `iOSDeviceType` with member values `iPhone`, `iPad`, `iWatch`. Create a variable called `myDevice` and assign it one member value.

```swift
enum iOSDeviceType: String {
case iPhone
case iPad
case iWatch
}

var myDevice = iOSDeviceType.iPad
```

b) Adjust your code above so that `iPhone` and `iPad` have associated values of type String which represents the model number, eg: `iPhone("6 Plus")`. Use a switch case and let syntax to print out the model number of each device.

```swift
enum iOSDeviceType {
case iPhone(String,String,String)
case iPad(String,String,String)
case iWatch
}

var iPhoneModels = iOSDeviceType.iPhone("4", "5", "6 Plus")
var iPadModels = iOSDeviceType.iPad("Mini", "Pro", "Air")

switch iPhoneModels {
case .iPhone(let model1,let model2 , let model3):
print("iphone models: \(model1), \(model2), \(model3)")
case .iPad(let model1,let model2 , let model3):
print("ipad models: \(model1), \(model2), \(model3)")
default:
print()
}
```

## Question 2

a) Write an enum called `Shape` and give it cases for `triangle`, `rectangle`, `square`, `pentagon`, and `hexagon`.

```swift
enum Shape {
case triangle,rectangle,square,pentagon,hexagon
}
```

b) Write a method inside `Shape` that returns how many sides the shape has. Create a variable called `myFavoritePolygon` and assign it to one of the shapes above, then print out how many sides it has.

```swift
enum Shape: String {
case triangle
case rectangle
case square
case pentagon
case hexagon
}


func howManySides(a: String) -> Int {
switch a {
case "triangle":
return 3
case "rectangle":
return 4
case "square":
return 4
case "pentagon":
return 5
case "hexagon":
return 6
default:
return 0
}
}

var myFavoritePolygon = Shape.square.rawValue
print(howManySides(a: myFavoritePolygon))
```

c) Re-write `Shape` so that each case has an associated value of type Int that will represent the length of the sides (assume the shapes are regular polygons so all the sides are the same length) and write a method inside that returns the perimeter of the shape.

```swift
enum Shape {
case triangle(Int)
case rectangle(Int)
case square(Int)
case pentagon(Int)
case hexagon(Int)
}

var sampleShape = Shape.triangle(3)

switch sampleShape {
case .triangle(let length):
print("perimeter is \(length * 3)")
case .rectangle(let length):
print("perimeter is \(length * 6)")
case .square(let length):
print("perimeter is \(length * 4)")
case .pentagon(let length):
print("perimeter is \(length * 5)")
case .hexagon(let length):
print("perimeter is \(length * 6)")
}
```

## Question 3

Write an enum called `OperatingSystem` and give it cases for `windows`, `mac`, and `linux`. Create an array of 10 `OperatingSystem` objects where each one is set to a random operating system. Then, iterate through the array and print out a message depending on the operating system.

```swift
enum OperatingSystem: String {
case windows
case mac
case linux
}

var arrayOfTen = [OperatingSystem.windows,OperatingSystem.mac,OperatingSystem.linux,OperatingSystem.linux,OperatingSystem.mac,OperatingSystem.windows,OperatingSystem.mac,OperatingSystem.linux,OperatingSystem.linux,OperatingSystem.mac]
func oSThingy(array: [OperatingSystem]) {
for a in array {
switch a {
case .mac:
print("mac: the OS of apple products")
case .linux:
print("linux: an OS with a penguin?")
case .windows:
print("windows: OS with window picture")
}
}
}
oSThingy(array: arrayOfTen)
```

## Question 4

You are working on a game in which your character is exploring a grid-like map. You get the original location of the character and the steps he will take.

- A step .up will increase the y coordinate by 1.
- A step .down will decrease the y coordinate by 1.
- A step .right will increase the x coordinate by 1.
- A step .left will decrease the x coordinate by 1.
- Print the final location of the character after all the steps have been taken.

```swift
enum Direction {
    case up
    case down
    case left
    case right
}

var location = (x: 0, y: 0)
var steps: [Direction] = [.up, .up, .left, .down, .left]

// your code here
func makingMyWayDownTown(steps: [Direction], location: (Int,Int)) -> (Int,Int) {
var newLocation = location
for a in steps {
switch a {
case .up:
newLocation.1 += 1
case .down:
newLocation.1 -= 1
case .left:
newLocation.0 -= 1
case .right:
newLocation.0 += 1
}
}
return newLocation
}
location = makingMyWayDownTown(steps: steps, location: location)
print(location)
```


## Question 5

a) Define an enumeration named `HandShape` with three members: `.rock`, `.paper`, `.scissors`.

```swift
enum HandShape {
case rock
case paper
case scissors
}
```

b) Define an enumeration named `MatchResult` with three members: `.win`, `.draw`, `.lose`.

```swift
enum MatchResult {
case win
case draw
case lose
}
```

c) Write a function called `match` that takes two `HandShapes` and returns a `MatchResult`. It should return the outcome for the first player (the one with the first hand shape).

Hint: Rock beats scissors, paper beats rock, scissor beats paper

```swift
func match(playerOne: HandShape,playerTwo: HandShape) -> MatchResult {
switch true {
case playerOne == playerTwo:
return MatchResult.draw
case playerOne == .paper, playerTwo == .rock:
return MatchResult.win
case playerOne == .rock, playerTwo == .scissors:
return MatchResult.win
case playerOne == .scissors, playerTwo == .paper:
return MatchResult.win
default:
return MatchResult.lose
}
}
```

## Question 6

a) You are given a `CoinType` enumeration which describes different coin values. Print the total value of the coins in the array `moneyArray` which contains tuples of type (`quantity`, `CoinType`).

```swift
enum CoinType: Int {
    case penny = 1
    case nickle = 5
    case dime = 10
    case quarter = 25
}

var moneyArray:[(Int,CoinType)] = [(10,.penny),
                                   (15,.nickle),
                                   (3,.quarter),
                                   (20,.penny),
                                   (3,.dime),
                                   (7,.quarter)]

// your code here
func totalValueOfChangeInPocket(coins: [(Int,CoinType)]) {
var money = 0
for a in coins {
switch a.1 {
case .dime:
money += (a.0 * CoinType.dime.rawValue)
case .nickle:
money += (a.0 * CoinType.nickle.rawValue)
case .penny:
money += (a.0 * CoinType.penny.rawValue)
case .quarter:
money += (a.0 * CoinType.quarter.rawValue)
}
}
print("\(money) cents")
}
totalValueOfChangeInPocket(coins: moneyArray)
```

b) Write a method in the `CoinType` enum that returns an Int representing how many coins of that type you need to have a dollar. Then, create an instance of `CoinType` set to `.nickle` and use your method to print out how many nickels you need to have to make a dollar.

```swift
enum CoinType: Int {
case penny = 100
case nickle = 20
case dime = 10
case quarter = 4
}

let coin = CoinType.nickle
var coinsInDollar = Int()
switch coin {
case .nickle:
coinsInDollar = CoinType.nickle.rawValue
case .penny:
coinsInDollar = CoinType.penny.rawValue
case .dime:
coinsInDollar = CoinType.dime.rawValue
case .quarter:
coinsInDollar = CoinType.quarter.rawValue
}
print("I need \(coinsInDollar) nickles to make a dollar")
```

## Question 7

a) Write an enum called `DayOfWeek` to represent the days of the week with a raw value of type String.

b) Given the array `poorlyFormattedDays`, write code that will produce an array of enums that match the days.

`let poorlyFormattedDays = ["MONDAY", "wednesday", "Sunday", "monday", "Tuesday", "WEDNESDAY", "thursday", "SATURDAY", "tuesday", "FRIDAy", "Wednesday", "Monday", "Friday", "sunday"]`

```swift
func properFormat(arr: [String]) -> [DayOfWeek] {
var newArr: [DayOfWeek] = []
for a in arr {
switch a.lowercased() {
case DayOfWeek.Monday.rawValue.lowercased():
newArr.append(DayOfWeek.Monday)
case DayOfWeek.Tuesday.rawValue.lowercased():
newArr.append(DayOfWeek.Tuesday)
case DayOfWeek.Wednesday.rawValue.lowercased():
newArr.append(DayOfWeek.Wednesday)
case DayOfWeek.Thursday.rawValue.lowercased():
newArr.append(DayOfWeek.Thursday)
case DayOfWeek.Friday.rawValue.lowercased():
newArr.append(DayOfWeek.Friday)
case DayOfWeek.Saturday.rawValue.lowercased():
newArr.append(DayOfWeek.Saturday)
case DayOfWeek.Sunday.rawValue.lowercased():
newArr.append(DayOfWeek.Sunday)
default:
newArr.append(DayOfWeek.Monday)
}
}
return newArr
}
var new = properFormat(arr: poorlyFormattedDays)
print(new)
```

c) Write a method in `DayOfWeek` called `isWeekend` that determines whether a day is part of the weekend or not and write code to calculate how many week days appear in `poorlyFormattedDays`.

```swift
func isWeekend(day: DayOfWeek) -> String {
switch day {
case .Saturday:
return "is weekend"
case .Sunday:
return "is weekend"
default:
return "is week day"
}
}
func weekDays(days: [String]) -> Int {
var count = 0
let proper = properFormat(arr: days)
for a in proper{
switch isWeekend(day: a){
case "is week day":
count += 1
default:
count += 0
}
}
return count
}

weekDays(days: poorlyFormattedDays)
```


## Question 8

a) Create an enum called `MetroLine` with cases for the colors of the metro train lines. Create an instance of `MetroLine`.

```swift
enum MetroLine {
case purple
case green
case yellow
case red
case gray
}

var theSeven = MetroLine.purple
```

b) Modify your enum so that each case has an associated value of either Character or Int that will represent the train on that line. Create a new instance of `MetroLine` and give it an appropriate train letter or number.

```swift
enum MetroLine {
case purple(Int)
case green(Int)
case yellow(Character)
case red(Character)
}
var yellowTrain = MetroLine.yellow("N")
```

c) Write code that prints the train letter or number of your instance of `MetroLine`.

```swift
var yellowTrain = MetroLine.yellow("N")

switch yellowTrain {
case .green(let train):
print(train)
case .purple(let train):
print(train)
case .yellow(let train):
print(train)
case .red(let train):
print(train)
}
```

## Question 9

a) Think of your own example of something that can be modeled as an enum and write it. Remember that enums allow you to create instances of a defined list of cases.

b) Add a method to your enum.... try to have the method make sense.

```swift
enum Pokemon {
case pikachu(String)
case eevee(String)
case mew(String)
case bulbasaur(String,String)
}

var myPokemon = Pokemon.pikachu("electric")

switch myPokemon {
case .eevee(let type):
print("My partner Pokemon is Eevee an its type is \(type)")
case .mew(let type):
print("My partner Pokemon is Mew an its type is \(type)")
case .bulbasaur(let type1, let type2):
print("My partner Pokemon is Bulbasaur an its types are \(type1) and \(type2)")
case .pikachu(let type):
print("My partner Pokemon is Pikachu an its type is \(type)")
}
```
