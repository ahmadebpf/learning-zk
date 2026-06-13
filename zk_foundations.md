# zk_foundations.md

# ZK Foundations Notebook

This notebook is the source of truth for foundational concepts learned while studying zero-knowledge proofs, finite fields, constraint systems, and zk-SNARKs.

---

# Glossary

- q: Modulus or field order (often prime)
- p: Prime number
- F_q: Finite field of order q
- Z_q: Integers modulo q
- ∈: Set membership
- ≡: Congruence modulo q
- ∧: Logical AND
- ∨: Logical OR
- ¬: Logical NOT
- ⟨a,b⟩: Inner product
- ∘: Hadamard product

---

# Sets and Logic

## Set
A collection of distinct elements.

## Subset
A ⊆ B if every element of A is also in B.

## Proper Subset
A ⊂ B if A ⊆ B and A ≠ B.

## Membership
x ∈ A means x belongs to A.

## Union
A ∪ B contains elements in either set.

## Intersection
A ∩ B contains elements in both sets.

## Set Membership as a Constraint

x ∈ {a,b,c}

can be expressed as:

(x-a)(x-b)(x-c)=0

---

# Boolean Constraints

To force x to be Boolean:

x(x-1)=0

Solutions:

x ∈ {0,1}

## Boolean Arithmetic

AND:
x ∧ y = xy

NOT:
¬x = 1-x

OR:
x ∨ y = x+y-xy

Example:

(x ∧ y) ∨ ¬u

can be encoded as:

a1 = xy
a2 = 1-u
out = a1 + a2 - a1*a2

---

# Modular Arithmetic

## Congruence

a ≡ b (mod q)

means q divides (a-b).

Equivalent:

a and b have the same remainder modulo q.

Example:

3 ≡ -8 (mod 11)

## Congruence Class

A congruence class modulo q is the set of all integers that have the same remainder when divided by q.

Example:

[3] mod 11 = {...,-19,-8,3,14,25,...}

## Additive Inverse

The additive inverse of x modulo q is:

-x ≡ q-x (mod q)

Example:

3⁻ (mod 11) = 8

## Multiplicative Inverse

x⁻¹ satisfies:

xx⁻¹ ≡ 1 (mod q)

Python:

pow(x, -1, q)

## Rational Numbers Modulo q

n/m ≡ n·m⁻¹ (mod q)

Python:

(n * pow(m, -1, q)) % q

For:

-n/m

Python:

(-n * pow(m, -1, q)) % q

## Solving Linear Equations

ax+b ≡ c (mod q)

x ≡ (c-b)a⁻¹ (mod q)

Python:

(c-b) * pow(a, -1, q) % q

---

# Groups and Fields

## Magma

Closure only.

## Semigroup

Closure + Associativity.

## Group

A set with a binary operation satisfying:

- Closure
- Associativity
- Identity
- Inverses

## Trivial Group

A group with exactly one element.

## Finite Field

A field is a set with two binary operators, where:

- The set forms an abelian group under addition.
- The nonzero elements form an abelian group under multiplication.

Equivalent memory definition:

A field is a set with two binary operators, where each binary operator forms a group with respect to the set, except that the multiplication group excludes 0.

## Field Orders

Finite fields exist only for:

q = p^n

where p is prime and n ≥ 1.

No field exists with 15 elements because:

15 = 3 × 5

is not a prime power.

---

# Linear Algebra

## Vector

An ordered collection of values.

## Hadamard Product

Element-wise multiplication.

(a,b,c) ∘ (d,e,f)

=

(ad, be, cf)

## Inner Product

⟨a,b⟩ = Σ aᵢbᵢ

Produces a scalar.

Relationship:

Inner Product = Sum(Hadamard Product)

## Matrix-Vector Multiplication

Each output entry is the inner product of:

- a matrix row
- the vector

---

# Fast Exponentiation

## Binary Exponentiation

50 = 32 + 16 + 2

Therefore:

g^50 = g^32 · g^16 · g^2

Compute:

g²
g⁴=(g²)²
g⁸=(g⁴)²
g¹⁶=(g⁸)²
g³²=(g¹⁶)²

Then multiply the required powers.

---

# Discrete Logarithms

Given:

g^x ≡ y (mod q)

The discrete logarithm is x.

## Discrete Log Assumption

Given g and g^x, recovering x is computationally infeasible for classical computers.

## Quantum Computing

Shor's algorithm can efficiently solve discrete logarithms on sufficiently powerful quantum computers.

## Order / Period

The order r of g is the smallest positive integer satisfying:

g^r ≡ 1 (mod q)

Period finding is central to Shor's algorithm.

---

# Common Mistakes

## Congruence Class

Incorrect:
"The two values when added together result in congruence to q."

Correct:
A congruence class modulo q is the set of all integers with the same remainder modulo q.

## Inner Product vs Hadamard Product

Incorrect:
They are the same operation.

Correct:
Hadamard product is element-wise multiplication.
Inner product is the sum of the Hadamard product elements.

## Discrete Logarithm

Incorrect:
The discrete logarithm is the value g^x.

Correct:
The discrete logarithm is the exponent x.
