


Lisp uses applicative-order evaluation

- *normal-order evaluation* :  fully expand and then reduce

- *applicative-order evaluation*： evaluate the arguments and then apply



- square root of x

  improve:　$(guess + \frac {x} {guess}) / 2$

  

- cube root of x

  improve: $(2guess + \frac {x} {guess^2})/3$






## Exercise 1.8 

cube root of x

There are still the cube-root of 0 (and cube-root of 100) convergence problem, where the answer approaches 0 (or 100) but never reaches it. 

```scheme
(define (cube-iter guess x)
  (if (good-enough? guess x)
      guess
      (cube-iter (improve guess x) x)
   )
)

(define (improve guess x)
  (/ (+ (* 2 guess) (/ x (* guess guess))) 3)
)

(define (good-enough? guess x)
 ; (< (abs (- (* guess guess guess) x)) 0.001)
 ; Based on Exerciese 1.7
 ; iterates until guess and next guess are equal,
 ; automatically produces answer to limit of system precision
  (= (improve guess x) guess)
)

(define (cube x)
  (cube-iter 1.0 x)
)
```



## 1.2 Procedures and the Processes They Generate


### fib

- recursive

```scheme
(define (fib n)
  (cond (= n 0) 0)
  (cond (= n 1) 1)
  (else (+ fib(- n 1) fib(- n 2))
)
```

- iterate

```scheme
(define (fib n)
  (fib-iter 1 0 n))

(define (fib-iter a b count)
  (if (= count 0)
      b
      (fib-iter (+ a b) a (- count 1))))
```

### Exercise 1.9

The easiest way to spot that the first process is recursive (without writing out the substitution) is to note that the "+" procedure calls itself at the end while nested in another expression; the second calls itself, but as the top expression.

```scheme
(define (+ a b)
  (if (= a 0)
      b
      (inc (+ (dec a) b))))

 (+ 4 5) 
 (inc (+ (dec 4) 5)) 
 (inc (+ 3 5)) 
 (inc (inc (+ (dec 3) 5))) 
 (inc (inc (+ 2 5))) 
 (inc (inc (inc (+ (dec 2) 5)))) 
 (inc (inc (inc (+ 1 5)))) 
 (inc (inc (inc (inc (+ (dec 1) 5))))) 
 (inc (inc (inc (inc (+ 0 5))))) 
 (inc (inc (inc (inc 5)))) 
 (inc (inc (inc 6))) 
 (inc (inc 7)) 
 (inc 8) 
  
 9 
```



```scheme
(define (+ a b)
  (if (= a 0)
      b
      (+ (dec a) (inc b))))

(+ 4 5)
(+ (dec 4) (inc 5))
(+ 3 6)
(+ (dec 3) (inc 6))
(+ 2 7)
(+ (dec 2) (inc 7))
(+ 1 8)
(+ (dec 1) (inc 8))
(+ 0 9)

9
```



### Exercise 1.10





### Exercise 1.11

- recursive

```scheme
(define (f n)
  (if (< n 3) n
  (+ (f (- n 1))
     (* 2 (f (- n 2)))
     (* 3 (f (- n 3))))))
```

- iterate

```scheme
(define (f n)
  (f-iter 2 1 0 n))

(define (f-iter a b c n)
  (if ( = n 0)
      c
      (f-iter (+ a (* 2 b) (* 3 c)) a b (- n 1))))
```



### Exercise 1.12



```scheme
(define (pascal col row)
  (cond ((= col 0) 1)
        ((= col row) 1)
        ((> col row) 0)
        (else (+ (pascal col (- row 1)) (pascal (- col 1) (- row 1))))))
```



## 1.2.4 Exponentiation



```scheme
(define (exp b n)
  (if (= n 0)
      1
      (* b (exp b (- n 1)))))
```



```scheme
(define (exp b n)
  (exp-iter b n product))

(define (exp-iter b n product)
  (if (= n 0)
      product
      (exp-iter b (- n 1) (* b product))))
```



```scheme
(define (gcd (a b))
  (if (= b 0)
      a
      (gcd b (remainder a b))))
``` 

## Exercise 2.2

```scheme
;; Point
(define (make-point x y)
    (cons x y))

(define (x-point point)
    (car point))
    
(define (y-point point)
    (cdr point))
 
;; Segment
(define (make-segment pointA pointB)
    (cons pointA pointB))

(define (start-segment segment)
    (car segment))

(define (end-segment segment)
    (cdr segment))

(define (average x y)
    (/ (+ x y) 2.0))

(define (midpoint-segment segment)
    (let ((pointA (start-segment segment))
        (pointB (end-segment segment)))
        (make-point (average (x-point pointA) (x-point pointB))
                    (average (y-point pointA) (y-point pointB))))
    )

;; Testing
(define (print-point p)
  (newline)
  (display "(")
  (display (x-point p))
  (display ",")
  (display (y-point p))
  (display ")"))

;; Auxiliary
(define (square x)
    (* x x))

;; Rectangle
(define (make-rectangle long-side short-side)
    (cons long-side short-side))

(define (lenth side)
    (let ((x1 (car (car side)))
        (y1 (cdr (car side)))
        (x2 (car (cdr side)))
        (y2 (cdr (cdr side))))
        (sqrt (+ (square (- x1 x2)) (square (- y1 y2))))))

(define (compute-perimeter rectangle)
    (let ((lenth-of-long (lenth (car rectangle)))
        (lenth-of-short (lenth (cdr rectangle))))
        (* 2 (+ lenth-of-long lenth-of-short))))

(define (compute-area rectangle)
    (let ((lenth-of-long (lenth (car rectangle)))
        (lenth-of-short (lenth (cdr rectangle))))
        (* lenth-of-long lenth-of-short)))

;; Testing
(define (print-info rectangle)
    (newline)
    (display "perimeter: ")
    (display (compute-perimeter rectangle))
    (newline)
    (display "area: ")
    (display (compute-area rectangle)))
    
(define long-side 
    (make-segment (make-point 1 2) (make-point 1 4)))
(define short-side 
    (make-segment (make-point 1 2) (make-point 12 2)))

(define rectangle-foo
    (make-rectangle long-side short-side))


(print-info rectangle-foo)

```


...This point is illustrated strikingly by the fact that we could implement cons, car, and cdr without using any data structures at all but only **using procedures**. 

```scheme
(define (cons x y) 
    (lambda (m) (m x y)))

(define (car z)
    (z (lambda (p q) p)))

(car (cons x y))
((cons x y) (lambda (p q) p))
```
## 2.1.4 Extended Exercise: Interval Arithmetic

```scheme
(define (make-interval a b) (cons a b))

(define (add-interval x y)
  (make-interval (+ (lower-bound x) 
                    (lower-bound y))
                 (+ (upper-bound x) 
                    (upper-bound y))))

(define (mul-interval x y)
  (let ((p1 (* (lower-bound x) 
               (lower-bound y)))
        (p2 (* (lower-bound x) 
               (upper-bound y)))
        (p3 (* (upper-bound x) 
               (lower-bound y)))
        (p4 (* (upper-bound x) 
               (upper-bound y))))
    (make-interval (min p1 p2 p3 p4)
                   (max p1 p2 p3 p4))))

;; Exercise 2.7
(define (upper-bount interval)
    (cdr interval))

(define (lower-bound interval)
    (car interval))

;; Exercise 2.8
(define (sub-interval x y)
    (make-interval (abs (- (car x) (cdr y)))
        (abs (- (cdr x) (car y)))))

;; Exercise 2.10
(define (div-interval x y)
    (if (<= (upper-bound y) (lower-bound y))
        (error "Invalid interval" y)
        (mul-interval x 
                (make-interval 
                    (/ 1.0 (upper-bound y)) 
                    (/ 1.0 (lower-bound y))))))
```

```scheme
;; Exercise 2.17
(define (last-pair l)
    (let ((rest (cdr l)))
    (if (null? rest)
        l
        (last-pair rest))))

;; Testing
(last-pair (list 23 72 12 32))

;; Exercise 2.18
(define (reverse l)
    (cons (last-pair l)))
```
## Hierachical Data and the Closure Property

### Exercise 2.17

```scheme
(define (last-pair list_arg)
  (if (null? (cdr list_arg))
      (car list_arg)
      (last-pair (cdr list_arg))))
```

### Exercise 2.18

```scheme
(define (append list1 list2)
  (if (null? list1)
      list2
      (cons (car list1) 
            (append (cdr list1) 
                    list2))))

(define (reverse list_arg)
    (if (null? (cdr list_arg))
        (list_arg)
        (append (reverse (cdr list_arg)
            (car list_arg)))))
```

### Exercise 2.28

```scheme
(define (fringe tree)
    (define nil '()))
    (if (null? tree)
        (let ((first (car tree)))
            (if not (pair? first)
                (cons first (fringe (cdr tree)))
                (append (fringe first) (fringe (cdr tree))))))))

```
### Exercise 2.19

```scheme
(define (first-denomination coin-values)
    (car coin-values))
(define (except-first-denomination coin-values)
    (cdr coin-values))
(define (no-more? coin-values)
    (null? coin-values))

(define (cc amount coin-values)
  (cond ((= amount 0) 
         1)
        ((or (< amount 0) 
             (no-more? coin-values)) 
         0)
        (else
         (+ (cc 
             amount
             (except-first-denomination 
              coin-values))
            (cc 
             (- amount
                (first-denomination 
                 coin-values))
             coin-values)))))
```

We should simply trust that it computes the factorial of `n-1`. Treating a recursive call as a functional abstraction has been called
a *recursive leap of faith*.