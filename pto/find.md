# find

> `find` is a command-line filesystem traversal and selection utility. It takes one or more starting points, traverses the corresponding filesystem hierarchy, evaluates an expression against each encountered filesystem object, and optionally performs an action on objects for which the expression evaluates to true.

>
> Conceptually, `find` exposes a small query-and-action language over the filesystem: **traversal domain → predicates → Boolean composition → actions**. Its interface therefore combines mechanisms that, in other systems, might be separated into a tree walker, metadata query API, expression language, and command executor.

>
> The exact capability set is implementation-dependent. The POSIX `find` utility defines a portable core, while GNU `findutils`, FreeBSD, and other UNIX implementations extend that core with additional predicates, traversal controls, actions, and formatting facilities.

## Formulation

###  What type of technical element is find?

> find is a technical production object: a software object produced to provide a particular operational capability over a technical substrate—in this case, the filesystem.

> Traverse a filesystem hierarchy → evaluate predicates on filesystem objects → perform actions on the objects that satisfy the predicates.

```text
Technical Production Object
└── find
    ├── Production purpose
    │   └── Locate/select filesystem objects
    │
    ├── Operational mechanism
    │   ├── filesystem traversal
    │   ├── predicate evaluation
    │   └── action execution
    │
    ├── Capability set
    │   ├── traversal
    │   ├── filtering/selection
    │   ├── metadata evaluation
    │   ├── expression composition
    │   └── actions on selected objects
    │
    └── Interface
        └── command-line expression
```

###  Which are the capabilities set?

| Capability category      | Capability Set                                                                            |
| ------------------------ | ----------------------------------------------------------------------------------------- |
| **Traversal**            | Recursively traverse directory hierarchies                                                |
| **Scope restriction**    | Specify starting paths; restrict traversal depth                                          |
| **Selection**            | Select objects by name, path, type, permissions, ownership, size, timestamps, links, etc. |
| **Boolean composition**  | Combine predicates with AND, OR, NOT, grouping                                            |
| **Pattern matching**     | Glob-style name/path matching                                                             |
| **Metadata inspection**  | Evaluate filesystem metadata                                                              |
| **Time-based selection** | Select by modification/access/change time                                                 |
| **Type selection**       | Files, directories, symbolic links, sockets, devices, etc.                                |
| **Action**               | Print, delete, execute commands, modify attributes, etc.                                  |
| **Result formatting**    | Control how selected paths are emitted                                                    |
| **Traversal control**    | Follow or avoid symbolic links; control descent and ordering                              |
| **Optimization**         | Predicate ordering and filesystem traversal optimizations                                 |

## Interface

> What is the interface to access the capabilities?

### Grammar

Canonical Interface Grammar:

```bash
## Grammar
find [option]  [starting-path...] [expression...]

expression
    → (test | action | operator | group)*

## Sentence
find /var/log -type f -name '*.log' -mtime -7 -print
```

Complete Grammar:

```g4
<find-command> ::= "find"
                   <global-option>*
                   <starting-point>+
                   <expression>*

<global-option> ::= "-H"
                  | "-L"
                  | "-P"
                  | "-D" <debug-options>
                  | "-O" <optimization-level>

<starting-point> ::= <pathname>

<expression> ::= <primary>
               | <operator>
               | "(" <expression> ")"

<primary> ::= <test>
            | <action>

<test> ::= <name-test>
         | <path-test>
         | <type-test>
         | <permission-test>
         | <ownership-test>
         | <size-test>
         | <time-test>
         | <link-test>
         | <filesystem-test>
         | <content-test>
         | <reference-test>
         | <miscellaneous-test>

<action> ::= "-print"
           | "-print0"
           | "-printf" <format>
           | "-ls"
           | "-delete"
           | "-exec" <command> <exec-terminator>
           | "-ok" <command> <exec-terminator>
           | "-quit"

<operator> ::= "-a"
             | "-and"
             | "-o"
             | "-or"
             | "!"
             | "-not"

<exec-terminator> ::= "\;"
                      | "+"
```


```text
find
 ├── traversal domain: /var/log
 ├── predicates:
 │    ├── type = regular-file
 │    ├── name matches *.log
 │    └── modification-time < 7 days
 └── action:
      └── print pathname
````

### Option Set

| Category                     | Flag / Expression      | Option set / capability                                   |
| ---------------------------- | ---------------------- | --------------------------------------------------------- |
| **Traversal**                | `-H`                   | Follow symbolic links specified as command-line arguments |
| **Traversal**                | `-L`                   | Follow symbolic links during traversal                    |
| **Traversal**                | `-P`                   | Never follow symbolic links; default                      |
| **Traversal**                | `-depth`               | Process directory contents before the directory itself    |
| **Traversal**                | `-maxdepth N`          | Limit traversal depth                                     |
| **Traversal**                | `-mindepth N`          | Ignore objects above minimum depth                        |
| **Traversal**                | `-xdev`, `-mount`      | Do not descend into other filesystems                     |
| **Traversal**                | `-ignore_readdir_race` | Suppress certain errors caused by directory-entry races   |
| **Name * Path Selection**    | `-name PATTERN`        | Match basename                                            |
| **Name * Path Selection**    | `-iname PATTERN`       | Case-insensitive basename matching                        |
| **Name * Path Selection**    | `-path PATTERN`        | Match complete path                                       |
| **Name * Path Selection**    | `-ipath PATTERN`       | Case-insensitive path matching                            |
| **Name * Path Selection**    | `-regex PATTERN`       | Match path using regular expression                       |
| **Type Selection**           | `-type TYPE`           | Select by filesystem object type                          |
| **Type Selection**           | `-xtype TYPE`          | Select by type after symlink resolution                   |
| **Size Selection**           | `-size N`              | Select by file size                                       |
| **Time Selection**           | `-mtime N`             | Select by modification time                               |
| **Time Selection**           | `-atime N`             | Select by access time                                     |
| **Time Selection**           | `-ctime N`             | Select by metadata-change time                            |
| **Time Selection**           | `-mmin N`              | Select by modification time in minutes                    |
| **Time Selection**           | `-amin N`              | Select by access time in minutes                          |
| **Time Selection**           | `-cmin N`              | Select by metadata-change time in minutes                 |
| **Ownership**                | `-user USER`           | Select by owner                                           |
| **Ownership**                | `-group GROUP`         | Select by group                                           |
| **Ownership**                | `-uid N`               | Select by numeric UID                                     |
| **Ownership**                | `-gid N`               | Select by numeric GID                                     |
| **Permissions**              | `-perm MODE`           | Select by permission bits                                 |
| **Links**                    | `-links N`             | Select by link count                                      |
| **Filesystem**               | `-fstype TYPE`         | Select by filesystem type                                 |
| **Filesystem**               | `-inum N`              | Select by inode number                                    |
| **Filesystem**               | `-samefile FILE`       | Select objects referring to same inode                    |
| **Content * Attributes**     | `-empty`               | Select empty files/directories                            |
| **Content * Attributes**     | `-readable`            | Select readable objects                                   |
| **Content * Attributes**     | `-writable`            | Select writable objects                                   |
| **Content * Attributes**     | `-executable`          | Select executable/searchable objects                      |
| **Boolean Composition**      | `-a`, `-and`           | Logical AND                                               |
| **Boolean Composition**      | `-o`, `-or`            | Logical OR                                                |
| **Boolean Composition**      | `!`, `-not`            | Logical negation                                          |
| **Boolean Composition**      | `\( ... \)`            | Group expressions                                         |
| **Actions**                  | `-print`               | Print pathname                                            |
| **Actions**                  | `-print0`              | Print pathname with NUL terminator                        |
| **Actions**                  | `-printf FORMAT`       | Formatted output                                          |
| **Actions**                  | `-ls`                  | Display `ls`-style information                            |
| **Actions**                  | `-delete`              | Delete selected objects                                   |
| **Actions**                  | `-exec COMMAND ... \;` | Execute command for each match                            |
| **Actions**                  | `-exec COMMAND ... +`  | Execute command with batches of matches                   |
| **Actions**                  | `-ok COMMAND ... \;`   | Execute command with confirmation                         |
| **Actions**                  | `-quit`                | Terminate traversal                                       |
| **Existence * Relationship** | `-exists`              | Select objects that exist                                 |
| **Reference Comparison**     | `-newer FILE`          | Newer than reference file                                 |
| **Reference Comparison**     | `-newermt DATE`        | Newer than specified timestamp                            |
| **Reference Comparison**     | `-anewer FILE`         | Access time newer than reference                          |
| **Reference Comparison**     | `-cnewer FILE`         | Status-change time newer than reference                   |

## References

- [find](https://en.wikipedia.org/wiki/Find_(Unix))
- [man pages - find](https://www.man7.org/linux/man-pages/man1/find.1.html)
