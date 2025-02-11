# Formal group theory

## Groups

<p>
  
  [https://crypto.stanford.edu/pbc/notes/group/group.html].
  
  We define a group $G^{\ast}$ as a set $G$ and a binary operation $\cdot$ having the following properties:

  1. For all $x, y \in G, x \cdot y \in G$. This is normally referred to as 'algebraic closure'.
  2. There exist an identity element $1 \in G$ such that $x \cdot 1 = x$ for all $x \in G$.
  3. The operation defined $(\cdot)$ is associative, that is, for all $x, y, z \in G$ we have $x(yz) = (xy)z$.
  4. For all $x \in G$ there exists an element $x^{-1}$ with $xx^{-1} = x^{-1}x = 1$ (the inverse). I proved this property here [https://github.com/Z323323/From-Fermat-to-the-group-theory?tab=readme-ov-file#proof-of-existence-and-uniqueness-of-inverses-in-z_p-and-z_phinast]. Note also that the formal definition of group doesn't imply we have a _finite_ group and it's therefore more general. The linked proof is about _finite_ multiplicative groups, which are the main interest for computer scientists.

  - If only $1,3$ holds for $G^{*}$ then $G^{\ast}$ is a semi-group.
  - If only $1, 2, 3$ holds for $G^{*}$ then $G^{\ast}$ is a monoid.

  In general if you see $G^{\ast}$ around in papers this will refer to a multiplicative group.

  If $G^{\ast}$ is commutative then

  5. For all $x, y \in G, xy = yx$

  and we call it _abelian_.

  ### Axioms

  1. Closure (not really trivial if you played around with Zn.py using $n$ non-prime).
  2. Associativity (trivial).
  3. Right and left cancellation:
     - $ax = bx$ iff $a = b$. This one is not that trivial if you think about _finite groups_ and therefore modular arithmetic [https://github.com/Z323323/From-Fermat-to-the-group-theory?tab=readme-ov-file#cancellation-law].
    
  ### Order

  The order of an element $g$ in a group $G$ is the smallest positive integer $k$ such that $g^{k} = 1$. We know this exists for all elements of $Z_{\phi(n)}^{\ast}$ (_finite groups_), while it doesn't for all elements of _infinite groups_ (holds only for $1$, at my current perspective).

  ### Subsets

  A subset $H$ of $G$ which satisfy the previous properties is called a subgroup of $G^{*}$. Every _finite group_ has two improper subgroups which are defined by the subsets $\\{1\\}$, and $G$. All other subgroups are defined as proper subgroups.

  We can write $H \leq G$ to refer to any subgroup of $G^{*}$ and if $H \neq G$ then $H < G$.
  
</p>


## Homomorphism and isomorphism

<p>
  
  An homomorphism is a map $f : G &rarr; H$ between two different groups where

  $f(x)f(y) = f(xy)$

  for all $x, y \in G$. If $f$ is bijective then $f$ is called **isomorphism**.

  Let's clarify this concept, since it looks really abstract, and it is indeed, and it's also really important in math.

  First thing to understand is the meaning of **map**, and the different kinds of map in mathematics.
  
  1. **map** = **function**. A function is a map which associates elements from a set (**domain**) to some elements of another set (**codomain**). The actual elements mapped will be elements $\in$ **codomain**, which are called **image** of the function/map, and so we could have **image = codomain** or not.

![Map](Map.SVG.png)

  2. A map/function has $2$ foundation constraints which defines it.
     - It can't have two mappings starting from the domain, it's exactly one map for every element of the domain, while it can for example has two elements which map the same element of the codomain/image.
     - Every element of the domain must be mapped (it's not true for the codomain).

  4. A map/function has different properties which define it's structure, it can be
     - **surjective**: every element of the codomain is mapped.
     - **injective**: every element of the domain maps $1$ and only $1$ element of the codomain.
     - **bijective**: if it's both surjective and injective.

  ![ISB](Inj_Surj_Bij.svg)
  
  Now let's get back to our omomorphism definition. An omomorphism is a particular mapping/function where its definition holds, that is, where the mapping $G &rarr; H$ must satisfy

  $(x \in G &rarr; H)(y \in G &rarr; H) = (xy \in G &rarr; H)$<br>
  $->$<br>
  $(x \in G &rarr; H)?_2(y \in G &rarr; H) = (x?_1y \in G &rarr; H)$<br>
  $->$<br>
  $(a \in H)?_2(b \in H) = (x?_1y \in G &rarr; H)$
  
  Here lie a couple behaviours which could not be straightforward at first sight, we can see that there are two implied relations $?_{1, 2}$ between $(a)?_2(b), a, b \in H$ and $x?_1y, x, y \in G$. This relation strongly affects the resulting property, and the reason of subscripts is because of the implied definitions

  $G^{?_1} = (\\{x, y, \dots \\}, ?_1)$<br>
  $H^{?_2} = (\\{a, b, \dots \\}, ?_2)$

  and because that relation (binary operation) will be defined individually for elements which belong to $G$ or $H$. Now, if we consider $G$ and $H$ as _multiplicative finite groups_ then the implied relation is exactly the same because the binary operation defined for _multiplicative finite groups_ is the same, but this is not true in general.
  
  #### Example

  Imagine the _infinite group_ $G$ defined over the positive integers towards infinity and $H$ being a _finite group_ $Z_{n}^{\ast}$ of order $n - 1$, thus $n$ is prime, we have

  $G = (\\{1, 2, \dots, \infty \\}, ?_1 = \cdot)$<br>
  $H = (\\{1, 2, \dots, n - 1 \\}, ?_2 = \cdot \mod n)$

  We define the omomorphism $f : G &rarr; H$ where $f(x) = x \mod n$, then we have

  $(x \in G &rarr; H)(y \in G &rarr; H) = (xy \in G &rarr; H)$<br>
  $->$<br>
  $(x \in G &rarr; H)?_2(y \in G &rarr; H) = (x?_1y \in G &rarr; H)$<br>
  $->$<br>
  $(x \mod n)?_2(y \mod n) = (x \cdot y \mod n)$<br>
  $->$<br>
  $(x \mod n) \cdot (y \mod n) \mod n = (x \cdot y \mod n)$

  which holds since [https://github.com/Z323323/From-Fermat-to-the-group-theory?tab=readme-ov-file#multiplication-property].

  This means that the set of positive integers is omomorphic to the set of positive integers $\mod n$ where $n$ is prime. Or stated in a different manner, there exists an omomorphism between the set of positive integers and the the set of positive integers $\mod n$ where $n$ is prime.

  Now, since our focus will be directed towards _finite multiplicative groups_ let's analyse the definition of homomorphism for two general finite groups $N = Z_{n}^{\ast}$, $M = Z_{m}^{\ast}$ where $n, m$ are prime numbers.

  $N = (\\{x, y, \dots, n - 1 \\}, \cdot \mod n)$<br>
  $M = (\\{a, b, \dots, m - 1 \\}, \cdot \mod m)$

  We can see that for multiplicative groups we can avoid the construction regarding the binary operator and just consider the modulo, then we define the omomorphism $f : N &rarr; M$, where $f(x)$ simply maps elements from the group $Z_{n}^{\ast}$ to $Z_{m}^{\ast}$.

  $(x \in N &rarr; M)(y \in N &rarr; M) = (xy \in N &rarr; M)$<br>
  $->$<br>
  $(x \mod n &rarr; M)(y \mod n &rarr; M) = (xy \mod n &rarr; M)$<br>
  $->$<br>
  $(a \mod m)(b \mod m) \mod m = (z \mod n) \mod m$

  Can you solve this in general? Because I can't honestly :'D. This is hard, and individual cases will require time to be analyzed.

  We can spot that in order to have an **isomorphism** then we necessarily have $|N| = |M|$, thus, $N = M$.
  
</p>

  ## Some basic theorems collapsed

<p>
  
  #### 1

  If $g \in G$ has order $o$, then $x^{m} = 1$ iff $o | m$. This is a direct consequence of [https://github.com/Z323323/Group-theory-elements?tab=readme-ov-file#proof-of-cyclicness-of-subgroups-and-uniqueness-of-each-element].

  #### 2

  If $x \in G$ has order $mn$, where $m, n$ are coprime, then $x$ can be uniquely expressed in the form $x = uv$ where $u$ has order $m$ and $v$ has order $n$. Picking $u = x^{bn}$ and $v = x^{am}$ such that $bn + am = 1$ solves the theorem, because $m, n$ are coprimes and then by Bezout's Identity it will always exist $a, b$ integers which solve the equality.
  
   #### 3

   A non-empty subset $H$ of $G$ is a subgroup of $G$ iff $H$ is closed under multiplication (1). This is a direct consequence of the definition of subgroups I wrote at [https://github.com/Z323323/Group-theory-elements/blob/main/README.md].

   #### 4 

   A non-empty subset $H \subset G$ is a subgroup iff $H^{2} \subset H$. To get this imagine $H$ not being a subgroup of $G$. We have that $e^{2} \not\in H$ for some element $e \in H$ and therefore $H$ not being a subgroup of $G$.

   #### 5

   For a subgroup $H$, for all $h \in H$ it must be that $hH = H = Hh$. Following [https://github.com/Z323323/Group-theory-elements?tab=readme-ov-file#multiplicative-groups-cyclic-subgroups-and-generators] $h$ must be some power of $e$ where $e$ is a generator for the subgroup; the lemma follows.

   #### 6

   For any set $S \subset H$, $SH = H = HS$. This is exactly the same logic of the previous one.

   #### 7

   A non-empty subset $H \subset G$ is a subgroup iff $H^{2} = H$. Follows from (4). You could also imagine $\langle h \rangle = H$, then shifting every element right by $1$ position clearly produces $H$.

   #### 8

   Let $g \in G$ and $H \leq G$, then $g^{- 1}Hg$ is a subgroup of $G$ isomorphic to $H$. To figure this out quickly, remember that $G$ and $H$ are defined over the same modulo, this means that we are basically removing elements from $H$ and then reinsert them probably altering the order. Calling $R$ the resulting set, we will have $|R| = |H|$ and $R = H$.
    
</p>
  


