# Monitor output of python script with tee
Python interpreter output is buffered so you might not see anything when piping to tee. You can use the -u option to fix that:
```
   -u     Force stdin, stdout and stderr to  be  totally  unbuffered.   On  systems
          where it matters, also put stdin, stdout and stderr in binary mode.  Note
          that there is internal buffering in xreadlines(), readlines()  and  file-
          object  iterators  ("for  line  in sys.stdin") which is not influenced by
          this option.  To work around this, you will want to use  "sys.stdin.read‐
          line()" inside a "while 1:" loop.
```
