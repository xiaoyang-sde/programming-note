# Context-Free Language

The language $L$ is context-free if it is generated by a context free grammar or accpeted by a pushdown automata.
Each regular langauge is a context-free language, because each regular langauge could be obtained from $\epsilon, \empty, \sigma$ with $\cup, \cdot, {*}$ and context-free language is closed under $\cup, \cdot, {*}$.

## Pumping Lemma for Context-Free Language

Let $L$ be context-free. There exists a $P \in N$ such that for all $s \in L$ of length $|s| \geq P$ could be decomposed as $s = uvxyz$ where $|vxy| \leq P$, $|v| + |y| \neq 0$, and $uv^i xy^i z \in L$ for all $i = 0, 1, \dots$.

Let $(V, \Sigma, R, S)$ be a context-free grammar for $L$. Let $b$ be the maximum length of all rules in $R$, which is the maximum branching factor of the grammar tree. Let $P = b^{|V| + 1}$ and $s$ be a string in $L$ such that $|s| \geq P$. Let $n$ be the number of leaves in the smallest (fewest nodes) grammar tree of $s$ and $h$ be the height of the smallest grammar tree of $s$, then $b \leq |s| \leq n \leq b^{h}$ and $n \geq |V| + 1$. Therefore, there's a pair of variables in the grammar tree that occurs at least twice.

## Contrapositive Form of Pumping Lemma

Let $L$ be non-context-free. **For all** $P \in N$ such that **there exists** an $s \in L$ of length $|s| \geq P$, **for all** $s = uvxyz$ where $|vxy| \leq P$, $|v| + |y| \neq 0$, **there exists** an $i$ such that $uv^i xy^i z \notin L$.

## Example

- Let $L = \{ a^n b^n a^n: n \geq 0 \}$. For all $P$, there exists an $s = a^P b^P a^P$. For all $s = uvxyz$, $uxz \notin L$. Therefore, $L$ is non-context-free.
- Let $L = \{ w \in \{ a, b, c \}^*: w \text{ contains equal number of } a, b, c \}$. For all $P$, there exists an $s = a^P b^P c^P$. For all $s = uvxyz$, $uxz \notin L$.

## Closure

### Union

Let $L', L''$ be context-free languages, then $L' \cup L''$ is a context-free language. Let $L'$ be $(V', \Sigma, R', S')$ and $L''$ be $(V'', \Sigma, R'', S'')$. The context-free grammar for $L' \cup L''$ is $(V' \cup V'' \cup \{ \epsilon \}, \Sigma, R' \cup R'' \cup \{ S \rightarrow S' | S'' \}, S)$.

### Concatenation

Let $L', L''$ be context-free languages, then $L' L''$ is a context-free language. Let $L'$ be $(V', \Sigma, R', S')$ and $L''$ be $(V'', \Sigma, R'', S'')$. The context-free grammar for $L' L''$ is $(V' \cup V'' \cup \{ \epsilon \}, \Sigma, R' \cup R'' \cup \{ S \rightarrow S' S'' \}, S)$.

### Kleene Star

Let $L$ be a context-free langauge, then $L^*$ is a context-free language. Let $L$ be $(V, \Sigma, R, S)$. The context-free grammar for $L^*$ $(V \cup \{ S_{\text{new}} \}, \Sigma, R \cup {S_{\text{new}} \rightarrow SS_{\text{new}} | \epsilon, S_{\text{new}} })$.

### Prefix

Let $L$ be a context-free language, then $\text{prefix}(L)$ is a context-free language. Let $P$ be a pushdown automata for $L$ and $P'$ be a transformed pushdown automata for $L$ in which $\sigma, \gamma \rightarrow \gamma'$ is changed to $\epsilon, \gamma \rightarrow \gamma'$, and the cloned state in $q$ is directed to $q'$ with $\epsilon, \epsilon \rightarrow \epsilon$. Therefore, if the string $w$ ends in $P$, it moves to $P'$ and tries to reach an accepted state.

### Suffix

Let $L$ be a context-free language, then $\text{suffix}(L)$ is a context-free language. Let $P$ be a pushdown automata for $L$ and $P'$ be a transformed pushdown automata for $L$ in which $\sigma, \gamma \rightarrow \gamma'$ is changed to $\epsilon, \gamma \rightarrow \gamma'$, and the cloned state in $q'$ is directed to $q$ with $\epsilon, \epsilon \rightarrow \epsilon$. Therefore, if the string $w$ ends in $P$, it moves to $P'$ and tries to reach an accepted state.

### Reverse

Let $L$ be a context-free language, then $L^R$ is a context-free language. Let $G$ be a context-free grammar of $L$, then a clone of $G$ with all rules reversed (from $X \rightarrow Y_1 Y_2 \dots Y_m$ to $X \rightarrow Y_m \dots Y_2 Y_1$) is a context-free grammar of $L^R$.

## Non-Closure

### Intersection

Let $L', L''$ be context-free languages, then $L' \cap L''$ might not be a context-free language. Let $L' = {a^n b^n c^m: n, m \geq 0}$ and $L'' = {a^n b^m c^m: n, m \geq 0}$, then $L' \cap L'' = {a^n b^n c^n: n \geq 0}$ is not context-free.

If $L'$ is regular, then $L' \cap L''$ is a context-free language. Let the NFA for $L'$ be $(Q', \Sigma, \delta', q_0', F')$ and the PDA for $L''$ be $(Q'', \Sigma, \Gamma, \delta'', q_0'', F'')$. The PDA for $L' \cap L''$ is defined as $(Q' \times Q'', \Sigma, \Gamma, \delta, (q_0' , q_0''), F' \times F'')$, $\delta((q', q''), \sigma, \gamma) = \delta'(q', \sigma) \times \delta''(q'', \sigma, \gamma)$.

### Complement

Let $L$ be a context-free language, then $\bar{L}$ might not be a context-free language. If the context-free language is both closed under complement and union, then it should be closed under intersection, which is proved to be false.

### Set Difference

Let $L', L''$ be context-free langauges, then $L' - L''$ might not be a context-free language. If the context-free language is both closed under set difference, then $\Sigma^* - L$ (complement) should be context-free, which is proved to be false.