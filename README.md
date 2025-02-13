# Formal group theory 1

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
  $((x \mod n) \mod m)((y \mod n) \mod m) \mod m = (z \mod n) \mod m$

  Now, before you start crying, note that we will face the same modulo operation operating with _finite groups_ in general (therefore subgroups relations), that is, something of this form

  $G = (\\{x, y, \dots, \phi(n) \\}, \cdot \mod n)$<br>
  $S = (\\{a, b, \dots, \phi(n)/p \\}, \cdot \mod n)$<br>
  $->$<br>
  $(a \mod n)(b \mod n) \mod n = c \mod n$

  We can spot that in order to have an **isomorphism** then we necessarily have $|G| = |S|$ which reduces the problem complexity by far because it means that we are operating under the same modulo **and** the same number of elements in the sets, thus, $G = S$.

  Note that unless specified, every operation from now on will be over the same modulo operation and we will refer to _finite multiplicative groups_.
  
</p>

  ## Some basic theorems collapsed

<p>
  
  #### $(1)$

  If $g \in G$ has order $o$, then $x^{m} = 1$ iff $o | m$. This is a direct consequence of [https://github.com/Z323323/Group-theory-elements?tab=readme-ov-file#proof-of-cyclicness-of-subgroups-and-uniqueness-of-each-element].

  #### $(2)$

  If $x \in G$ has order $mn$, where $m, n$ are coprime, then $x$ can be uniquely expressed in the form $x = uv$ where $u$ has order $m$ and $v$ has order $n$. Let $u = x^{bn}$ and $v = x^{am}$ such that $bn + am = 1$, by Bezout's Identity that equation always has a solution. This means that for example, if the solution of the identity is $bn - am = 1$ then

  $\displaystyle x = \frac{x^{bn}}{x^{am}}$
  
  This theorem could look very strange at first, you should note that we are making an abstraction considering $x$, because $x = g^{k}$ for some $k$ and
  
  $bn - am = 1$<br>
  $->$<br>
  $\displaystyle g^{k} = \frac{g^{kbn}}{g^{kam}} = g^{k(bn - am)} = g^{k(1)} = g^{k} = x$

  We can easily replace $bn - am = 1$ using the general form $bn + am = 1$ being aware we will either end up having $bn - am = 1$ or $am - bn = 1$ which produces the same outcome.
  
   #### $(3)$

   A non-empty subset $H$ of $G$ is a subgroup of $G$ iff $H$ is closed under multiplication (1). This is a direct consequence of the definition of subgroups I wrote at [https://github.com/Z323323/Group-theory-elements/blob/main/README.md].

   #### $(4)$

   A non-empty subset $H \subset G$ is a subgroup iff $H^{2} \subset H$. To get this imagine $H$ not being a subgroup of $G$. We have that $e^{2} \not\in H$ for some element $e \in H$ and therefore $H$ not being a subgroup of $G$.

   #### $(5)$

   For a subgroup $H$, for all $h \in H$ it must be that $hH = H = Hh$. Following [https://github.com/Z323323/Group-theory-elements?tab=readme-ov-file#multiplicative-groups-cyclic-subgroups-and-generators] $h$ must be some power of $e$ where $e$ is a generator for the subgroup; the lemma follows.

   #### $(6)$

   For any set $S \subset H$, $SH = H = HS$. This is exactly the same logic of the previous one.

   #### $(7)$

   A non-empty subset $H \subset G$ is a subgroup iff $H^{2} = H$. Follows from (4). You could also imagine $\langle h \rangle = H$, then shifting every element right by $1$ position clearly produces $H$.

   #### $(8)$

   Let $g \in G$ and $H \leq G$, then $g^{- 1}Hg$ is a subgroup of $G$ isomorphic to $H$. To figure this out quickly, remember that $G$ and $H$ are defined over the same modulo, this means that we are basically removing elements from $H$ and then reinsert them probably altering the order. Calling $R$ the resulting set, we will have $|R| = |H|$ and $R = H$.

   ### Setting up a convenient formalization on subgroups

   Analyzing $(2)$ I noticed we can make a convenient formalization. 

   Let $S$ be a subgroup of $G$, we can refer to every element of $S$ letting $g \in G$ generator for $G$ and writing 

   $g^{kx}$

   where $x \geq 1$ and $k$ is a constant such that the order $o$ of $S$ is $\phi(n) / k$ for some $k | \phi(n)$ ($S$ is the subgroup defined by the roots of unity of $o$).

   #### Example 1

   Let $S$ be a subgroup of $G$ of order $o = \phi(n) / 2$, and $g$ a generator for $G$, then we can represent every element of $S$ using the general form

   $g^{2x}$

   #### Example 2

   Let $G$ of order $\phi(n)$ where $\phi(n) = 2 \cdot 3 \cdot 13$; let $g$ a generator for $G$ and $S$ a subgroup of order $o = 13$, then we have
   
   $\displaystyle o_S = \frac{\phi(n)}{2 \cdot 3}$ 
   
   and we can define the general form for every element of $S$ as

   $g^{6x}$

</p>

## Lagrange's theorem

<p>

  [https://crypto.stanford.edu/pbc/notes/group/lagrange.html].

  #### Lemma

  Let $H$ be a subgroup of $G$ and $r, s \in G$, then $Hr = Hs$ iff $rs^{- 1} \in H$, otherwise $Hr$ and $Hs$ have no element in common.

  #### Proof

  Let $r = g^{k_1x}, s = g^{k_2x}$, and the general form for any element of $S$ as $g^{kx}$. In order to have $Hr = Hs$ it must be that
  
  $(k_1 + k)x = (k_2 + k)x$<br>
  $->$<br>
  $k_1 = k_2$

  Under this result we can easily see that $rs^{- 1}$ translates to

  $\displaystyle \frac{g^{k_1x}}{g^{k_2x}} = g^{(k_1 - k_2)x}$<br>

  and under $Hr = Hs$ we have $k_1 = k_2$ and

  $g^{(k_1 - k_2)x} = 1 \in H$

  which is always true since $1$ belongs to every subgroup.

  #### Theorem

  If $H$ is a subgroup of $G$ then $|G| = n|H|$ for some positive integer $n$ which is called _index_ of $H$ in $G$. Furthermore, there exist $r_1, \dots, r_n$ such that $G = Hr_1 \cup \dots \cup Hr_n$, and an equivalent construction holds for $H$ if the _index_ $i$ of $H$ is a composite number.

  (Here I guess Ben mistyped $g_1 \dots$)

  #### Proof

  The first statement derives directly from the general form for subgroups elements I wrote previously. The _index_ indicates the number of cofactors of $o_G$.

  The second statement holds because, recalling the general form for the elements of $H$ subgroup of $G$ being $g^{kx}$ and $(2)$, we can use two elements which belong to two different subgroups having coprimes orders to build every element of $G$ such that the two orders multiplied equal the order of $G$. Under this last assumption $(o_G = o_Ho_S)$ lies the proof for this theorem, because setting a new hypothesis where $o_G = o_Ho_So_Ro_Fo_L \dots$ where all orders are pairwise coprime produces 
  
  $G = g^{k_Hx}g^{k_Sx}g^{k_Rx} \dots$
  
  which produces the general form for the elements of $G$

  $g^{\phi(n)x} = g^{x}$

  which is an equivalent result compared to $G = Hr_1 \cup \dots \cup Hr_n$, even though I guess there exist some $r_q \in H$. The statement is not the clearest.

  #### Corollary 1

  Let $|G|$ be the order of $G$, and $g \in G$, then $g \in H$ and $|H| | |G|$. This is a direct consequence of the Euler's theorem and the general forms structure.

  #### Corollary 2

  Let $G$ a group of prime order, then $G$ has no subgroups while being cyclic by Euler's theorem (and corollary but the more I study these topics the more I realize Euler's theorem is enough to state cyclicality).
  
</p>

  ## Cyclic groups

  <p>

  It is worth to spend a couple words on _additive finite groups_ now. To define them we can just take the definition of multiplicative subgroups and change the identity element to $0$. It derives that the inverse of a number in an additive group is its negative. Also, it is quite easy to figure out that for any prime $n$, the order of any subgroup of $Z_{n}^{+}$ will be $n$, because, for example, imagine $Z_{17}^{+}$, it's quite simple to figure out that we will encounter $0$ every time we add any generator $17$ times and not before since no elements shares the $17$ cofactor before being multiplied by it. Let's now talk about uniqueness of elements and cases having $n$ which is not prime.

  #### Example

  Defining $Z_{6}^{+}$ and using $1, 2, 3, 4, 5$ as test-generators we get

  $\\{1, 2, 3, 4, 5, 0, \dots \\}$<br>
  $\\{2, 4, 0, 2, 4, 0, \dots \\}$<br>
  $\\{3, 0, 3, 0, 3, 0, \dots \\}$<br>
  $\\{4, 2, 0, 4, 2, 0, \dots \\}$<br>
  $\\{5, 4, 3, 2, 1, 0, \dots \\}$

  and we can derive a couple of simple properties. We have $1, 5$ being generators for the set and it's quite intuitive to derive that any generator will need to be coprime with the modulo. Now let's talk about uniqueness and orders. Elements which share the same cofactor(s) with the modulo will have the same order, and every element before $0$ will be different ensuring uniqueness of elements because, let $n = abc$, moving the problem to multiplicative groups we get

  - $a \cdot bc \equiv 0 \mod abc$
  - $ab \cdot c \equiv 0 \mod abc$
  - $d \cdot abc \equiv 0 \mod abc$
  - $aa \cdot bc \equiv 0 \mod abc$
  - $ad \cdot bc \equiv 0 \mod abc$
  - $abd \cdot c \equiv 0 \mod abc$
  - $de \cdot abc \equiv 0 \mod abc$

  where numbers of the left side of $\cdot$ represent some test-generators for $Z_{abc}^{+}$, and numbers on the right represent their subgroup order (which prove everything said but uniqueness). Now keeping the problem on multiplicative groups we know that we can represent any number which is coprime with $n = abc$ as the product of some $g^{x}$, g^{y}$ where $g$ is a generator for $Z_{abc}^{*}$,

  


  </p>


