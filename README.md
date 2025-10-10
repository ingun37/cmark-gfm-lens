# CMarkGFM Lens

Unofficial collection of Lens for [cmark-gfm](https://hackage.haskell.org/package/cmark-gfm).

This package is written in the style of [writing lenses without lens](https://github.com/ekmett/lens/wiki/How-can-I-write-lenses-without-depending-on-lens%3F) making it a lightweight dependency.

# Example
```haskell
import CMarkGFM
import CMarkGFM.Lens
import Control.Lens

foo :: CMark.Node -> ()
foo node =
  let posInfo = node ^. _posInfo             -- Lens' PosInfo
      nodeType = node ^. _nodeType           -- Lens' NodeType
      text = nodeType . _TEXT       -- Prism' NodeType Text
      childNodes  = node ^. _nodesLens       -- Lens' Node [Node]
      childNodes' = node ^.. _nodes          -- Traversal' Node [Node]
      -- Remove all the TEXTs at depth 2
      node'' = set (_nodes . _nodes . _nodeType . _TEXT) "" node
   in ()
```

For more extensive examples, go to [/test/Main.hs](/test/Main.hs).

# CMark (No GFM) Lens

For the lenses for `cmark-lens` go https://github.com/ingun37/cmark-lens