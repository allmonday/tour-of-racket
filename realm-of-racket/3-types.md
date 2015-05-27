## building blocks 

boolean

```racket
(zero? 1)
```

symbols

```racket
(symbol=? 'foo 'Foo)
;;; => f
```

numbers

```racket
(expt 2 10)
;;; => 1024
(sqrt -1)
(/ 4 6)
;;; => 2/3
(/ 4.0 6)
```

strings

```racket
"tutti fruitti"
(string-append "tutti" "frutti")
```

lists

```racket
empty
'()
(list)

(cons 'chicken empty)
(cons 'chicken '())

(cons 'pork '(beef chicken))
(list 'port 'beef 'chicken)

;;; first and rest
(first (list 'port 'beef 'chicken)) ;;; => 'pork
(rest (list 'port 'beef 'chicken))  ;;; => '(beef chicken)

```


nestted lists

```racket
(list 'cat (list 'duck 'bat) 'ant)
;;; => '(cat (duck bat) ant)
```


structs

```racket
(struct student (name id# dorm))
(define freshman (student 'Joe 1234 'NewHall))
(student-name freshman)
```

```racket
;;; list of struct
(struct student (name id# dorm))
(define mimi (student 'Mimi 1234 'NewHal))
(define nicole (student 'Nicole 5678 'NewHall))
(define eric (student 'Eric 4332 'NewHall))
(define in-class (list mimi nicole eric))
(student-id# (third in-class))
```

nested struct

```racket
(define freshman1 (student 'Kikodo 123 'OldHall))

(struct student-body (freshmen sophomores juniors seniors))
(define all-students
    (student-body (list freshman1 (student 'Mary 0101 'OldHall))
                  (list (student 'Jeff 5678 'OldHall))
                  (list (student 'Bob 4321 'Apartment))
                  empty))

(student-name (first ( student-body-freshmen all-students)))                
```


struct transparent

```racket
(struct example2 (p q r) #:transparent)
(define ex2 (example2 9 8 7))
ex2
```

