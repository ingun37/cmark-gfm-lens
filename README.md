# CMarkGFM Lens

Collection of Lens for [cmark-gfm](https://hackage.haskell.org/package/cmark-gfm)

This package is written in the style of [writing lenses without lens](https://github.com/ekmett/lens/wiki/How-can-I-write-lenses-without-depending-on-lens%3F) making it a lightweight dependency.

```haskell
import CMarkGFM
import CMarkGFM.Lens
import Control.Lens

foo :: CMark.Node -> ()
foo node =
  let posInfo = node ^. _posInfo             -- get PosInfo
      nodeType = node ^. _nodeType           -- get NodeType
      text = node ^. _nodeType . _TEXT       -- get content of TEXT with Prism' NodeType Text
      childNodes  = node ^. _nodesLens       -- get [Node] with Lens' Node [Node]
      childNodes' = node ^.. _nodesTraversal -- get [Node] with Traversal' Node [Node]
      -- Remove all the TEXTs at depth 2
      node'' = set (_nodesTraversal . _nodesTraversal . _nodeType . _TEXT) "" node
   in ()
```

For the lenses for `cmark-lens` go https://github.com/ingun37/cmark-lens