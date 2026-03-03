# GNU Find

> ...


## Meta

> Evaluation Framework.
> 

> **The understanding of a concept is proportional** to the time invested in deep reflection, deliberate practice, and repeated engagement with its nuances. If a Concept has been learned soft of by osmosis - then is not well understood.

### **✅** Evaluation

> What is my **epistemic assessment** of this topic? How well do I understand this subject?
> 

> See more in [Guia Mayor](https://www.notion.so/Guia-Mayor-cce02f04c4724677ba46b314151134db?pvs=21).
> 

| **Dimension** | **Note** |
| --- | --- |
| Coverage | Does this note include all essential concepts, examples, and details I need? |
| Coherence & Structure | Are the ideas logically organized and easy to follow? |
| Epistemic Self-Assessment | What is the level of capturing of the given target domain?  What is the level of ‘internationalization’ - understanding? |
| Should I Reorganize This -in My Content Forest? | Should I move, merge, or split this note in my content system for better integration? |
| Study Strategy | What’s my study Strategy? Should I Change It? |

### **🌌** Signature

> A comprehensive list of aspects to cover in order to understand a topic.
> 

> A tool is a teleologically organized causal architecture whose internal mechanisms generate environment-coupled state transformations under structured triggering regimes.
>

| Aspect                           | Description                                                                                                                                                                                                          |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nucleus (Deepest Essence) 🧬** | A recursive filesystem graph walker + boolean expression evaluator + action executor.                                                                                                                                |
| **Telos (Intent) 🎯**            | To select filesystem objects based on metadata predicates and optionally trigger side effects (print, delete, exec).                                                                                                 |
| **Gnosis (Understanding) 🧠**    | Build a mental model in three layers: (1) directory tree as a rooted graph, (2) expression as short-circuit boolean program, (3) actions as terminal operators. Understand precedence, lazy evaluation, and pruning. |
| **Relatio (Connections) 🔗**     | Complements `xargs`, `grep`, `stat`, `chmod`, `rm`, `tar`, and shell pipelines in Unix-like systems (e.g., Linux environments).                                                                                      |
| **Idoneitas (Suitability) 📐**   | Highly expressive for metadata-driven filtering; scales well with large trees; precise selection semantics.                                                                                                          |
| **Limites (Limits) ⛔**           | Performance on huge trees without pruning; unsafe deletion if mis-specified; complex quoting; portability differences between GNU and BSD variants.                                                                  |
| **Dynamis (Evolution) 🌱**       | Integration with `-printf`, improved performance heuristics, possible parallel traversal (not native), integration with modern filesystems.                                                                          |
| **Critica (Critique) 🔍**        | Syntax complexity; surprising precedence rules; danger of destructive actions; differences across implementations.      

## Formulation

A **technical object** may be modeled as a **state-transition operator**:

$S_{t+1} = T_o(S_t, \tau_t, E_t)$

For `find`:

* $S_t$: traversal state (current directory node, accumulated evaluation context).
* $\tau_t$: filesystem entry event (stat() result, name, inode metadata).
* $E_t$: environment (filesystem hierarchy, permissions, mount points).
* $T_o$: evaluation + traversal + action dispatch.

`find` operates as:

1. Traverse node.
2. Retrieve metadata.
3. Evaluate expression.
4. If true → execute actions.
5. Continue traversal (unless pruned).

## **Structure**

> What is the **internal structure** of this technical object?

### Dynamics

- **(Induced Dynamics)** What types of dynamics are induced by the technical object? Which are the types of dynamics that can be trigger? What kinds of state-transformation processes can be triggered?
- **(Conception of State)** What is the most useful formal conception of “state” for analyzing this technical object?  Which components of the state are external (i.e., environmental)?
- **(Triggering)** How are the dynamics **trigger**?  Which triggers are user-initiated, system-initiated, or externally induced?  Are triggers synchronous, asynchronous, event-driven, or continuous?
- (**Interaction - Complementary**)  Which **‘external elements’ does the technical object require** to ‘induce dynamics’?   Which **elements are** **needed to trigger** such dynamics?

## Interaction Grammar

> What grammar governs the commands executed by find?

The GNU find command is a filesystem traversal and filtering utility whose command-line grammar consists of:

`find [options] [start-point...] [expression]*`

1. Start points (paths)
2. Options (global modifiers)
3. Expression (tests, actions, and operators forming a boolean predicate)

More precisely:

```ebnf
(* 1. Top-Level Command Structure *)
find_command = 'find', [ global_option ], { global_option }, 
               [ starting_point_list ], [ expression ] ;

(* 2. Starting Points (Paths) *)
starting_point_list = path, { path } ;
path                = string_literal ;

(* 3. Global Options (Pre-expression flags) *)
global_option       = ( '-H' | '-L' | '-P' )
                    | '-D', debug_flag
                    | '-O', optimization_level ;

debug_flag          = string_literal ; (* e.g., "help", "tree", "search" *)
optimization_level  = digit ;          (* 0, 1, 2, 3 *)

(* 4. Expression Structure (Operators, Tests, Actions) *)
(* Precedence is handled by the structure: NOT > AND > OR > List (Comma) *)

expression          = list_expression ;

list_expression     = or_expression, { ',', or_expression } ;

or_expression       = and_expression, { ( '-o' | '-or' ), and_expression } ;

and_expression      = not_expression, { [ '-a' | '-and' ], not_expression } ;
(* Note: Adjacent expressions are implicitly AND-ed, hence -a is optional *)

not_expression      = ( '!' | '-not' ), not_expression
                    | primary ;

(* 5. Primaries (Tests, Actions, and Positional Options) *)
primary             = '(' expression ')'
                    | positional_option
                    | test
                    | action ;

(* 6. Positional Options (Affect tests following them *)
positional_option   = '-daystart'
                    | '-follow'
                    | '-regextype', regex_type
                    | '-maxdepth', number
                    | '-mindepth', number
                    | '-mount'
                    | '-noleaf'
                    | '-xdev' ;

(* 7. Tests (Return True or False) *)
test                = ( '-name' | '-iname' ), pattern
                    | ( '-path' | '-ipath' ), pattern
                    | ( '-regex' | '-iregex' ), pattern
                    | '-type', file_type
                    | ( '-size' ), size_spec
                    | ( '-mtime' | '-atime' | '-ctime' ), time_spec
                    | ( '-user' | '-uid' ), user_spec
                    | ( '-group' | '-gid' ), group_spec
                    | '-perm', permission_spec
                    | '-empty'
                    | '-false'
                    | '-true'
                    | '-executable'
                    | '-readable'
                    | '-writable' ;

(* 8. Actions (Perform side effects) *)
action              = '-delete'
                    | '-print'
                    | '-print0'
                    | '-printf', format_string
                    | '-ls'
                    | '-fls', output_file
                    | '-fprint', output_file
                    | '-fprint0', output_file
                    | '-fprintf', output_file, format_string
                    | '-prune'
                    | '-quit'
                    | exec_action ;

(* 9. Exec Action Structure (Complex) *)
exec_action         = exec_command, exec_terminator ;

exec_command        = ( '-exec' | '-execdir' | '-ok' | '-okdir' ), 
                      utility_name, [ argument_list ] ;

argument_list       = exec_argument, { exec_argument } ;
exec_argument       = string_literal ; (* May contain '{}' for substitution *)

(* Terminators: ';' usually requires shell escaping as \;, '+' creates a list *)
exec_terminator     = ';' | '+' ;

(* 10. Terminals and Primitive Types *)
string_literal      = ? any sequence of characters passed by the shell ? ;
number              = ? a sequence of digits [0-9]+ ? ;
digit               = '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9' ;

(* Specific arguments *)
file_type           = 'b' | 'c' | 'd' | 'p' | 'f' | 'l' | 's' | 'D' ;
pattern             = string_literal ; (* Glob pattern *)
regex_type          = string_literal ; (* e.g., "emacs", "posix-awk" *)
user_spec           = string_literal | number ;
group_spec          = string_literal | number ;
output_file         = path ;
format_string       = string_literal ;

(* Time/Size Specs (e.g., +5, -2, 10) *)
time_spec           = [ '+' | '-' ], number ;
size_spec           = [ '+' | '-' ], number, [ size_unit ] ;
size_unit           = 'b' | 'c' | 'w' | 'k' | 'M' | 'G' ;

(* Permissions can be symbolic or octal *)
permission_spec     = string_literal ; 
```

## Evaluation Model

For each filesystem entry:

- Traverse directory tree.
- Evaluate expression left-to-right.
- Apply short-circuit logic.
- If expression is true:
  - Execute action
  - If no explicit action → -print is implied

## References

- [GNU Find](https://www.gnu.org/software/findutils/manual/html_mono/find.html)
- [find](https://man7.org/linux/man-pages/man1/find.1.html)
- [Findutils](https://www.gnu.org/software/findutils/)
- [Difference between find and GNU find](https://unix.stackexchange.com/questions/475020/difference-between-find-and-gnu-find)
