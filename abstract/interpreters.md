# [Abstracting Definitional Interpreters: Functional Pearl](https://plum-umd.github.io/abstracting-definitional-interpreters/)

```
e ∈ exp     ::=    (vbl x)         [variable]
             |     (num n)      [conditional]
             |     (if0 e e e)    [binary op]
             |     (app e e)    [application]
             |     (rec x e)    [rec binding]
             |     (lam x e)  [function defn]
x ∈ var     ::=     x, y,...  [variable name]
b ∈ bin     ::=     +, -,...    [binary prim]
```

```haskell
(define ((ev ev) e)
  (match e
    [(num n)        (return n)]
    [(vbl x)        (do ρ ← ask-env
                        (find (ρ x)))]
    [(if0 e₀ e₁ e₂) (do v  ← (ev e₀)
                        z? ← (zero? v)
                        (ev (if z? e₁ e₂)))]
    [(op2 o e₀ e₁)  (do v₀ ← (ev e₀)
                        v₁ ← (ev e₁)
                        (δ o v₀ v₁))]
    [(rec f e)      (do ρ  ← ask-env
                        a  ← (alloc f)
                        ρ′ ≔ (ρ f a)
                        v  ← (local-env ρ′ (ev e))
                        (ext a v)
                        (return v))]
    [(lam x e₀)     (do ρ ← ask-env
                        (return (cons (lam x e₀) ρ)))]
    [(app e₀ e₁)    (do (cons (lam x e₂) ρ) ← (ev e₀)
                        v₁ ← (ev e₁)
                        a  ← (alloc x)
                        (ext a v₁)
                        (local-env (ρ x a) (ev e₂)))]))
```

```haskell
(define (δ o n₀ n₁)
  (match o
    ['+ (return (+ n₀ n₁))]
    ['- (return (- n₀ n₁))]
    ['* (return (* n₀ n₁))]
    ['/ (if (= 0 n₁) fail (return (/ n₀ n₁)))]))
(define (zero? v) (return (= 0 v)))
```