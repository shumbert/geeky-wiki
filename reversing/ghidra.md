# Ghidra
sometimes when renaming variables in the decompiler, ghidra renames registers in the disassembly. this is quite confusing as the same register can be used for different things in the same function

https://reverseengineering.stackexchange.com/questions/24708/ghidra-renaming-eax

This is a feature that can be deactivated by unticking the option Markup Register Variable Reference found in the Edit -> Tool Options window in the pane Options -> Listing Fields -> Operands Field.

You can automatically highlight a variable or register throughout a function by clicking on it. By default you have to click the middle button. However you can change to the left click by going to Edit > Tool Options > Listing Fields > Cursor text highlight

## Debugger
when setting breakpoints in the GUI it may not actually registered by the back-end debugger. open the debugger console and manually add the breakpoint if needed
