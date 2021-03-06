# Python implementation of `head`

In this exercise, we'll write a Python program to emulate the Unix `head` command.
If you read `man head`, you will see that this program (probably) defaults to showing the first 10 lines of a given file:

```
NAME
     head -- display first lines of a file

SYNOPSIS
     head [-n count | -c bytes] [file ...]

DESCRIPTION
     This filter displays the first count lines or bytes of each of the speci-
     fied files, or of the standard input if no files are specified.  If count
     is omitted it defaults to 10.

     If more than a single file is specified, each file is preceded by a
     header consisting of the string ``==> XXX <=='' where ``XXX'' is the name
     of the file.

EXIT STATUS
     The head utility exits 0 on success, and >0 if an error occurs.
```

The program should handle a _single_ file provided as a positional argument:

```
$ ./head.py inputs/the-bustle.txt
The bustle in a house
The morning after death
Is solemnest of industries
Enacted upon earth,--

The sweeping up the heart,
And putting love away
We shall not want to use again
Until eternity.
```

The program should accept a `-n` or `--num` option for the number of lines to show (default 10):

```
$ ./head.py -n 5 inputs/sonnet-29.txt
Sonnet 29
William Shakespeare

When, in disgrace with fortune and men’s eyes,
I all alone beweep my outcast state,
```

The program should reject any argument that is not a readable file:

```
$ ./head.py blargh
usage: head.py [-h] [-n int] FILE
head.py: error: argument FILE: can't open 'blargh': \
[Errno 2] No such file or directory: 'blargh'
```

The program should reject a `--num` argument less than 1:

```
$ ./head.py -n 0 inputs/gettysburg.txt
usage: head.py [-h] [-n int] FILE
head.py: error: --num "0" must be greater than 0
```

Given no arguments, it should print a short usage:

```
$ ./head.py
usage: head.py [-h] [-n int] FILE
head.py: error: the following arguments are required: FILE
```

Or a longer usage for `-h` or `--help`:

```
$ ./head.py -h
usage: head.py [-h] [-n int] FILE

Rock the Casbah

positional arguments:
  FILE               Input file

optional arguments:
  -h, --help         show this help message and exit
  -n int, --num int  Number of lines (default: 10)
```

The program should pass all tests:

```
$ make test
pytest -xv test.py
============================= test session starts ==============================
...
collected 8 items

test.py::test_exists PASSED                                              [ 12%]
test.py::test_usage PASSED                                               [ 25%]
test.py::test_bad_file PASSED                                            [ 37%]
test.py::test_bad_num PASSED                                             [ 50%]
test.py::test_default PASSED                                             [ 62%]
test.py::test_num_1 PASSED                                               [ 75%]
test.py::test_n_2 PASSED                                                 [ 87%]
test.py::test_num_3 PASSED                                               [100%]

============================== 8 passed in 0.54s ===============================
```
