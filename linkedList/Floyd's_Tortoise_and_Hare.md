# Floyd's Tortoise and Hare

## Phase 1
We initialize two pointers - the fast hare and the slow tortoise. Then, until hare can no longer advance, we increment tortoise once and hare twice. If, after advancing them, hare and tortoise point to the same node, we return it. Otherwise, we continue. If the while loop terminates without returning a node, then the list is acyclic, and we return null to indicate as much.

https://gyazo.com/65fedb729ccaa076c150878f6794e8af

Here, the nodes in the cycle have been labelled from 0 to $C-1$, where $C$ is the length of the cycle. The noncyclic nodes have been labelled from $-F$ to $-1$, where $F$ is the number of nodes outside of the cycle. After $F$ iterations, tortoise points to node 0 and hare points to some node $h$, where $F \equiv h \pmod CF≡h(modC)$. This is because hare traverses $2F$ nodes over the course of $F$ iterations, exactly $F$ of which are in the cycle. After $C-h$ more iterations, tortoise obviously points to node $C-h$, but (less obviously) hare also points to the same node. To see why, remember that hare traverses $2(C-h)$ from its starting position of $h$:
$$
\begin{aligned} h + 2(C-h) &= 2C - h \\ &\equiv C-h \pmod C \end{aligned}
$$

Therefore, given that the list is cyclic, hare and tortoise will eventually both point to the same node, known henceforce as the intersection.

## Phase 2

Given that phase 1 finds an intersection, phase 2 proceeds to find the node that is the entrance to the cycle. To do so, we initialize two more pointers: ptr1, which points to the head of the list, and ptr2, which points to the intersection. Then, we advance each of them by 1 until they meet; the node where they meet is the entrance to the cycle, so we return it.

Use the diagram below to help understand the proof of this approach's correctness.

https://leetcode.com/problems/linked-list-cycle-ii/Figures/142/diagram.png

We can harness the fact that hare moves twice as quickly as tortoise to assert that when hare and tortoise meet at node hh, hare has traversed twice as many nodes. Using this fact, we deduce the following:
$
\begin{aligned} 2 \cdot distance(tortoise) &= distance(hare) \\ 2(F+a) &= F+a+b+a \\ 2F+2a &= F+2a+b \\ F &= b \\ \end{aligned}
$

Because $F=b$, pointers starting at nodes $h$ and $0$ will traverse the same number of nodes before meeting.