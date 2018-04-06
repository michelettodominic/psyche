# psyche
Psyche is an esoteric programming language whose design is heavily influenced by brainf, another esoteric
programming language known for its minimalistic syntax whilst still retaining Turing-completeness. Psyche
seeks to improve upon brainf by adding a variety of features on top of brainf's canonical 8 commands:
 - Psyche adds the ability to write procedures which can optionally take arguments. Procedures are a
sequence of Psyche commands which can be executed at a later time. Whether to inline functions are
treat function calls in a more traditional sense are implementation dependent. The Eros interpreter
by default utilises function calls but inlining can be turned on by changing the optimisation level
(For more information on optimisation, go to the help command line terminal).
Instead of being named, procedures are stored in a stack. Thus, only the topmost procedure can be
accessed and called at any point in time. To get around this implementation feature, commands exist
which can modify the procedure stack.
 - Psyche also adds a stack to the traditional tape model of memory used in canonical brainf. In
canonical brainf, cells cannot be copied without in turn destroying another cell. To remedy this
problem, Psyche offers a stack which can be used to store values from a cell which can then be put
back into a cell at a later date. The values in the stack themselves cannot be altered -- the stack
can only be pushed or popped. The stack is also used to hold the arguments passed to a procedure.
Because of this, it is possible for a procedure to consume more values from the stack than it was
called with. If this should occur, a warning should be issued. In the Eros interpreter, one is, but
warnings can be turned off (For more information on warnings, go to the help command line terminal).
 - Psyche takes the concept of a command that denotes input to the program that are common in dialects
of brainf and extends it to maintaining an input store, which is a queue-like (FIFO) data structure
that holds the input of the program. The canonical , command works as it does in brainf, dequeuing
a byte from the input store, but there exists a command which can add to the input store as well.
It is implementation dependent on what to do when an EOF is reached; in the Eros interpreter, by
default the program halts, but an option to take input from standard in (usually, a keyboard)
exists (For more information on this, go to the help command line terminal). Note: enabling this
option may result in programs that do not terminate by themselves.

There are several aspects of the Psyche language which are implementation-dependent. These include the
memory model used to hold the memory of the program during its execution, as well as what should happen
during parsing when an unexpected character is encountered. The Eros interpreter implements these as such:
- By default, the Eros interpreter uses a vector (a dynamically-allocated array capable of being
resized) that can grow to be up to 30000 bytes in size. This reflects the canonical implementation of
the brainf interpreter created by Urban Mueller. The Eros interpreter will by default stop execution
and throw a runtime error if the size of the internal vector grows beyond 30000 as a guard, but this
feature can be turned off.
 - The Eros interpreter by default will allow its vector to grow in size until it reaches a max limit,
by default 30000, but this limit can be altered, or even turned off. When this occurs, the vector can
grow to as large as the C++ runtime library will allow it. However, static memory can be turned on,
which will strictly prevent the vector from resizing but will allow for wrapping to occur when moving
the data pointer. Both the memory type (static or dynamic) as well as for the behaviour when an invalid
index is reached (growing past the size limit of the vector, or wrapping in static memory) can be
altered in the memory management command line. For more information about the MMCL, type \z to enter the
MMCL.
- The Eros interpreter strictly enforces that all code outside of whitespace be valid Psyche code, outside
of comments and input, which can contain any valid ASCII characters (Note: special characters must be
encoded, similar to the traditional C-style, prepended with a \. For a list of escape sequences, type
\help escape).
 - The Eros interpreter also implements special guards in place to prevent programs from running infinite
loops. These two guards, runtime timing out and maximum memory size, are settings which help to
mitigate runtime errors; by default, they are 5 minutes and 30,000 bytes respectively, but both settings
can be altered in the MMMCL. Programs that either timed out or used too much memory can also be forced
to run again on a case-by-case basis, using the \force command. The state of the interpreter's memory
can also be rolled back to the most recent successful execution of code with the \back command.

By default, the Eros interpreter treats user input when modifying a value of memory of the input store as
bytes, meaning that entering "1" would store the ASCII character code for the digit 1, 49, not the value 1.
For ease of entering input, the Eros interpreter uses special syntax for use input. For more information
on the syntax used by the Eros interpreter, type \help input.

The Eros interpreter maintains memory between one program and the next. Because of this, there exist several
interpreter commands that allow for the direct manipulation of the input store and memory tape, as well as
for moving the memory pointer around, or for resetting the interpreter's state back to initial conditions.
Other useful commands exist as well. For a full list of commands and a brief description of what they do,
type \help commands. For a more in-depth look at what a command does and the argument(s) it takes, type
\help to enter the command line help terminal.

For a full list of valid Psyche commdands and what they do, type \help symbols.

Psyche interpreter 1.0.0 created by Dominic Micheletto.
