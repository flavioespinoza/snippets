# snippets
Code snippets I don't want to forget


### Using an arithmetic operator inside a variable

- https://github.com/koalaman/shellcheck/issues/2000
 
**`Rule Id`**: SC1102

For bugs

My shellcheck version: 0.7.1
 The rule's wiki page does not already cover this
 I tried on shellcheck.net and verified that this is still a problem on the latest commit
Here's a snippet or screenshot that shows the problem:

```shell
#!/bin/sh
op='+'
echo "$((1 $op 2))"
Here's what shellcheck currently says:
Line 3:
echo "$((1 $op 2))"
     ^-- SC2005: Useless echo? Instead of 'echo $(cmd)', just use 'cmd'.
      ^-- SC1102: Shells disambiguate $(( differently or not at all. For $(command substition), add space after $( . For $((arithmetics)), fix parsing errors.
```
Here's what I wanted or expected to see:
No warnings.

Using an arithmetic operator inside a variable is fine in busybox's sh and in bash 5:

```shell
$ docker run --rm -v "$PWD:/mnt" alpine sh /mnt/op.sh 
3
$ bash op.sh 
3
$
```
