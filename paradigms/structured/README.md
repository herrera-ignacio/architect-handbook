# Structured Programming

> Structured programming imposes discipline on direct transfer of control.

The first paradigm to be adopted (but not the first to be invented) was structured programming, which was discovered by _Edsger Sybe Dijkstra_ in __1968__.  Dijkstra showed that the use of unrestrained jumps (`goto` statements) is harmful to program structure. He replaced those jumps with the more familiar `if`/`then`/`else`  and `do`/`while`/`until` constructs.

## History

> Edsger Wybe Dijkstra born in Rotterdam in 1930, and in 1948 graduated from high school with highest possible marks in math, physics, chemistry, and biology. In March 1952, at the age of 21, Dijkstra took a job with the Mathematical Center of Amsterdam as the Netherderland's very first programmer. In 1955, he concluded that the intellectual challenge of programming was greater than the intellectual challenge of theoretical physics. As a result, he choose programming as his long-term career.

Dijkstra started his career in the era of vacuum tubes, when computers were huge, fragile, slow, unreliable, and extremly limited. Programs were written in binary, or in very crude assembly language. Input took the physical form of paper tape or punched cards. The edit/compile/test loop was hours, if not days, long.

The problem that Dijkstra recognized, early on, was that programming is _hard_, and a program of any complexity contains too many details for a human brain to manage without help. Overlooking just one small detail results in programs that may seem to work, but fail in surprising ways.

> Dijkstra's solution was to apply the mathematical discipline of __proof__. His vision was the construction of a Euclidian hierarchy of postulates, theorems, corollaries, and lemmas. Programmers would use proven structures, and tie them together with code that they would then prove correct themselves.

Dijkstra realized that he would have to demostrate the technique for writing basic proofs of simple algorithms. This he found to be quite challenging. During his investigation, Dijkstra discovered that certain uses of `goto` statements prevent modules from being decomposed recursively into smaller and smaller units, thereby preventing use of the divide-and-conquer approach necessary for reasonable proofs.

Dijkstra realized that there were some "good" uses of `goto` corresponding to simple selection and iteration constrol structures such as `if/then/else` and `do/while`. Modules that used only those kinds of control structures _could_ be recursively subdivided into provable units.

Dijkstra knew that those control structures, when combined with sequential execution, were special. They had been identified two years before by _Bohm and Jacopini_ who proved that __all programs can be constructured from just three structures: sequence, selection, and iteration__.

This discovery was remarkable:

> The very control structures that made a module provable were the same minimum set of control structures from which all programs can be built. Thus structured programming was born.

Dijkstra showed that __sequential statements could be proved correct through simple enumeration__. The technique mathematically traced the inputs of the sequence to the outputs of the sequence. This approach was no different from any normal mathematical proof.

> Dijkstra tackled selection through reapplication of enumeration. Each path through the selection was enumerated. If both paths eventually produced appropriate mathematical results, then the proof was solid.

To __prove iteration correct__, Dijkstra had to use __induction__. He proved the case for 1 by enumeration. Then he probed the case that if N was assumed correct, N + 1 was correct, again by enumeration. He also proved the starting and ending criteria of the iteration by enumeration.

> In _1968_, Dijkstra wrote a letter to the editor of _CACM_, which was published in the March issue. The title of this letter was _"Go To Statement Considered Harmful"_. The article outlined his position on the tree control structures. Eventually the argument petered out. As computer languages evolved, the `goto` statement moved ever rearward, until it all but disappeared.

> Nowadays we are all structured programmers, though not necessarily by choice. It's just that our lagnuages don't give us the option to use undisciplined direct transfer of control.
