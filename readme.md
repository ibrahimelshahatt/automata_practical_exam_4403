# Automata Theory Examples: DFA and Turing Machine

This repository contains examples of formal language automata:
1.  A Deterministic Finite Automaton (DFA) for recognizing strings containing the substring "101".
2.  A Python implementation of a Turing Machine (TM) that decides if a given binary number is divisible by 3.

---

## Problem 1: DFA for Substring "101"

This DFA accepts any binary string that contains the substring "101" at least once.

### 1. Formal Definition

The DFA is defined as M = (Q, Σ, δ, q₀, F) where:

*   **Q = {q0, q1, q2, q3}** (Set of states)
    *   `q0`: Initial state (no part of "101" seen, or pattern broken).
    *   `q1`: The last input symbol was '1' (potential start of "101").
    *   `q2`: The last two input symbols were "10" (potential "101" prefix).
    *   `q3`: The substring "101" has been encountered (accepting state).
*   **Σ = {0, 1}** (The input alphabet).
*   **q₀ = q0** (The start state).
*   **F = {q3}** (The set of accept states).
*   **δ (Transition Function):**

    | Current State | Input '0' | Input '1' |
    |---------------|-----------|-----------|
    |      q0       |    q0     |    q1     |
    |      q1       |    q2     |    q1     |
    |      q2       |    q0     |    q3     |
    |      q3       |    q3     |    q3     |

    Alternatively, as a list of transitions:
    *   δ(q0, 0) = q0
    *   δ(q0, 1) = q1
    *   δ(q1, 0) = q2
    *   δ(q1, 1) = q1  (e.g., if input is "11", we've seen '1', so stay in q1)
    *   δ(q2, 0) = q0  (e.g., if input is "100", pattern "10" is broken, restart)
    *   δ(q2, 1) = q3  (e.g., if input is "101", substring found!)
    *   δ(q3, 0) = q3  (Once "101" is found, any subsequent input keeps it in the accept state)
    *   δ(q3, 1) = q3

### 2. State Diagram

```mermaid
graph LR
    --> q0;
    q0--0-->q0;
    q0--1-->q1;
    q1--0-->q2;
    q1--1-->q1;
    q2--0-->q0;
    q2--1-->q3;
    q3--0-->q3;
    q3--1-->q3;
    q3((q3));

Problem 2: Turing machine for binary division by

This section describes the Turing Machine (TM) implemented in Python ('tm_divisibl) that determines whether a given binary input string represents a different number of numberstm_divisible_by_3.py

How to

TM handles the binary string from left to right, keeping track of the remainder of the number encountered so far when split by 3
A binary number can be processed bit by bit using the following recurrence:
If it is the number that the first represents Nk The bits and coefficient of the remainder 3 is 'rim = N% 3.
whenrem = N % 3b (0 or 1) is the app

The new number is ".N' = 2*N + b

The new remainder is "rim" = (2 * N + b) % 3 = (.rem' = (2*N + b) % 3 = (2*(N % 3) + b) % 3 = (2*rem + b) % 3

TM uses three main cases to represent these r

q_rem0The number processed so far is identical to 0 (.mod.

q_rem1The number processed so far matches 1 (.mod.

q_rem2The number processed so far matches 2 (

TM starts at (the initial value represents 0, which has a remainder of 0). It reads each bit, updates the state based on the above iteration, and moves rq_rem0
When the empty symbol ('⊔) encounters at the end of⊔

If you're in q_rem0, the number is divisible by 3, so it goes to q_rem0q_accept.

If you are in "q_r or"q_rem2q_rem1q_rem2, the number is not divisible by 3, so it moves to 'q_reje.q_reject

Python implementation ('tm_divisibltm_divisible_by_3.py)

Python script consists of two main types:

Year "TuringMachi" separated.TuringMachine

The function 'create_divisible_by_3_tm() that specifies and returns the TM specified for this problem.create_divisible_by_3_tm()

TuringMachine Class

__init__(self, states, input_alphabet, tape_alphabet, transitions, start_state, accept_state, reject_state, blank_symbol='⊔'):
Initializes the TM with its components. The transitions Expected as a dictionary of dictionaries: '{'current_state': {'symbol_read': ('next_state', 'symbol_to_write', 'direction').{'current_state': {'symbol_read': ('next_state', 'symbol_to_write', 'direction')}}

_initialize_tape(self, input_string)Set
up the ribbon as a dictionary to assign positions to symbols

simulate(self, input_string, max_steps=1000):
Runs the TM simulation on the input_stringReturns "true" for acceptance, TrueFalse to reject or if it has been exceeded. Prints the results and steps taken.max_steps

create_divisible_by_3_tm() function

This function defines the specific components of division.

States: '{'q_rem0', 'q_rem1', 'q_rem2', 'q_accept', 'q_{'q_rem0', 'q_rem1', 'q_rem2', 'q_accept', 'q_reject'}

Input Alphabet: {'0', '1'}

Tape Alphabet: '{'0', '1', '⊔ (where {'0', '1', '⊔'}⊔ Is it BL

Start State: q_rem0

Accept State: 'q_accepq_accept

Reject State: q_reject

Transitions:

From (current number % 3 == 0):q_rem0

Read "0": "(0*2 + 0)% 3 = 0. Go to (0*2 + 0) % 3 = 0q_rem0To write

Reading "1": "(0*2 + 1)%. Go to (0*2 + 1) % 3 = 1q_rem1، WRI

: Rayais the limit of the number, and the remainder is equal to 0. ⊔q_accept، WR, Stay.⊔

From (current number % 3 == 1):q_rem1

Read "0":. Go to (1*2 + 0) % 3 = 2q_rem2, write '0', move Right.

Read '1': . Go to (1*2 + 1) % 3 = 0q_rem0, write '1', move Right.

: read the number ends, the remainder is 1.: Move to ⊔q_reject, write , Stay.⊔

From (current number % 3 == 2):q_rem2

Read '0': . Go to (2*2 + 0) % 3 = 1q_rem1, type "0", and move right.

Read '1': . Go to (2*2 + 1) % 3 = 2q_rem2, type "1", and move right.

Read : Number ends, remainder is 2. Go to ⊔q_reject, write , Stay.⊔

How to Run

Save the Python code as .tm_divisible_by_3.py

Run it from your terminal:

python tm_divisible_by_3.py
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

The script will execute predefined test cases and print the results.

Example Output for input "110" (binary for 6, which is divisible by 3):

Input: '110'
Accepted '110' in 4 steps.
Result: Accept (Expected: Accept)
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

Example Output for input "101" (binary for 5, not divisible by 3):

Input: '101'
Rejected '101' in 4 steps.
Result: Reject (Expected: Reject)
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

The empty string is treated as 0, which is divisible by 3, and is accepted.""

This README provides a comprehensive overview of both the DFA for "101" and the Turing Machine for divisibility by 3.

IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END