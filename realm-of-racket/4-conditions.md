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
