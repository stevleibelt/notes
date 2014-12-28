# [2014-12-28 by raichoo](https://events.ccc.de/congress/2014/Fahrplan/events/6162.html)

# outline

* dependent types
* correspondence and constrcutive logic
* live coding with [idris](http://en.wikipedia.org/wiki/Idris_(programming_language))
* effects
* type providers

# idris

* developed by edwin brady
* intented as a research tool
* pure functional programming language (like haskell)
* dependently typed
* syntax is close to haskell
* focus on general purpose programming
* totality checking
* interactive proving with tactics (similar to [Coq](http://en.wikipedia.org/wiki/Coq))

# motivation

* expressivity
    * types keep our runtime behaviour in check
    * more expressive type systems allow us to encode more invariants
    * type level language is a language of its own

# dependent types

* value to value (normally called functions)
* type to value (bind a function a variable)
* type to type (list or data structure)
* value to type (thats the new thing, e.g. string vector with the content "string" and the length "1 + n")
* vector (general vector)

# curry howard correspondence

* proof (usefull for test/type driven development)
* truth
* falsity
* conjunction (and proof using)
* disjunction (or proof using)
* implication
* universal quantification ([proof by induction](http://en.wikipedia.org/w/index.php?title=Proof_by_induction&redirect=no)
* existential quantification
* negation
* law of the excluded middle
