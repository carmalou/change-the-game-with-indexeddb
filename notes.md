- Looks like if you don't make a keypath autoincrement (like a primary key) you must initialize that index. 

- If you make the keypath autoincrement, you don't need to initialize the index

- Can you specify more than one keyPath?
    - Yes, you can specify an array of strings as keyPaths.
    - HOWEVER when you try to do a `get()` by keyPath, you must include an array of keyPaths _in the same order_.
    - If you only search by one keyPath when you've specified an array of strings, you'll get undefined _even if_ that keyPath exists