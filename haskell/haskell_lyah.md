## Functions

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

## List

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

## Tuple

```haskell
rightTriangles = [ (a,b,c) | c <- [1..10], a <- [1..c], b <- [1..a], a^2 + b^2 == c^2]
--[(4,3,5),(8,6,10)]
```

#### Tuple Functions

- fst, snd (for pair)
- zip

## Types

#### Use GHCi to examine type (:t)

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
```

#### Common Types

- Int, Integer
- Float, Double
- Bool
- Char
- Tuples (max elements = 62)
- Empty Tuple : ()

#### Explicit Declartion

#### Type Class
```

```