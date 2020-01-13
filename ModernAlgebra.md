# Modern Algebra 

Groups, Rings, Lattice ...

> [https://en.wikipedia.org/wiki/Semigroup](https://en.wikipedia.org/wiki/Semigroup)

|                    | Totality | Associativity | Identity | Invertibility | Commutativity |
| :----------------: | :------: | :-----------: | :------: | :-----------: | :-----------: |
|   Semi-groupoid    |          |   Required    |          |               |               |
|   Small Category   |          |   Required    | Required |               |               |
|      Groupoid      |          |   Required    | Required |   Required    |               |
|     Quasigroup     | Required |               |          |   Required    |               |
|       Magama       | Required |               |          |               |               |
|    Unital Magma    | Required |               | Required |               |               |
|        Loop        | Required |               | Required |   Required    |               |
|     Semi group     | Required |   Required    |          |               |               |
| Inverse Semi group | Required |   Required    |          |   Required    |               |
|       Monoid       | Required |   Required    | Required |               |               |
| Commutative monoid | Required |   Required    | Required |               |   Required    |
|       Group        | Required |   Required    | Required |   Required    |               |
|   Abelian Group    | Required |   Required    | Required |   Required    |   Required    |

Notes:

- Let $(S, \cdot)$ be a set $S$ equipped with a binary operator $\cdot$.
- Totality: Closure. $\forall x,y \in S$, $x \cdot y \in S$ 
- Associativity: $\forall x,y,z \in S$, $(x \cdot y) \cdot z = x \cdot (y \cdot z)$
- Identity: $\forall x \in S, \exist e \in S$
  - left identity: $e \cdot x = x$
  - right identity: $x \cdot e = x$
  - both: Identity
- Invertibility: $\forall x \in S$, $e$ is the identity element. $\exist y \in S$
  - left invertible: $y \cdot x = e$
  - right invertible: $x \cdot y = e$
  - both: invertible
- Commutativity: $\forall x,y \in S$, $x \cdot y = y \cdot x$