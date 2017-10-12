*   Add `offset` property

    adds Dissolve instance public `offset` property containing current offset

    **SamyPesse**

*   Skip large data chunks incrementally

    data should be incrementally (as we receive the data) released from the memory (buffer),
    instead of releasing single big chunk of data once it's buffered entirely
    In specific case, this resolves in peak memory allocation of ~300MB (depends on settings)
    while parsing 2GB file instead of previous peak allocation of 2GB of memory;

    *fogine*

*   Add a new `skip` operation.

    This new operation allows to easily `skip` a specific number of bytes. It
    has the same semantics as `buffer` and `string`.

    *Nikolay Perevozchikov*

*   Refactor `dissolve` internals to improve performance.

    By slicing up the `Dissolve#_transform` method into smaller methods,
    we can allow V8 to optimize these smaller methods individually, while
    making each method less prone to deoptimizations.

    Reduce GC pressure by reducing the number of intermediate arrays that get
    created in `tap` and `loop` operations

    *Arthur Schreiber*

*   Allow `objectMode` to be overridden.

    By default, the `dissolve` stream is in `objectMode`, but disabling this
    mode allows piping a `dissolve` stream into another stream that only
    accepts `Buffer` objects.

    *Lee Treveil*
