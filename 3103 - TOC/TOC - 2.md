---
course: "CSE 3103: Theory of Computation (TOC)"
class: "TOC - 2"
duration: "1:16:21"
---
# TOC - 2: Mathematical Preliminaries, Formal Languages, and Deterministic Finite Automata (DFA)

## Overview
This lecture formally begins the core syllabus of Theory of Computation following the introductory overview in the first class. It introduces the three main areas of the course, reviews the discrete mathematics foundations (sets, sequences, tuples, graphs, alphabets, strings, languages, and closure operations), and dives into Deterministic Finite Automata (DFA) with formal definitions, representation methods, dead/reject states, and five worked examples.

## Topic Map
- Course Structure & Motivation
  - Three central areas: Finite Automata Theory, Computability Theory, Complexity Theory
  - Practical motivation: Compiler design and modeling computation on paper
- Mathematical Preliminaries & Formal Language Foundations
  - Sets, sequences, tuples, power sets, Cartesian products, and directed graphs
  - Alphabets ($\Sigma$), strings ($w$), and languages ($L$)
  - Closure operations: $\Sigma^0$, $\Sigma^n$, Kleene star ($\Sigma^*$), and positive closure ($\Sigma^+$)
  - Language representations and operations (union, concatenation, power, Kleene star)
- Finite Automata Roadmap
  - FA with output (Mealy, Moore: outside syllabus) vs. without output (DFA, NFA, $\epsilon$-NFA)
  - Planned flow: DFA, NFA, $\epsilon$-NFA, conversions to DFA, DFA minimization
- Deterministic Finite Automata (DFA)
  - Formal 5-tuple definition: $(Q, \Sigma, \delta, q_0, F)$
  - Meaning of determinism and avoiding ambiguity
  - Transition representations: diagram, table, and extended transition function ($\delta^*$)
  - Dead (reject/trap) states
  - Worked examples:
    - Odd number of 0s and odd number of 1s (plus parity variants)
    - Strings starting with `0`
    - Strings of exact length 2
    - Strings starting with `01`
    - Strings ending with `01` (in-class exercise and board walkthrough)

## Detailed Notes

### 1. Course Structure & Motivation
- **Theory of Computation (ToC)** provides a theoretical representation of the computers we use and the computations we perform.
- **Three Central Areas**:
  1. **Finite Automata Theory** (Automata Theory): Covers Finite Automata (FA), Pushdown Automata (PDA), Linear Bounded Automata (LBA, a variant of Turing Machine), and Turing Machines (TM).
  2. **Computability Theory**: Studies what problems can be solved by these models.
  3. **Complexity Theory**: Studies efficiency and resource bounds (covered in part later in the course; the main focus is Automata Theory and Computability Theory).
- **Intuition & Compiler Design Motivation**:
  - Consider a compiler for a programming language: given any source program, the compiler either **accepts** it (no syntax errors, reaches a final state) or **rejects** it (syntax error, fails to reach a final state).
  - Although there are only two outcomes (accept/reject), humans can write valid or invalid programs in infinitely many ways.
  - Before building an actual compiler, ToC models are used on paper to prove whether a machine can recognize all valid programs of a language and reject all invalid ones.
  - Even a simple on/off switch is a basic computing machine with two states.

### 2. Mathematical Preliminaries & Formal Language Foundations
- **Sets vs. Sequences**:
  - **Set**: Unordered collection; duplicates do not matter. For example, $\{1, 2, 3\} = \{3, 2, 1\} = \{1, 1, 2, 3\}$.
  - **Sequence**: Ordered list of objects; both order and repetition matter.
- **Tuples & Cartesian Product**:
  - Cartesian product of sets $A$ and $B$: $A \times B = \{(x, y) \mid x \in A, y \in B\}$.
  - Elements of a Cartesian product are **tuples** (enclosed in parentheses, e.g., pairs, 3-tuples, $k$-tuples).
- **Power Set**:
  - If a set has cardinality $n$ (e.g., $n = 3$), its power set has cardinality $2^n$ (e.g., $2^3 = 8$), containing all subsets from size $0$ up to $n$.
- **Graphs**:
  - Consist of **vertices** (nodes, drawn as circles) and **edges/arcs** (paths between nodes).
  - Edges can be directed or undirected, and weighted or unweighted. In ToC, we primarily use **directed graphs** with labeled/weighted transitions.
- **Alphabets, Strings, and Languages**:
  - **Alphabet ($\Sigma$)**: A **finite** set of symbols/characters (analogous to Bangla or English letters/vowels/consonants).
    - Examples: $\Sigma = \{0, 1\}$, $\Sigma = \{a, b, \dots, z\}$, $\Sigma = \{0\text{-}9, a\text{-}f\}$ (sequential ranges can be shortened with a hyphen or `...`), or sets including special symbols.
  - **String ($w$)**: A **finite** sequence of symbols from an alphabet concatenated together (analogous to a word). A string must be finite; an infinitely long word cannot convey bounded meaning.
  - **Language ($L$)**: A set of strings over an alphabet. Unlike alphabets and strings, a language can be **finite** or **infinite**:
    - Infinite example: All binary numbers starting with `0`.
    - Finite example: All binary numbers of exact length $2$ ($4$ strings) or exact length $3$ ($8$ strings).
- **Powers of an Alphabet & Closure Operations**:
  - $\Sigma^0 = \{\epsilon\}$, where $\epsilon$ denotes the empty string ("nothing" / empty symbol).
  - $\Sigma^1 = \Sigma$ (all strings of length $1$).
  - $\Sigma^2 = \Sigma \times \Sigma$ (all strings of length $2$; for $\Sigma = \{0, 1\}$, $\Sigma^2 = \{00, 01, 10, 11\}$).
  - $\Sigma^3$ gives all strings of length $3$ ($000, 001, \dots, 111$).
  - **Kleene Closure / Kleene Star ($\Sigma^*$)**: Union of all powers from length $0$ to $\infty$:
    $$\Sigma^* = \Sigma^0 \cup \Sigma^1 \cup \Sigma^2 \cup \Sigma^3 \cup \dots = \bigcup_{i=0}^{\infty} \Sigma^i$$
  - **Positive Closure ($\Sigma^+$)**: Union of all powers from length $1$ to $\infty$ (excludes $\epsilon$):
    $$\Sigma^+ = \Sigma^1 \cup \Sigma^2 \cup \Sigma^3 \cup \dots = \bigcup_{i=1}^{\infty} \Sigma^i$$
  - **Relationship**:
    $$\Sigma^* = \{\epsilon\} \cup \Sigma^+, \qquad \Sigma^+ = \Sigma^* - \{\epsilon\}$$
- **Worked Examples on Alphabet Powers**:
  1. For $\Sigma = \{0, 1\}$: $\Sigma^+ - (\Sigma^4 \cup \Sigma^5 \cup \dots) = \Sigma^1 \cup \Sigma^2 \cup \Sigma^3$ (strings of length 1, 2, and 3).
  2. For $\Sigma = \{a, b\}$: $\Sigma^* - (\Sigma^1 \cup \Sigma^2 \cup \Sigma^4 \cup \Sigma^5 \cup \dots) = \Sigma^0 \cup \Sigma^3 = \{\epsilon\} \cup \Sigma^3$.
  3. For $\Sigma = \{a, b, c\}$: $\Sigma^* - (\Sigma^0 \cup \Sigma^1 \cup \Sigma^3 \cup \Sigma^4 \cup \dots) = \Sigma^2$.
  4. For $\Sigma = \{a, b, c\}$: $\Sigma^* - (\Sigma^1 \cup \Sigma^2 \cup \dots) = \Sigma^0 = \{\epsilon\}$.
  5. For $\Sigma = \{a, b, c\}$: $|\Sigma^4| = |\Sigma|^4 = 3^4 = 81$.
- **Representing Languages & Language Operations**:
  - Languages can be described in English or via set-builder notation:
    - $L = \{w \mid w \text{ has an equal number of } 0\text{s and } 1\text{s}\}$
    - $L = \{w \mid w \text{ is a binary integer that is prime}\}$
    - $L = \{w \mid w \text{ is a syntactically correct C program}\}$ (the machine recognizing this is a C compiler)
    - Shorthand forms: $\{0^n 1^n \mid n \ge 0\}$ (equal count of $0$s followed by $1$s) and $\{0^i 1^j \mid i \le j\}$ (count of $0$s is at most the count of $1$s).
  - **Operations on Languages**: Follow standard set and string rules:
    - Union: $L_1 \cup L_2$
    - Concatenation: $L_1 L_2$ (pairs each string from $L_1$ with each string from $L_2$)
    - Power: $L^2 = L \cdot L$, $L^3 = L \cdot L \cdot L$
    - Kleene star ($L^*$) and positive closure ($L^+$)

### 3. Finite Automata Roadmap
- **Two Categories of Finite Automata**:
  1. **With output**: Mealy machine, Moore machine (not in the course syllabus).
  2. **Without output**: DFA, NFA, $\epsilon$-NFA (covered in the syllabus).
- **Topic Sequence**:
  1. Characteristics and fundamentals of FA
  2. Deterministic Finite Automata (DFA)
  3. Nondeterministic Finite Automata (NFA)
  4. $\epsilon$-NFA (NFA with $\epsilon$-transitions)
  5. Conversions: $\text{NFA} \to \text{DFA}$ and $\epsilon\text{-NFA} \to \text{NFA} \to \text{DFA}$ (note: $\epsilon$-NFA cannot go directly to DFA without going through NFA; NFA and $\epsilon$-NFA are easier to design on paper, but only DFAs can be directly implemented on a computer).
  6. DFA Minimization (removing redundant or unreachable states produced after conversion).

### 4. Deterministic Finite Automata (DFA)
- **Formal 5-Tuple Definition**: A DFA is defined as $(Q, \Sigma, \delta, q_0, F)$:
  1. $Q$: Finite set of states.
  2. $\Sigma$: Finite set of input symbols (alphabet).
  3. $\delta$: Transition function, $\delta: Q \times \Sigma \to Q$.
  4. $q_0$: Start state ($q_0 \in Q$). There is always **exactly one** start state.
  5. $F$: Set of final / accepting states ($F \subseteq Q$). There can be **multiple** final states. Non-final states act as rejecting states.
- **What "Deterministic" Means**:
  - From **every** state in $Q$, for **every** input symbol in $\Sigma$, there must be **exactly one** outgoing transition.
  - No missing transitions (every symbol must be handled at every state).
  - No ambiguous branching (one input symbol from one state cannot lead to two different states, because a real machine could not decide which path to follow).
  - However, multiple *different* symbols (e.g., both `0` and `1`) from the same state *can* lead to the same target state (often written on one arrow as `0, 1` or `0 + 1`).
- **Three Ways to Represent Transitions**:
  1. **State Transition Diagram**: Directed graph where states are circles, the start state has a dangling incoming arrow, and final states have double circles.
  2. **State Transition Table**: Rows list states (start state marked with $\to$, final states marked with $*$), columns list symbols in $\Sigma$, and cells give the next state.
  3. **Transition Function Notation**: Writing $\delta(q, a) = q'$ directly, and using the **extended transition function** $\delta^*$ to process full strings one symbol at a time:
     $$\delta^*(q, aw) = \delta^*(\delta(q, a), w)$$
     A string $w$ is accepted if $\delta^*(q_0, w) \in F$ once the entire string is consumed (no symbols left).
- **Dead (Reject / Trap) States**:
  - When a prefix already violates the language rule (so no continuation can ever make the string valid), the DFA routes that transition into a non-final state with self-loops on all symbols in $\Sigma$. This ensures the DFA handles all possible erroneous inputs deterministically.

#### Worked Example 1: Odd Number of 0s and Odd Number of 1s
- **Language**: $L = \{w \in \{0, 1\}^* \mid w \text{ contains an odd number of } 0\text{s and an odd number of } 1\text{s}\}$.
- **Smallest accepted strings**: `01` and `10` ($\epsilon$ has $0$ zeros and $0$ ones, which are both even).
- **States (by parity of 0s and 1s)**:
  - $q_0$ (Start): Even 0, Even 1
  - $q_1$: Odd 0, Even 1
  - $q_2$ (Final, double circle): Odd 0, Odd 1
  - $q_3$: Even 0, Odd 1
- **Transitions**:
  - From $q_0$: on `0` $\to q_1$; on `1` $\to q_3$
  - From $q_1$: on `0` $\to q_0$; on `1` $\to q_2$
  - From $q_2$: on `0` $\to q_3$; on `1` $\to q_1$
  - From $q_3$: on `0` $\to q_2$; on `1` $\to q_0$
- **Transition Table**:

| State | `0` | `1` |
| :--- | :---: | :---: |
| $\to q_0$ | $q_1$ | $q_3$ |
| $q_1$ | $q_0$ | $q_2$ |
| $* q_2$ | $q_3$ | $q_1$ |
| $q_3$ | $q_2$ | $q_0$ |

- **Tracing Examples**:
  - `01`: $q_0 \xrightarrow{0} q_1 \xrightarrow{1} q_2 \in F$ (Accepted).
  - `10`: $q_0 \xrightarrow{1} q_3 \xrightarrow{0} q_2 \in F$ (Accepted).
  - `000001` (5 zeros, 1 one): $q_0 \xrightarrow{0} q_1 \xrightarrow{0} q_0 \xrightarrow{0} q_1 \xrightarrow{0} q_0 \xrightarrow{0} q_1 \xrightarrow{1} q_2 \in F$ (Accepted).
  - `0111`: $\delta^*(q_0, 0111) = \delta^*(q_1, 111) = \delta^*(q_2, 11) = \delta^*(q_1, 1) = q_2 \in F$ (Accepted).
  - `010`: $q_0 \xrightarrow{0} q_1 \xrightarrow{1} q_2 \xrightarrow{0} q_3 \notin F$ (Rejected).
  - `10101` (2 zeros, 3 ones): ends at $q_3 \notin F$ (Rejected).
- **Parity Variants Using the Same Diagram**:
  - Odd 0, Even 1: make $q_1$ the final state.
  - Even 0, Odd 1: make $q_3$ the final state.
  - Even 0, Even 1: make $q_0$ the final state (note: here start state and final state are the same, so $\epsilon$ is accepted).
  - Union ("Odd 1 and Even 0" OR "Even 1 and Odd 0"): make both $q_1$ and $q_3$ final states.

#### Worked Example 2: Binary Strings Starting with `0`
- **Language**: $L = \{w \in \{0, 1\}^* \mid w \text{ starts with } 0\}$.
- **Smallest string**: `0`.
- **Design**:
  - $q_0$ (Start) $\xrightarrow{0} q_1$ (Final).
  - $q_1$ has a self-loop on `0, 1` (once it starts with `0`, any trailing symbols keep it valid).
  - $q_0 \xrightarrow{1} q_{\text{reject}}$ (dead state), and $q_{\text{reject}}$ has a self-loop on `0, 1` (once it starts with `1`, it can never become valid).

#### Worked Example 3: Binary Strings of Exact Length 2
- **Language**: $L = \{w \in \{0, 1\}^* \mid |w| = 2\} = \{00, 01, 10, 11\}$.
- **Design**:
  - $A$ (Start) $\xrightarrow{0, 1} B \xrightarrow{0, 1} C$ (Final) $\xrightarrow{0, 1} D$ (Dead/Reject).
  - $D$ has a self-loop on `0, 1`.
  - Strings of length 0 or 1 stop before $C$; strings of length 2 stop at $C$; strings of length $\ge 3$ fall into $D$.

#### Worked Example 4: Binary Strings Starting with `01`
- **Language**: $L = \{w \in \{0, 1\}^* \mid w \text{ starts with } 01\}$.
- **Smallest string**: `01`.
- **Design**:
  - $q_0$ (Start) $\xrightarrow{0} q_1 \xrightarrow{1} q_2$ (Final).
  - $q_2$ has a self-loop on `0, 1`.
  - $q_0 \xrightarrow{1} q_3$ (Dead) and $q_1 \xrightarrow{0} q_3$ (Dead), with a self-loop on `0, 1` at $q_3$.

#### Worked Example 5: Binary Strings Ending with `01` (In-Class Exercise)
- **Language**: $L = \{w \in \{0, 1\}^* \mid w \text{ ends with } 01\}$.
- **Smallest string**: `01`.
- **Design**:
  - $q_0$ (Start): represents having no useful suffix progress toward `01` (or starting fresh).
    - On `0` $\to q_1$
    - On `1` $\to q_0$ (self-loop; leading `1`s do not start `01` and do not prevent a later `01`)
  - $q_1$: represents having just seen a `0` as the potential start of `01`.
    - On `1` $\to q_2$ (Final)
    - On `0` $\to q_1$ (self-loop; the newest `0` still gives a trailing `0` ready for `1`)
  - $q_2$ (Final): represents having just seen `01`.
    - On `0` $\to q_1$ (the new `0` can be the start of a new `01` suffix)
    - On `1` $\to q_0$ (suffix becomes `...011`, breaking `01`, so we must wait for a `0` again)
- **Tracing Examples**:
  - `11110101`: stays in $q_0$ for all `1`s, $q_0 \xrightarrow{0} q_1 \xrightarrow{1} q_2 \xrightarrow{0} q_1 \xrightarrow{1} q_2 \in F$ (Accepted).
  - `01011`: $q_0 \xrightarrow{0} q_1 \xrightarrow{1} q_2 \xrightarrow{0} q_1 \xrightarrow{1} q_2 \xrightarrow{1} q_0 \notin F$ (Rejected).

## Exam / Important Points
- **DFA vs. NFA rules**: In a DFA, every state must have **exactly one** outgoing transition for **every** symbol in $\Sigma$. Forgetting transitions for an input symbol or drawing two outgoing arrows for the same symbol from one state makes it invalid as a DFA (that would be an NFA).
- **Single-to-multiple vs. multiple-to-single**: Multiple *different* input symbols from one state can go to the same destination state (valid), but a *single* input symbol from one state cannot go to multiple states.
- **Start state vs. Final states**: There is always **one** start state, whereas there can be **multiple** final states (used when modeling unions/OR conditions). Start and final states can also be the same state (e.g., when $\epsilon$ is in the language, such as "even 0s and even 1s").
- **Always include Reject/Dead States when required**: For prefix/length constraints (like "starts with 01" or "exact length 2"), you must include a dead state with self-loops for all symbols so invalid strings are deterministically rejected rather than left undefined.
- **$\Sigma^*$ vs. $\Sigma^+$**: Remember that $\Sigma^*$ includes $\epsilon$ (length 0), whereas $\Sigma^+$ starts at length 1 ($\Sigma^+ = \Sigma^* - \{\epsilon\}$).
- **Design strategy for DFAs**: First identify the smallest string(s) in the language and build the backbone path for them, then add remaining transitions for every input symbol at every state, checking whether each transition keeps progress, resets progress, or enters a dead state.
- **Notation in Transition Tables**: Mark the start state with an arrow ($\to$) and final state(s) with an asterisk ($*$).
- **Coming up next class**: Variants such as "begins or ends with `01`" and arithmetic/divisibility DFAs (e.g., binary numbers divisible by 3).

## Announcements & Logistics
- None mentioned. (Next class will continue with additional DFA examples such as "begins or ends with 01" and binary numbers divisible by 3.)

## Open Questions / Unclear Parts
- **~29:25**: During the set-difference example on $\Sigma = \{a, b, c\}$ that evaluates to $\{\epsilon\}$, the board expression being subtracted was only referred to verbally as "৪" (problem 4) and "zero থাকবে মানে epsilon থাকবে", so the exact subtracted terms on the board (either $\Sigma^+$ or $\Sigma^1 \cup \Sigma^2 \cup \dots$) are inferred from context.
- **~1:11:30 - 1:14:20**: While the teacher walked around the classroom checking students' solutions to the "ends with 01" exercise, parts of individual student feedback were quiet or off-mic, though all common mistakes and the full correct solution were subsequently explained on the board.
