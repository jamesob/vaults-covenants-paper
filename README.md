Vaults are a technique for substantially reducing the risk of Bitcoin management. In
this paper, we examine their relationship to different covenant implementations. We
survey the vault implementations that are currently usable, as well as that would be
possible only with proposed consensus updates (e.g. OP_CTV). 

A new approach, `OP_VAULT`, is presented which avoids the pitfalls of a general
covenant proposal while still allowing the covenant-like behavior necessary for a
featureful vault implementation. The design assumes the deployment of package relay
and ephemeral anchors for dynamic fee management, but allows for different fee
management approaches should they come. It allows batching vault operations, partial
unvaultings, dynamic withdrawal targets, and recursive deposits.

### Compiling

Requires `xelatex`; probably, you want to install `texlive-most` on your distribution.

Use this handy shell function:

```sh
watch-tex () {
  JOBNAME=${1%.tex}
  xelatex -halt-on-error -shell-escape $1
  evince $JOBNAME.pdf &
  PDF_PS=$!
  RUNTEX="xelatex -halt-on-error -shell-escape $1"
  BIB="$JOBNAME.bib"
  if [ -f "${BIB}" ]
  then
    ls $1 | entr -s "rm -f ${BIB} ; $RUNTEX ; biber $JOBNAME ; $RUNTEX ; $RUNTEX"
  else
    ls $1 | entr -s "$RUNTEX"
  fi
  kill ${PDF_PS}
}

$ watch-tex 2022-vaults-paper.tex
```
