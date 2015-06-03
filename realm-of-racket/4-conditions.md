## is it .. ?

### return boolean

```racket
(zero? 42)  ;;; only Number
(symbol=? 'a 'b)  ;;; only symbol
```

### huh?

```racket
(struct student (name id# dorm) #:transparent)
(define sophomore3 (student 'David 100234 'PG))
(student-name sophomore3) ;;; => 'David

(student? 'a) ;;; => #f
(student? sophomore3)   ;;; => #t
(student? (student 1 2 3))  ;;; => #t
```

```racket
(number? 'a)
(number? 10)

(string? "hello world")
(symbol? 'a)
(symbol? 10)

(image? 10) ;;; #f
(boolean? "false") ;;; #f

(list? 'eh) ;;; #f
(cons? '(what is that about?))
(empty? 'a)

(real? 10)
(real? (sqrt -1))
(rational? 2/3)
(integer? 1.0)  ;;; #t
(integer? 1)

(exact-integer? 1.0) ;;; #f
```

### =?

```racket
(= 1 2)
(= (sqrt -1) 0+1i)
(boolean=? #f #f)
(string=? "hello world" "good bye")
(equal? (student 'David 100234 'PG) sophomore3)  ;;; 直接比较, = 则是转成number后比较
```

### if

`#f is false and anything that is not false is true`

```racket
(if (= 1 2) 
      'yup
      'nope)
;;; => 'nope
```

```racket
(if '(1)
      'everything-except-#f-counts-as-#t
      'aw-heck-no)
;;; => 'everything-except-#f-counts-as-#t

(if empty
      'everything-except-#f-counts-as-#t
      'aw-heck-no)
;;; => 'everything-except-#f-counts-as-#t

(if false
      'everything-except-#f-counts-as-#t
      'aw-heck-no)
;;; => 'aw-heck-no
```

if 后跟的表达式不会被预先 evaluate

```racket
(if (odd? 5)
      'odd-number
      (/ 1 0))
;;; => 'odd-number
```

### cond

```racket
(cond [(= x 7) 5]
        [(odd? x) 'odd-number]
        [else 'even-number])
;;; => 5
```


### recursion

```racket
(define (my-length a-list)
  (if (empty? a-list)
      0
      (add1 (my-length (rest a-list)))))
  
(my-length '(list of fou symbols))
```

### tricks with cond

```racket
(and #t #f #f)
(or #t #f #f)


(define is-it-even #f)
(or (odd? 5) (set! is-it-even #t))
(and (even? x) (set! is-it-even #t))


;;; usual way
(if file-modified
    (if (ask-user-about-saving)
        (save-file)
        false)
    false)

;;; concise way
(and file-modified (ask-user-about-saving) (save-file))

;;; another
(when (and file-modified (ask-user-about-saving))
    (save-file))

(define tasks '(1 clean 3 homework 4 party))
(member 3 tasks)
;;; => '(3 homework 4 party)

```

### Equality

```racket
(struct point (x y) #:transparent)
(define (distance-to-origin p)
  (sqrt (+ (sqr (point-x p)) (sqr (point-y p)))))
(distance-to-origin (point 3 4))
;;; => 5

(define pt1 (point 1 2))
(define pt2 (point 1 2))
(equal? pt1 pt2)
;;; => #t  比较每一个元素, 比较值

(eq? pt1 pt2)
;;; => #f
(eq? pt1 pt1)
;;; => #t  比较引用
```

### test

```racket
(require rackunit)
(check-equal? (add1 5) 7)
```
output
```
--------------------
FAILURE
actual:     6
expected:   7
name:       check-equal?
location:   (unsaved-editor1936 3 0 33 25)
expression: (check-equal? (add1 5) 7)
```

```racket
;;; with message
(check-equal? 5 6 "NUMBERS MATTER!")
```

- `check-not-equal`
- `check-pred`
  ```racket
  (define number 4)
  (check-pred number? 4)
  ```
- `check-=`  within certain range
- `check-true`
- `check-false`
- `check-not-false`
