# SAT Solver using DPLL

This code was originally written as an assignment for the course **EE677: Foundations of VLSI CAD** at IIT Bombay. The code solves a satisfiabilty problem in [Conjuctive Normal Form](https://www.wikiwand.com/en/Conjunctive_normal_form) (CNF) using the famous [DPLL Algorithm](https://www.wikiwand.com/en/DPLL_algorithm). If the problem is satisfiable, one possible solution is returned.

## Algorithm
The code is written in Python 3, it might not be compatible with previous versions. The problem is defined in CNF form. The DPLL algorithm can be explained by the following pseudocode.

```bash
solve_dpll(cnf):
    while(cnf has a unit clause {X}):
        delete clauses contatining {X}
        delete {!X} from all clauses
    if null clause exists:
        return False
    if CNF is null:
        return True
    select a literal {X}
    cnf1 = cnf + {X}
    cnf2 = cnf + {!X}
    return solve_dpll(cnf1)+solve_dpll(cnf2)
```

## Usage
- Please write the CNF form problem in a text file in the following way.
- For Example: (!B+A+!C)(B+A+!C)(!B+!A+!C)(B)(C) will be written as

```
!B A !C
B A !C
!B !A !C
B
C
```
- Save it in \<filename\> (example problem.txt).
- Run the following command

```bash
$ python3 SATSolver.py --input problem.txt
```

## Example
For CNF = (!B+A+!C)(B+A+!C)(!B+!A+!C)(B)(C), we get
```bash

CNF = (!B+A+!C)(B+A+!C)(!B+!A+!C)(B)(C)
Units = ['C', 'B']
CNF after unit propogation = (!A)(A)

CNF = (!A)(A)(A)
Units = ['!A', 'A']
CNF after unit propogation = ()
Null clause found, backtracking...

CNF = (!A)(A)(!A)
Units = ['!A', 'A']
CNF after unit propogation = ()
Null clause found, backtracking...

Reached starting node!
Number of Splits = 3
Unit Propogations = 6

Result: UNSATISFIABLE

```
## TODO
- [ ] Refactor into a pythonic module
- [ ] Update README
- [ ] Use argparse for command line inputs
- [ ] Add a verbosity command line option
