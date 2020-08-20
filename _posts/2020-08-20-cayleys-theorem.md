---
layout: post
title: Cayley's Theorem
show-avatar: false
tags:
  - maths
  - physics
  - group theory
published: true
---
Cayley's Theorem is a fascinating link between the symmetric groups and all other groups. The theorem states that: any group G can be embedded into a subgroup of the permutation group of G. In other words there is some isomorphism from G onto a subgroup of Perm(G), this perhaps doesnt seem like the most groundbreaking assertion but it means that any proof for subgroups of a permutation group works generally.

To prove the theorem a group G is chosen along with a permutation group of that group (a group that has all the possible permutation actions on G, not all possible permutations of G), then showing that G maps onto a subset of Perm(G).

### Proof

$$Perm(G)$$ is the group of permutations on G. As Perm(G) has the order $$|G|!$$ the order of $$Perm(G)$$ is always greater than or equal to that of $$G$$. Cayley's theorem is easy to demonstrate for small groups like $$Z_3 = (\{0,1\}, + \text{mod } 2)$$. Since  $$Perm(Z_2)$$ contains an identity and a transposition action. This is clearly isomorphic to the original set with 1 being the identity and 2 the transposition.

The proof for the theorem involves taking an homomorphism from $$G$$ to a subset of $$Perm(G)$$ and showing that the map is isomorphic and its image is a group.

Consider a group $$G = (\{g_i\}, \star)$$ and an homomorphic map $$h: G \rightarrow Perm(G); \space h(g_1 \star g_2) = h(g_1) \diamond h(g_2)$$ where $$\diamond$$ is the composition law of Perm(G).

h must be isomorphic if h is a bijective map from $$G4 to a subset of $$Perm(G)$$ there are no constraints when selecting our subset of $$Perm(G)$$ so the map can be trivially surjective.

h is injective iff the kernel of $$G4 is the singleton $$e_G$$. Suppose $$h(g_i) \diamond h(g_1) = h(g_i); \space \forall  g_i$$, if this is the case then as $$h(g_i) \diamond h(g_1) = h(g_i \star g_1)$$ we can see that $$g_i \star g_1 = g_i$$. Now suppose we pick the identity of G: $$e \neq g_1 \Longrightarrow g_1 = g_1 \star e = e$$. This means the kernel is a singleton and so $$h$$ is injective.

The image of $$h$$ in $$Perm(G)$$ is a group if it follows group laws. Since we already know the identity exists and that it is associative as it inherits the group composition of Perm(G), only the exitence of inverses and closure neeed to be shown.

$$
h(g_1) \diamond h(g_2)(x) = h(g_1)(g_2 \star x) = g_1 \star g_2 \star x = h(g_1 \star g_2)(x); \space \forall x \in G
$$

This shows that the image of h is a group. The structure is conserved, including the group properties of G.
