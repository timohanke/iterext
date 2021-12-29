# iterext
Extensions for Motoko Iter package

Sometimes it is required to multiple values at once from an iterator. The `Iter` package provides the function `next` which only gets one value, if available. 

Moreover, it canont be known in advance how many values an interator has available. The `Iter` package provides the function `size` but calling it will consume all values from the iterator, i.e. the values cannot be obtained anymore after calling `size`.

In this extension package we provide a fixed length buffer. The buffer provides a method `fill` which can be called on an iterator. Then the buffer will be filled with values from the iterator until the buffer is full or the iterator is exhausted. If the buffer is full then it can be later reset and used again to be filled from the same iterator. If the iterator is exhausted but the buffer not yet full then the buffer can be continued to be filled from the current fill level onwards with values from another iterator.

Example:
```
import Iter "mo:base/Iter";
import IterExt "iterext.mo";
let buffer : BlockBuffer<Nat> = BlockBuffer(64);
let iter = Iter.range(1,100);
buffer.fill(iter);
let a : [Nat8] = buffer.toArray();
```
This will create an array `a` of length `64` filled with `1,2,...,64`.
