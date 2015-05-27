## 1. 前缀表达式

```racket
(+ 3 (* 2 4))
(+ 1 2 3 4 5)
'((1 2 3 4 5) (2 3 4 5 6))  ;;; list 会保持原样
```

## 2. define variable

```racket
(define (function-name argument-name ...) 
    function-body-expression
    function-body-expression
    ...)
```

### keywords

- set!

    ```racket 
    (define a 10)
    (set! a 20)
    ```
- define
