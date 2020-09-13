# Miscellaneous tools
## hexdump
```
hexdump -C <binary>
```

## objdump
```
objdump -d <binary>
objdump -x <binary>
objdump -R <binary> # print dynamic relocations
```

## Dynamic linker
```
LD_DEBUG=all /path/to/binary # print dynamic loader debug information
```

