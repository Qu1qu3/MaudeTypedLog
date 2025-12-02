# MAUDETYPEDLOG

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
...

### show program
This command prints the loaded program.
```
MaudeTypedLog> load program 1
Loaded program 1
MaudeTypedLog> show program
Show program function:
---------------------
Program clauses:
p(s(0)) :- .
p(0) :- .
q(s(0)) :- .
q(a) :- .
r(s(X0)) :- p(s(X0)), q(s(X0)).
```

### show predicates
This command prints the heads of every predicate of the loaded program.
```
MaudeTypedLog> show predicates
Show predicates function:
---------------------
Program predicates:
p(s(0))
p(0)
q(s(0))
q(a)
r(s(X0))
```