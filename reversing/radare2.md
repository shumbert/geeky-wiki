# radare2
```
aaa # automatically analyze functions
afl # print all functions
s sym.main # seek to function main
pdf # print disassembly
afvn <old name> <new name> # rename variable
```

## Visual mode
```
VV # enter visual mode
V! # fancier mode
Arrows or j/k/;/l # move around
<Tab>/<Shift>+<Tab> # change block
<Shift> + Arrows or j/k/;/l # move block around
p # shift representation
? # help
<Shift> + r # randomize colors
: # enter command move
```

## Debug
```
r2 -d <binary file> <args>
ood <args> # re-open file in debug mode
db <address> # place breakpoint
dc # run the program
dr # show registers
dr <register>=<val>  # set register value
s # step
<Shift> + s # step and do not enter function
```

