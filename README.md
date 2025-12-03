# MAUDETYPEDLOG


MaudeTypedLog is a typed logic programming interpreter tool for Prolog. The tool is written in Maude and thus requires the [Maude System to run](https://maude-lang.github.io/)


## Files
The repository contains 6 files:
* unification.maude: contains the definition for the unification algorithm
* lp-syntax.maude: contains the commonly known syntax of Prolog
* lp-semantics.maude: contains the three rules that manage the 3-value unification (unifies, false, wrong)
* detectError.maude: contains the modules responsible for verifying if a program contains type errors
* MaudeTypedLog.maude: the front-end of the tool. Contains the commands and the interaction object of the tool
* file.maude: contains built-in Maude functions to interact with the user

## How to start the tool

The user should download all the files and all of them must be in the same folder, let's say "/MaudeTypedLog" for example. The user should head to this folder and can execute the following command to start directly the interpreter:
```
maude MaudeTypedLog.maude
erewrite in MTL-IO : interpret .

   =====================================
               MaudeTypedLog
            A Maude based Typed
          Unification Interpreter
   ====================================


MaudeTypedLog>
```
The user can start firstly Maude and then load the file "MaudeTypedLog.maude":
```
maude
Maude> load MaudeTypedLog.maude
erewrite in MTL-IO : interpret .

   =====================================
               MaudeTypedLog
            A Maude based Typed
          Unification Interpreter
   ====================================


MaudeTypedLog>
```

## MaudeTypedLog commands

The MaudeTypedLog tool has 7 commands:

### list programs
This command shows a list of all the predefined and a small description of it.
```
MaudeTypedLog> list programs
Available preloaded programs:
        1. Example 1. Paper Example 1, it is type safe.
        2. Example 2. Paper Example 2. Non-free type-error.
        3. Example 3. A basic program with no type-errors.
        4. Example 4. Error-free version of program Example 2.
        5. Example 5. Program with 2 type-errors.
        6. Append example. Non-terminating example.
        7. Member example. Terminating program error-free.
        8. Sumlist example.
        9. Max example.
```

### load program <N>
This command loads a program which index is the same as appears in the "list programs" command. It does not append the program, completely substituted the older by the newer one.
```
MaudeTypedLog> load program 1
Loaded program 1
MaudeTypedLog> load program 4
Loaded program 4
```

### check
This command verifies that a program is type-safe. Generates all the generic queries and executes them. After that, verifies query per query the output and decides whether it contains a type error or not.
```
MaudeTypedLog> load program 2
Loaded program 2
MaudeTypedLog> check
Type checking program...
q(X0) :- p(a).
```

### query
This command makes a query to a loaded program. It returns "True" if the query unifies, "No solution" in case it does not unify and "Type error in this query" if every unification process reaches to a type error.
```
MaudeTypedLog> load program 1
Loaded program 1
MaudeTypedLog> query (r(1))
Executing query:
---------------------
True.
```

In order to make a query the syntax is very similar to Prolog, but has a few differences.
* Variables must be written as X(<N>), being N the id of the variable
* Queries must be introduced inside parenthesis, as shown in the example.
* Introducing the term "s(0)" may result in execution errors due to parsing.


### show program
This command prints the loaded program.
```
MaudeTypedLog> load program 1
Loaded program 1
MaudeTypedLog> show program
Show program function:
---------------------
Program clauses:
p(1) :- .
p(0) :- .
q(1) :- .
q(a) :- .
r(X0) :- p(X0), q(X0).
```

### show predicates
This command prints the heads of every predicate of the loaded program.
```
MaudeTypedLog> show predicates
Show predicates function:
---------------------
Program predicates:
p(1)
p(0)
q(1)
q(a)
r(X0)
```


### quit

In order to leave the tool the user should execute the "quit" command.
```
MaudeTypedLog> quit
Goodbye
rewrites: 66714 in 150ms cpu (722088ms real) (444760 rewrites/second)
result Portal: <>
Bye.
```