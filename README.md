# Theory of Computer Science (TCS) — JFLAP Comprehensive Assignment
### Curated 30 Problems and Solutions

- **Student Name:** Vedang Mendhurwar
- **Roll No / ID:** 40
- **Course:** Theory of Computer Science (TCS) / Formal Languages & Automata
- **Tool Used:** JFLAP (Java Formal Languages and Automata Package)
- **Format:** JFLAP `.jff` (XML-based formal models)

---

## Overview

This repository contains a curated, comprehensive collection of 30 problems and solutions covering the core syllabus of **Theory of Computer Science (TCS)** and **Formal Languages & Automata Theory**. 

The problems have been selected, deduplicated, standardized, and validated across reference archives to ensure a balanced progression from regular languages to context-free languages, pushdown automata, transducers, and Turing computability:
1. **Deterministic Finite Automata (DFA):** Q01 – Q06
2. **Nondeterministic Finite Automata (NFA) & Subset Construction:** Q07 – Q10
3. **Regular Expressions & Regular Grammars:** Q11 – Q15
4. **Finite State Transducers (Mealy & Moore Machines):** Q16 – Q17
5. **Context-Free Grammars (CFG) & Parsing Models:** Q18 – Q26
6. **Pushdown Automata (PDA & NPDA):** Q27 – Q28
7. **Turing Machines (Standard & Multi-Tape):** Q29 – Q30

Every file in this directory is a clean, syntactically valid XML `.jff` model verified to load seamlessly in JFLAP without external dependencies.

---

## Problem Index and Solution Breakdown

| Q# | Problem Statement | Automaton / Model Type | Filename | Summary of Logic & State Behavior |
|:---:|:---|:---:|:---|:---|
| **01** | Accept all strings over $\Sigma = \{a, b\}$ that end in substring `"ab"` | **DFA** | `Q01_DFA_Ends_With_ab.jff` | **States: $\{q_0, q_1, q_2\}$**, Start: $q_0$, Final: $q_2$. $q_0$ represents no match / trailing `b`; on reading `a`, moves to $q_1$ (potential prefix `a`). From $q_1$, reading `b` reaches accept state $q_2$. Any subsequent `a` loops back to $q_1$; `b` resets to $q_0$. |
| **02** | Accept all strings over $\Sigma = \{a, b\}$ containing an even number of `a`'s | **DFA** | `Q02_DFA_Even_Number_Of_As.jff` | **States: $\{q_0, q_1\}$**, Start: $q_0$, Final: $q_0$. State $q_0$ tracks even parity of symbol `a`, while $q_1$ tracks odd parity. Reading `a` toggles between $q_0$ and $q_1$; reading `b` self-loops, preserving parity. Also serves as regular grammar conversion baseline. |
| **03** | Accept all strings over $\Sigma = \{a, b\}$ that start with symbol `"a"` | **DFA** | `Q03_DFA_Starts_With_a.jff` | **States: $\{q_0, q_1, q_2\}$**, Start: $q_0$, Final: $q_1$. From initial state $q_0$, input `a` transitions to accepting trap state $q_1$ which loops on all symbols. Input `b` transitions to dead/reject state $q_2$ which traps all subsequent symbols. |
| **04** | Accept all strings over $\Sigma = \{a, b\}$ containing substring `"aa"` | **DFA** | `Q04_DFA_Contains_Substring_aa.jff` | **States: $\{q_0, q_1, q_2\}$**, Start: $q_0$, Final: $q_2$. State $q_0$ searches for first `a`; $q_1$ records one `a` seen. Seeing a second consecutive `a` transitions to $q_2$ (absorbing accept state). If `b` is encountered at $q_1$, resets to $q_0$. |
| **05** | Pattern matching DFA for grep regex `(a\|b)*abb` | **DFA** | `Q05_DFA_Grep_Pattern_abb.jff` | **States: $\{q_0, q_1, q_2, q_3\}$**, Start: $q_0$, Final: $q_3$. Knuth-Morris-Pratt style deterministic string matcher tracking prefixes of target pattern `"abb"`. $q_0$ (empty), $q_1$ (`a`), $q_2$ (`ab`), $q_3$ (`abb`, accept). Transitions rewind to appropriate prefix on mismatch. |
| **06** | DFA minimization demonstration with redundant equivalent states | **DFA** | `Q06_DFA_Minimization_Equivalence.jff` | **States: $\{q_0, q_1, q_2\}$**, Start: $q_0$, Final: $\{q_1, q_2\}$. States $q_1$ and $q_2$ both accept and have identical transition behaviors on symbols `a` and `b`. JFLAP table-filling minimization combines $q_1$ and $q_2$ into a single equivalent state, reducing to 2 states. |
| **07** | NFA accepting strings over $\Sigma = \{a, b\}$ ending in `"ab"` | **NFA** | `Q07_NFA_Ends_With_ab.jff` | **States: $\{q_0, q_1, q_2\}$**, Start: $q_0$, Final: $q_2$. State $q_0$ nondeterministically loops on `a` and `b`, and guesses the arrival of the suffix `"ab"` by branching on `a` to $q_1$ and `b` to $q_2$. Requires fewer transitions than DFA. |
| **08** | NFA accepting strings whose second-to-last symbol is `"a"` | **NFA** | `Q08_NFA_Second_To_Last_Is_a.jff` | **States: $\{q_0, q_1, q_2\}$**, Start: $q_0$, Final: $q_2$. State $q_0$ loops on $\{a, b\}$; upon reading `a`, branches to $q_1$. From $q_1$, reading any symbol (`a` or `b`) reaches final state $q_2$. Ideal benchmark for subset construction to DFA. |
| **09** | NFA over $\Sigma = \{0, 1\}$ accepting strings containing substring `"01"` | **NFA** | `Q09_NFA_Contains_01.jff` | **States: $\{q_0, q_1, q_2\}$**, Start: $q_0$, Final: $q_2$. Initial state $q_0$ loops on `0` and `1`. On reading `0`, it nondeterministically branches to $q_1$. State $q_1$ transitions on `1` to final state $q_2$, which loops indefinitely on `0` and `1`. |
| **10** | NFA over $\Sigma = \{0, 1\}$ accepting strings that start with `0` and end with `1` | **NFA** | `Q10_NFA_Starts_0_Ends_1.jff` | **States: $\{q_0, q_1, q_2\}$**, Start: $q_0$, Final: $q_1$. From $q_0$, initial `0` moves to $q_2$. Intermediate transitions process `0` and `1`, and symbol `1` moves to accepting state $q_1$. Shows compact non-deterministic branching for prefix-suffix validation. |
| **11** | Regular expression for strings over $\Sigma = \{a, b\}$ ending in `"abb"` | **Regular Expression** | `Q11_Regex_Strings_Ending_abb.jff` | **Expression:** `(a+b)*abb`. Formal algebraic representation of the regular language where an arbitrary sequence of `a`'s and `b`'s is followed strictly by suffix `abb`. JFLAP converts this directly to Generalized Transition Graph (GTG) and DFA. |
| **12** | Regular expression for binary strings ending in `"01"` | **Regular Expression** | `Q12_Regex_Strings_Ending_01.jff` | **Expression:** `(0+1)*01`. Algebraic regex specification characterizing the regular language over binary alphabet $\{0, 1\}$ with suffix `01`. Demonstrates Kleene star closure followed by concatenation. |
| **13** | Regular expression for strings over $\Sigma = \{a, b\}$ containing exactly one `"a"` | **Regular Expression** | `Q13_Regex_Exactly_One_a.jff` | **Expression:** `b*ab*`. Specifies all strings containing any number of `b`'s, exactly one single occurrence of `a`, followed by any number of `b`'s. Demonstrates language partitioning by count restriction. |
| **14** | Right-linear regular grammar generating $L = \{a^* b a\}$ | **Regular Grammar** | `Q14_Regular_Grammar_a_star_b_a.jff` | **Productions:** $S \to aS \mid bA$, $A \to a$. Non-terminal $S$ produces zero or more leading `a`'s, then generates `b` transitioning to non-terminal $A$, which terminates with single terminal `a`. Strictly right-linear regular grammar format. |
| **15** | Regular grammar for systematic conversion to equivalent DFA | **Regular Grammar** | `Q15_Regular_Grammar_To_DFA_Conversion.jff` | **Productions:** $S \to aA \mid bS \mid b$, $A \to a \mid bA$. Demonstrates the formal isomorphism between regular grammars and finite state machines, where non-terminals map directly to states and productions map to state transitions. |
| **16** | Mealy machine synchronous sequence detector for pattern `"01"` | **Mealy Machine** | `Q16_Mealy_Machine_Detect_01.jff` | **States: $\{q_0, q_1\}$**, Start: $q_0$. Outputs are associated with transitions: $q_0 \xrightarrow{0 / 0} q_1$, $q_0 \xrightarrow{1 / 0} q_0$, $q_1 \xrightarrow{0 / 0} q_1$, $q_1 \xrightarrow{1 / 1} q_0$. Output `1` is emitted at the exact transition step where the sequence `"01"` is completed. |
| **17** | Moore machine sequence detector for pattern `"01"` | **Moore Machine** | `Q17_Moore_Machine_Detect_01.jff` | **States: $\{q_0, q_1, q_2\}$**, Outputs: $\lambda(q_0) = 0$, $\lambda(q_1) = 0$, $\lambda(q_2) = 1$. Outputs depend strictly on current state. State $q_0$ (initial), $q_1$ (prefix `0`), and $q_2$ (matched `"01"` emitting output `1`). Demonstrates 1-cycle delay compared to Mealy. |
| **18** | Context-Free Grammar generating classic language $L = \{a^n b^n \mid n \ge 0\}$ | **CFG** | `Q18_CFG_Language_AnBn.jff` | **Productions:** $S \to aSb \mid \lambda$. Canonical context-free grammar generating matching counts of leading `a`'s and trailing `b`'s, proving non-regularity via pumping lemma and expressing recursive nested structure. |
| **19** | Context-Free Grammar generating palindromes over $\Sigma = \{a, b\}$ | **CFG** | `Q19_CFG_Palindromes.jff` | **Productions:** $S \to aSa \mid bSb \mid a \mid b \mid \lambda$. Generates both even-length and odd-length palindromic strings by expanding matching outer terminals recursively and terminating on base cases ($a, b, \lambda$). |
| **20** | Context-Free Grammar for balanced parentheses (Dyck language) | **CFG** | `Q20_CFG_Balanced_Parentheses.jff` | **Productions:** $S \to (S)S \mid \lambda$. Generates all well-formed, properly nested, and concatenated strings of parentheses. Fundamental grammar for compiler syntax analysis and pushdown automata conversion. |
| **21** | Grammar in Chomsky Normal Form (CNF) for $L = \{a^n b^n \mid n \ge 1\}$ | **CFG (CNF)** | `Q21_CFG_Chomsky_Normal_Form_CNF.jff` | **Productions:** $S \to AX \mid AB$, $X \to SB$, $A \to a$, $B \to b$. Converted to strict CNF format where every production is either $A \to BC$ (two variables) or $A \to a$ (single terminal). Prerequisite for the CYK parsing algorithm. |
| **22** | Context-Free Grammar with unit and single terminal derivations | **CFG** | `Q22_CFG_Single_Symbol_Derivation.jff` | **Productions:** $S \to A \mid b$, $A \to a$. Educational exercise demonstrating unit production elimination ($S \to A$) and simplifying grammar derivations in formal language transformations. |
| **23** | Context-Free Grammar generating multi-symbol language $L = \{a c^n b \mid n \ge 1\}$ | **CFG** | `Q23_CFG_Multiple_Symbols_Derivation.jff` | **Productions:** $S \to aAb$, $A \to cA \mid c$. Non-terminal $S$ establishes prefix $a$ and suffix $b$ enclosing non-terminal $A$, which recursively derives one or more occurrences of symbol $c$. |
| **24** | LL(1) grammar for arithmetic expressions without left-recursion | **CFG (LL Parsing)** | `Q24_LL_Grammar_Arithmetic_Expressions.jff` | **Productions:** $E \to TX$, $X \to +TX \mid \lambda$, $T \to FY$, $Y \to *FY \mid \lambda$, $F \to (E) \mid a$. Left-recursion eliminated and left-factored to allow top-down deterministic predictive parsing with 1-token lookahead. |
| **25** | Left-recursive grammar for bottom-up shift-reduce LR parsing | **CFG (LR Parsing)** | `Q25_LR_Grammar_Bottom_Up_Parsing.jff` | **Productions:** $E \to E + T \mid T$, $T \to a$. Left-recursive expression grammar naturally suited for shift-reduce bottom-up parsers (LR(0), SLR(1), LR(1)) to produce left-associative parse trees. |
| **26** | Chomsky Normal Form grammar for CYK table dynamic programming | **CFG (CYK Parsing)** | `Q26_CYK_Parsing_CNF_Grammar.jff` | **Productions:** $S \to AB \mid BC$, $A \to BA \mid a$, $B \to CC \mid b$, $C \to AB \mid a$. Strict CNF grammar designed for membership testing using Cocke-Younger-Kasami $O(n^3)$ dynamic programming matrix in JFLAP. |
| **27** | Deterministic Pushdown Automaton for $L = \{a^n b^n \mid n \ge 1\}$ | **PDA** | `Q27_PDA_Language_AnBn.jff` | **States: $\{q_0, q_1, q_2, q_3, q_4\}$**, Start: $q_0$, Final: $q_4$. $q_0 \to q_1$ pushes initial stack bottom marker $Z$. $q_1$ reads $a$ and pushes $A$ to count symbols. On reading $b$, moves to $q_2$ popping $A$. Loops popping $A$ on $b$. Reaches $q_4$ (final) on empty input and stack top $Z$. |
| **28** | Nondeterministic Pushdown Automaton for even palindromes $L = \{w w^R\}$ | **NPDA** | `Q28_NPDA_Even_Length_Palindromes.jff` | **States: $\{q_0, q_1, q_2, q_3\}$**, Start: $q_0$, Final: $q_3$. State $q_1$ reads first half $w$ and pushes corresponding symbols ($A, B$). It nondeterministically makes a $\lambda$-transition to $q_2$, guessing the midpoint. State $q_2$ matches incoming symbols with stack top. Transitions to $q_3$ on stack marker $Z$. |
| **29** | Single-Tape Standard Turing Machine deciding $L = \{0^n 1^n \mid n \ge 1\}$ | **Turing Machine** | `Q29_Turing_Machine_Standard_0n1n.jff` | **States: $\{q_0, q_1, q_2, q_3, q_4\}$**, Start: $q_0$, Final: $q_4$. State $q_0$ reads `0`, replaces with $X$, moves Right. In $q_1$, skips `0`'s and $Y$'s to find first `1`, replaces with $Y$, moves Left. $q_2$ moves Left back to $X$, then shifts right to repeat. When all $0$'s matched, checks all $Y$'s and halts in $q_4$. |
| **30** | Two-Tape Turing Machine copying arbitrary binary input string | **Multi-Tape TM** | `Q30_Turing_Machine_MultiTape_Copy.jff` | **States: $\{q_0, q_1\}$**, Start: $q_0$, Final: $q_1$. Tape 1 contains input string over $\{0, 1\}$; Tape 2 is initially blank. State $q_0$ reads symbol on Tape 1, writes identical symbol on Tape 2, and advances both heads Right. On reading blank on Tape 1, halts in $q_1$. |

---

## Instructions for Opening and Running in JFLAP

1. **Prerequisites:** 
   - Java Runtime Environment (JRE / JDK 8 or later).
   - JFLAP executable (downloadable from [jflap.org](https://www.jflap.org/modules/)).

2. **Running Models:**
   - Launch JFLAP: `java -jar JFLAP7.1.jar` (or double click the JAR file).
   - Click **File $\to$ Open** and navigate into the `JFLAP_30_Solutions_Vedang Mendhurwar` directory.
   - Select any desired problem (e.g. `Q01_DFA_Ends_With_ab.jff`).

3. **Simulating Inputs:**
   - **Step by State:** In JFLAP menu, select **Input $\to$ Step with State...** to step character by character.
   - **Fast Run / Multiple Run:** Select **Input $\to$ Multiple Run** to test a batch of accepting and rejecting strings simultaneously.
   - **Conversions:** For NFA, CFG, or Regular Grammar files, select the **Convert** menu (e.g. *Convert to DFA*, *Convert to Grammar*, *Convert to PDA*).
