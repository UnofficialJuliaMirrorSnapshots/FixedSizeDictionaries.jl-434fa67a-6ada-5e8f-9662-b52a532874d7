
[![Build Status](https://travis-ci.org/SimonDanisch/FixedSizeDictionaries.jl.svg?branch=master)](https://travis-ci.org/SimonDanisch/FixedSizeDictionaries.jl)
[![Build status](https://ci.appveyor.com/api/projects/status/rug74qwk1dbl62wx?svg=true)](https://ci.appveyor.com/project/SimonDanisch/fixedsizedictionaries-jl)
[![codecov.io](https://codecov.io/github/SimonDanisch/FixedSizeDictionaries.jl/coverage.svg?branch=master)](https://codecov.io/github/SimonDanisch/FixedSizeDictionaries.jl?branch=master)
[![Coverage Status](https://coveralls.io/repos/github/SimonDanisch/FixedSizeDictionaries.jl/badge.svg?branch=master)](https://coveralls.io/github/SimonDanisch/FixedSizeDictionaries.jl?branch=master)

# FixedSizeDictionaries

Library which implements a FixedSize variant of Dictionaries.
These can be stack allocated and have `O(1)` indexing performance without boundcheck.
It implements most parts of the `Base.Dict` interface.
This package is useful, when you want anonymous composite types.
You should be a bit careful with generating a lot of FixedSizeDict's, since
it will compile a unique set of functions for every field of a Dict.

Usage: 

```Julia
    # constructors:
    kvdict = FixedKeyValueDict((:a => 22, :b => 3f0, :c => 3f0))
    FixedKeyValueDict(((:a, 22), (:b, 3f0), (:c, 3f0)))
    FixedKeyValueDict(:a => 22, :b => 3f0, :c => 3f0)
    FixedKeyValueDict((:a, :b, :c), (22, 3f0, 3f0))
    FixedKeyValueDict(Dict(:a => 22, :b => 3f0, :c => 3f0))
    @get(kvdict.a) == 22
    @get(kvdict.b) == 3f0
    @get(kvdict.c) == 3f0
    keys(kvdict) == (Val{:a}, Val{:b}, Val{:c})
    values(kvdict) == (22, 3f0, 3f0)

    val = get(kvdict, Val{:a}) do
        "default"
    end
    val == 22
    val = get(kvdict, Val{:Y}) do
        "default"
    end
    val == "default"
    
    kvdict = FixedKeyDict((:a => 22, :b => 3f0, :c => 3f0))
    kvdict == FixedKeyDict(((:a, 22), (:b, 3f0), (:c, 3f0)))
    kvdict == FixedKeyDict(:a => 22, :b => 3f0, :c => 3f0)
    kvdict == FixedKeyDict((:a, :b, :c), [22, 3f0, 3f0])
    kvdict == FixedKeyDict(Dict(:a => 22, :b => 3f0, :c => 3f0))

    # same functions as FixedKeyValueDict plus:

    @get kvdict.a = 10
    values(kvdict) == (10, 3f0, 3f0)
    
```


## Automatic generated API docs:

---

<a id="type__abstractfixedsizedict.1" class="lexicon_definition"></a>
#### FixedSizeDictionaries.AbstractFixedSizeDict{Keys} [¶](#type__abstractfixedsizedict.1)
Dictionary types which keys are fixed at creation time


*source:*
[FixedSizeDictionaries/src/core.jl:4](https://github.com/SimonDanisch/FixedSizeDictionaries.jl/tree/1822b7619c5e50d427aad995057f6931a72a2f54/src/core.jl#L4)

---

<a id="type__fixedkeydict.1" class="lexicon_definition"></a>
#### FixedSizeDictionaries.FixedKeyDict{Keys<:Tuple, Values<:AbstractArray{T, 1}} [¶](#type__fixedkeydict.1)
Dictionary types which keys are fixed at creation time


*source:*
[FixedSizeDictionaries/src/core.jl:15](https://github.com/SimonDanisch/FixedSizeDictionaries.jl/tree/1822b7619c5e50d427aad995057f6931a72a2f54/src/core.jl#L15)

---

<a id="type__fixedkeyvaluedict.1" class="lexicon_definition"></a>
#### FixedSizeDictionaries.FixedKeyValueDict{Keys<:Tuple, Values<:Tuple} [¶](#type__fixedkeyvaluedict.1)
Dictionary types which keys and values are fixed at creation time


*source:*
[FixedSizeDictionaries/src/core.jl:9](https://github.com/SimonDanisch/FixedSizeDictionaries.jl/tree/1822b7619c5e50d427aad995057f6931a72a2f54/src/core.jl#L9)

---

<a id="macro___get.1" class="lexicon_definition"></a>
#### @get(expr) [¶](#macro___get.1)
Allows getfield like access to the keys of a FixedDict


*source:*
[FixedSizeDictionaries/src/core.jl:145](https://github.com/SimonDanisch/FixedSizeDictionaries.jl/tree/1822b7619c5e50d427aad995057f6931a72a2f54/src/core.jl#L145)

## Internal

---

<a id="method__call.1" class="lexicon_definition"></a>
#### call(::Type{FixedSizeDictionaries.FixedKeyDict{Keys<:Tuple, Values<:AbstractArray{T, 1}}},  key_values) [¶](#method__call.1)
Constructor for a list of pairs of key => value.
Arbitrary data structures of length 2 can be used


*source:*
[FixedSizeDictionaries/src/core.jl:63](https://github.com/SimonDanisch/FixedSizeDictionaries.jl/tree/1822b7619c5e50d427aad995057f6931a72a2f54/src/core.jl#L63)

---

<a id="method__call.2" class="lexicon_definition"></a>
#### call(::Type{FixedSizeDictionaries.FixedKeyValueDict{Keys<:Tuple, Values<:Tuple}},  key_values) [¶](#method__call.2)
Constructor for a list of pairs of key => value.
Arbitrary data structures of length 2 can be used


*source:*
[FixedSizeDictionaries/src/core.jl:41](https://github.com/SimonDanisch/FixedSizeDictionaries.jl/tree/1822b7619c5e50d427aad995057f6931a72a2f54/src/core.jl#L41)

---

<a id="method__call.3" class="lexicon_definition"></a>
#### call{N}(::Type{FixedSizeDictionaries.FixedKeyDict{Keys<:Tuple, Values<:AbstractArray{T, 1}}},  keys::NTuple{N, Symbol},  values::AbstractArray{T, 1}) [¶](#method__call.3)
Constructor for a list of keys together with a list of values which should have the same length


*source:*
[FixedSizeDictionaries/src/core.jl:54](https://github.com/SimonDanisch/FixedSizeDictionaries.jl/tree/1822b7619c5e50d427aad995057f6931a72a2f54/src/core.jl#L54)

---

<a id="method__call.4" class="lexicon_definition"></a>
#### call{N}(::Type{FixedSizeDictionaries.FixedKeyValueDict{Keys<:Tuple, Values<:Tuple}},  keys::NTuple{N, Symbol},  values::NTuple{N, Any}) [¶](#method__call.4)
Constructor for a list of keys together with a list of values which should have the same length


*source:*
[FixedSizeDictionaries/src/core.jl:31](https://github.com/SimonDanisch/FixedSizeDictionaries.jl/tree/1822b7619c5e50d427aad995057f6931a72a2f54/src/core.jl#L31)

---

<a id="method__call.5" class="lexicon_definition"></a>
#### call{T<:FixedSizeDictionaries.AbstractFixedSizeDict{Keys}}(::Type{T<:FixedSizeDictionaries.AbstractFixedSizeDict{Keys}},  args...) [¶](#method__call.5)
Generic constructor that dispatches XDict(pair, pair, ...) to XDict((pair, pair))


*source:*
[FixedSizeDictionaries/src/core.jl:22](https://github.com/SimonDanisch/FixedSizeDictionaries.jl/tree/1822b7619c5e50d427aad995057f6931a72a2f54/src/core.jl#L22)

---

<a id="method__getfield_expr.1" class="lexicon_definition"></a>
#### getfield_expr(dict,  key) [¶](#method__getfield_expr.1)
generates the expression to acces a field of a dict via a Val{Symbol}


*source:*
[FixedSizeDictionaries/src/core.jl:138](https://github.com/SimonDanisch/FixedSizeDictionaries.jl/tree/1822b7619c5e50d427aad995057f6931a72a2f54/src/core.jl#L138)
