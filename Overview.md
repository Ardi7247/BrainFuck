# Description
If you're here you probably have a general idea of what brainfuck is, Although if you don't, see the [wiki](https://en.wikipedia.org/wiki/Brainfuck) or read below.
Regardless of your knowledge on brainfuck, I hope I can provide insight or information to further your understanding. Although, at the end of the day
it's not that serious. This is an esolang so the goal is to present a mental challenge or have fun.

## Commands
`>` Moves the 2D cursor one cell to the right.

`<` Moves the 2D cursor one cell to the left.

`+` Increment the current cell by one.

`-` Decrement the current cell by one.

`.` Writes the current byte to console.

`,` Accepts one byte of input from the user.

`[` If the current cell's byte is equal to zero, move the 2D cursor immediately to the instruction after the matching '\]' symbol.

`]` Returns to the instruction after the matching '\[' symbol.

#### These instructions are Turing complete, meaning it can simulate any Turing machine. A Brainfuck program will either halt, or continue forever.

### So, what can you do with these instructions?

Many things. If you plan to experiment with brainfuck, I highly recommend [this](https://ashupk.github.io/Brainfuck/brainfuck-visualizer-master/) wonderful interpreter.
It can greatly help visualization and debugging of brainfuck code, and has one of the most interactive and useful layouts. Plus, it's totally free. Huge credit to
[Ashu Prakash](https://ashupk.github.io/) for creating this. That aside, brainfuck can do many things. For example, adding two numbers.

#### Addition

```
++ ;Set the first cells value to 2
> ;Move the 2D cursor 1 cell to the right
++ ;Set the second cells value to 2
[- ;Creates a loop and subtracts 1 from this cell each iteration
<+> ;Adds 1 to the first cell then moves back to continue loop
]< ;End loop and return cursor to cell 1
. ;Print current cell
```

The above code will return the number 4, as the result of 2+2. We can do something similar for subtraction.

#### Subtraction

```
++ ;Set the first cells value to 2
> ;Move the 2D cursor 1 cell to the right
++ ;Set the second cells value to 2
[- ;Creates a loop and subtracts 1 from this cell each iteration
<-> ;Subtracts 1 from the first cell then moves back to continue loop
]< ;End loop and return cursor to cell 1
. ;Print current cell
```

Cool, we can add and subtract. However, things get a little more complicated when we want to **Compare**. We'll need a couple of things before we're ready to
compare numbers. One of these things is a condition.

####Conditions

With conditions, we can make something akin to an If Then statement by using loops in a clever way. Loops will only execute their code
if the value of the current cell is greater than zero. So, We can make an If statement like so:

```
+ ;1 will represent a value of true here
[ ;This loop will only execute if the current cell is greater than zero
[-] ;We can use this subtraction loop to clear the current cell; This will cause the loop to not happen again after execution
>+++< ;Set the second cell to three
]
```

With this, we are essentially saying "if memory\[1] is above 0, then set memory\[2] to 3." This can function as a basic conditional statement,
and is extremely powerful for making code in brainfuck. However, what if we wanted to write a condition in a way that wouldn't interfere with the memory used or
cause it to be unusable later? In this case, we can simply clone the memory to a new cell with a loop.

```
[>+>+<<-]>> ;Clone the current cell's value to the 2 cells ahead of it; Then move to the latter clone for usage in the program
```

With this, we can move the second clone to the first position with another loop.

```
[>+>+<<-]>>
[-<<+>>] ;Add the current cell's value 2 cells to the left
```

From there, a condition that preserves memory is easy. We just need to put it all together.

```
+ ;Set Cell 1 to the value of 1
[>+>+<<-]>> ;Clone the current cell's value to the 2 cells ahead of it; Then move to the latter clone for usage in the program
[-<<+>>] ;Add the current cell's value 2 cells to the left
< ;Move the 2D cursor to the 2nd Cell
[[-]
>+++< ;Set cell 3 to 3
]
```

Now, if cell 1's value is greater than 0, then cell 3's value will be set to 3. This time, however we keep the data in Cell 1 to be used later.

# More coming soon

