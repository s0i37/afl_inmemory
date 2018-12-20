## My little changes

Inspired http://shell-storm.org/blog/In-Memory-fuzzing-with-Pin/

#### Steps to reproduce

Run any target application, for example:

`./inmemory`

Instrument blackbox application through https://github.com/s0i37/DBI/blob/master/pin/afl/fuzz.cpp using RVA offsets:

`__AFL_SHM_ID=1337 pin -pid $(pidof inmemory) -t /full/path/to/DBI/pin/afl/fuzz.so -module inmemory -entry 0x151 -exit 0x1d4`

Interact with application to entering to infinity loop.

Run AFL:

`__AFL_SHM_ID=1337 AFL_NO_FORKSRV=1 AFL_SKIP_BIN_CHECK=1 ~/src/afl/afl-fuzz -i in -o out -- banner`

Average fuzz speed ~30000/s iteration in trivial example
