## Chapter 1: Starting Out

### Functions

#### Func Call

```haskell
div 92 10 --get 9
82 `div` 10 --the same
```

#### Func Def

```haskell
doubleMe x = x + x --func name must begin with lowercase
hello = "hello" --a function without any parameter is a definition (or a name)
doubleSmallNumber x = if x > 100 then x else 2 * x --else part is mandatory
```

### List

#### Basic List

```haskell
lostNumbers = [4,8,15,16,23,42]
```

#### List Operations

- Concat

```haskell
[1,2,3,4] ++ [9,10,11,12] --get [1,2,3,4,9,10,11,12]
'A':" SMALL CAT" --get "A SMALL CAT"
```

- Access Element

```haskell
[9.4,33.2,96.2,11.2,23.25] !! 1 --get 33.2
```

- Compare

> The order of the two lists is determined by the order of the first pair of differing elements.

```haskell
[3,2,1] > [2,1,0] --True
[3,4,2] > [2,4] --True
```

- Other Operations
  - length
  - null
  - reverse
  - take
  - drop
  - maximum
  - minimum
  - sum
  - product
  - elem
  - head
  - tail
  - last
  - init
  - cycle 
  - repeat
  - replicate

#### Ranges

```haskell
['a'..'z'] --"abcdefghijklmnopqrstuvwxyz"
[1..20] --[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
[20,19..1] --reverse above 
[3,6..20] --[3,6,9,12,15,18]
take 24 [13,26..]
take 10 (cycle [1,2,3]) --[1,2,3,1,2,3,1,2,3,1]
```

#### List  Comprehension

```haskell
[x*2 | x <- [1..10]] --[2,4,6,8,10,12,14,16,18,20]
[x*2 | x <- [1..10], x*2 >= 12] --[12,14,16,18,20]
[x+y | x <- [1,2,3], y <- [10,100,1000]] --[11,101,1001,12,102,1002,13,103,1003]
```

### Tuple

```haskell
rightTriangles = [ (a,b,c) | c <- [1..10], a <- [1..c], b <- [1..a], a^2 + b^2 == c^2]
--[(4,3,5),(8,6,10)]
```

#### Tuple Functions

- fst, snd (for pair)
- zip



## Chapter 2: Believe the Type


###  Explicit Type Declaration

```haskell
ghci> :t 'a' 
'a' :: Char 
ghci> :t True 
True :: Bool 
ghci> :t "HELLO!" 
"HELLO!" :: [Char] 
ghci> :t (True, 'a')
(True, 'a') :: (Bool, Char) 
ghci> :t 4 == 5 
4 == 5 :: Bool

addThree :: Int -> Int -> Int -> Int 
addThree x y z = x + y + z
```



### Common Types

- Int, Integer (unbounded)
- Float, Double
- Bool
- Char
- Tuples (max elements = 62)
- Empty Tuple : ()

### Type Variable and Type Class
```haskell
ghci> :t (==) 
(==) :: (Eq a) => a -> a -> Bool
```

>  Everything before => symbol is called a class constraint.

####  Common type classes

Eq, Odd, Show, Read, Enum, Bounded, Num, Floating, Intergral



## Chapter 3: Syntax in Functions

### Pattern Matching

```haskell
sayMe :: Int -> String 
sayMe 1 = "One!" 
sayMe 2 = "Two!" 
sayMe 3 = "Three!" 
sayMe 4 = "Four!" 
sayMe 5 = "Five!" 	w
sayMe x = "Not between 1 and 5"
-- Note that if we moved the last pattern (sayMe x) to the top, the function
-- would always print "Not between 1 and 5",

factorial :: Int -> Int 
factorial 0 = 1 
factorial n = n * factorial (n - 1)

addVectors (x1, y1) (x2, y2) = (x1 + x2, y1 + y2)
first :: (a, b, c) -> a 
first (x, _, _) = x

ghci> let xs = [(1,3),(4,3),(2,4),(5,3),(5,6),(3,1)] 
ghci> [a+b | (a, b) <- xs] 
[4,7,6,8,11,4]

head' :: [a] -> a 
head' [] = error "Can't call head on an empty list, dummy!"
head' (x:_) = x

firstLetter :: String -> String firstLetter "" = "Empty string, whoops!" firstLetter all@(x:xs) = "The first letter of " ++ all ++ " is " ++ [x]
```

### Guards

```haskell
myCompare :: (Ord a) => a -> a -> Ordering 
a `myCompare` b 
  | a == b = EQ 
  | a <= b = LT 
  | otherwise = GT
```

### Where Keyword

```haskell
bmiTell :: Double -> Double -> String 
bmiTell weight height 
    | bmi <= 18.5 = "You're underweight, you emo, you!" 
    | bmi <= 25.0 = "You're supposedly normal. Pffft, I bet you're ugly!" 
    | bmi <= 30.0 = "You're fat! Lose some weight, fatty!" 
    | otherwise = "You're a whale, congratulations!" 
where bmi = weight / height ^ 2
```


#### where bindings aren’t shared across function bodies of different patterns

```haskell
-- Counterexample
greet :: String -> String
greet "Juan" = niceGreeting ++ " Juan!" 
greet "Fernando" = niceGreeting ++ " Fernando!" 
greet name = badGreeting ++ " " ++ name 
    where niceGreeting = "Hello! So very nice to see you,"
          badGreeting = "Oh! Pfft. It's you."
```

#### Pattern Matching with where

```haskell
initials :: String -> String -> String 
initials firstname lastname = [f] ++ ". " ++ [l] ++ "."
	where (f:_) = firstname 
		  (l:_) = lastname
```

#### Functions in where Blocks

```haskell
calcBmis :: [(Double, Double)] -> [Double] 
calcBmis xs = [bmi w h | (w, h) <- xs] 
	where bmi weight height = weight / height ^ 2
```



### Let Keyword

```haskell
cylinder :: Double -> Double -> Double 
cylinder r h = 
	let sideArea = 2 * pi * r * h 
		topArea = pi * r^2
	in sideArea + 2 * topArea
```



#### Let expressions vs Where bindings

- Let expressions are **expressions** (has a value)
- Let expression are local to **guards**, where bindings are local to **patterns**

#### Let expression use cases

- introduce functions in a local scope

```haskell
[let square x = x * x in (square 5, square 3, square 2)]
-- [(25,9,4)]
```

- They can be separated with semicolons, which is helpful when you want to bind several variables inline and can’t align them in columns:

```haskell
(let a = 100; b = 200; c = 300 in a*b*c, let foo="Hey "; bar = "there!" in foo ++ bar)
--(6000000,"Hey there!")
```

- Pattern matching with let expressions can be very useful for quickly dismantling a tuple into components and binding those components to names
```haskell
(let (a, b, c) = (1, 2, 3) in a+b+c) * 100 
--600
```

#### let in List Comprehensions

```haskell
calcBmis :: [(Double, Double)] -> [Double] 
calcBmis xs = [bmi | (w, h) <- xs, let bmi = w / h ^ 2]
```

### Case Expressions

```haskell
head' :: [a] -> a 
head' [] = error "No head for empty lists!" 
head' (x:_) = x

--equivalent:
head' :: [a] -> a 
head' xs = case xs of [] -> error "No head for empty lists!" 
					(x:_) -> x
```

### Declaration vs. expression style
> https://wiki.haskell.org/Declaration_vs._expression_style

## Chapter 4: Hello Recursion!

### Maximum Awesome

```haskell
maximum' :: (Ord a) => [a] -> a 
maximum' [] = error "maximum of empty list!" 
maximum' [x] = x 
maximum' (x:xs) = max x (maximum' xs)
```

### Quick Sort

```haskell
quicksort :: Ord a => [a] -> [a]
quicksort [] = []
quicksort (x:xs) = quicksort smallerOrEq ++ [x] ++ quicksort larger
    where smallerOrEq = [x' | x' <- xs, x' <= x]
          larger = [x' | x' <- xs, x' > x]
```

## Chapter 5: Higher-Order Functions

### Curried Functions

> Every function in Haskell officially takes only one parameter.
>
> All the functions we’ve used so far that accepted multiple parameters have been curried functions. 
>
> A curried function is a function that, instead of taking several parameters, always takes exactly one parameter.
>
> Then when it’s called with that parameter, it returns a function that takes the next parameter, and so on.



```haskell
compareWithHundred :: Int -> Ordering 
compareWithHundred  = compare 100
--compareWithHundred 99 --GT

divideByTen :: (Floating a) => a -> a 
divideByTen = (/10)
--divideByTen 200 --20.0
```

#### Sections

> **Infix** functions can also be partially applied by using **sections**. To section an infix function, simply surround it with **parentheses** and supply a parameter on **only one side**. That creates a function that takes one parameter and then applies it to the side that’s missing an operand.

```haskell
isUpperAlphanum :: Char -> Bool 
isUpperAlphanum = (`elem` ['A'..'Z'])
```



### Some Higher-Orderism Is in Order

```haskell
ghci> applyTwice f x = f (f x)
ghci> :t applyTwice
applyTwice :: (t -> t) -> t -> t

ghci> applyTwice (+3) 10 
16

ghci> applyTwice (++ " HAHA") "HEY" 
"HEY HAHA HAHA" 

ghci> applyTwice ("HAHA " ++) "HEY" 
"HAHA HAHA HEY" 

ghci> applyTwice (multThree 2 2) 9 
144

ghci> applyTwice (3:) [1] 
[3,3,1]
```

