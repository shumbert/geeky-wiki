# gdb
## compile program with debugging information
```
gcc -g <source file>
```

## disassemble
```
set disassembly-flavor intel
disassemble main
```

## break points
```
break *main
break *0x0000000000400607
break <address> if i >= ARRAYSIZE # conditional breakpoint

delete # delete all breakpoints
clear <funtion> # delete breakpoints set in function

watch <var> # pause the program when var is modified
info breakpoints # shows information on all breakpoints
```
## run the program
```
file <executable> # debug executable 
run
run > /tmp/output.txt
run <arg1> <arg2> ...
start # run program until main()

continue # continue execution after breakpoint
step # goes into functions
next # do not go into functions
stepi # step one machine instruction
nexti # next one machine instruction
until # if at end of loop continue execution until loop is exited
finish # pause at the end of the current function
```

## dump registers
```
info registers
```

## set registers
```
set $eax=0
```

## print stuff
```
print $eax
x/s <address> # print as string
printf "%s\n" <address>
```
## Hooks
```
define hook-stop
info registers
x/24wx $esp
x/2i $eip
end
```

## Misc
```
<ENTER> # repeat previous intruction
```
