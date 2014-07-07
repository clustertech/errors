Copyright Info
==============

This pakcage is forked from godrobox of dropbox
https://github.com/dropbox/godropbox

Adapted by Chen, Tianxu  (jackeychen@clustertech.com)

Why this change?
==============

1. The errors package in godropbox has many dependencies and looks heavyweight
if the user only wants to use errors package.

2. The name such as DropboxError and DropboxBaseError are too specific to
Dropbox.

Changes
==============

Remove all dependency on orginal project.
Remove the Dropbox key word and use more general names for interface and
structure.

Usage
=========

1. Generate an error with stack trace:

  package main

  import (
    "fmt"

    "github.com/clustertech/errors"
  )

  func main() {
    e := errors.New("Oh, error !")
    fmt.Println(e)
  }

  The output is like:

    ERROR:
    Oh, error !

    ORIGINAL STACK TRACE:
    goroutine 1 [running]:
    main.main()
      /home/jackey/temp/test/src/main.go:14 +0x32


2. Wrap an existing error with stack trace:

  package main

  import (
    "fmt"
    "os"

    "github.com/clustertech/errors"
  )

  func main() {
    _, err := os.Stat("file/not/exsit")
    e := errors.Wrap(err, "Fail to read file")
    fmt.Println(e)
  }


  The output is like:

    ERROR:
      Fail to read file
      stat file/not/exsit: no such file or directory

      ORIGINAL STACK TRACE:
      goroutine 1 [running]:
      main.main()
        /home/jackey/temp/test/src/main.go:15 +0x61

3. Implement StackError interface to customize the error message.

The helper function StackTrace can be used:

  stack, content := errors.StackTrace()

To get more information about it, the unit test can be checked. There is
an example in the test code.

License
=======

Same as original
https://github.com/dropbox/godropbox/blob/master/license.txt
