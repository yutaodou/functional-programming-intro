- ### Programming Paradigm
- ### Functional programming

#### 1. High order functions

```java
List<Integer> values = newArrayList(11, 2, 43, 14, 5, 76, 6);

Collections.sort(values, new Comparator<Integer>() {
	@Override
	public int compare(Integer one, Integer other) {
	    return one.compareTo(other);
	}
});    

// After Java 8
Collections.sort(values, (a, b) -> a.compareTo(b));
```

```haskell
add :: a -> a -> a
add a b = a + b

perform :: a -> a -> (a -> a -> a) -> a
perform a b action = action a b

let result = perform 1 1 add 	
-- result = 2


-- 函数可以作为参数传递以后.....
-- Function composition
(.) :: (b -> c) -> (a -> b) -> c
(.) f g x = f(g(x))

plus :: a -> a
plus x = x + 1

double :: a -> a
double x = x * 2

plusThenDouble = double.plus

let result = plusThenDouble 1
// result = 4
```

#### 2. Currying 科里化

```javascript
function add(x, y) {
	return x + y;
}

// add(1, 1)
// add(1, 2)
// add(1, 3)
// add(1, 4)
// add(1, 5)

var addOne = function(y){
	return function(){
		return add(1, y);
	}
}

// addOne(1)
// addOne(2)
// addOne(3)
// addOne(4)
```

```haskell
add :: a -> (a -> a)
add a b = a + b

addOne :: a -> a
addOne = add 1
-- addOne 1
-- addOne 2
-- addOne 3

-- real world examples
map (*2) [1..10]
```

#### 3. Concise and expressive

 ```haskell
 let squareTriangles = [(a,b,c) | a <- [1..10], b <- [1..10], c <- [1..10], a*a + b*b == c*c]
 ```

#### 4. Tail recursion
```java
private static Integer factorial(int num) {
    if (num == 1) {
        return 1;
    }
    return num * factorial(num - 1);
}

Integer result = factorial(10);
// result = 3628800

private static Integer factorial2(int accu, int num) {
    if (num == 1) {
        return accu;
    }
    return factorial2(accu * num, num - 1);
}

Integer result = factorial2(1, 10);
// result = 3628800
```

```haskell
let values = [1..10]
let result = foldl (\x y -> x * y) 1 values
-- result = 3628800
```

#### 5. Pattern Matching
```haskell
data Category = Book | Food | Medical | Other

data Product = Product String Float Category

getTax :: Product -> Float
getTax product = case product of
	(Product _ price Book) -> price * 0.05 // 书籍适用税率0.05
	(Product _ _ Food) -> 0.0	// 食品免税
	(Product _ _ Medical) -> 0.0 // 药品免税
	(Product _ price _) -> price 0.1 // 其他商品 0.1消费税
```

#### 6. Pure function

我们可以说一个函数是纯函数，如果它满足一下两个条件：
- 输出结果只依赖于输入参数，相同的输入参数总能得到相同的输出结果。
- 函数的执行不对外产生任何副作用，不修改可变对象状态或者输出。
