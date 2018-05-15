- Looks like if you don't make a keypath autoincrement (like a primary key) you must initialize that index. 

- If you make the keypath autoincrement, you don't need to initialize the index

- Can you specify more than one keyPath?
    - Yes, you can specify an array of strings as keyPaths.
    - HOWEVER when you try to do a `get()` by keyPath, you must include an array of keyPaths _in the same order_.
    - If you only search by one keyPath when you've specified an array of strings, you'll get undefined _even if_ that keyPath exists

# Cursor:

```
var open = window.indexedDB.open('deathstar2');

open.onsuccess = function(event) {
	var db = event.target.result;
	var transaction = db.transaction("stormtroopers", "readonly");
    var objectStore = transaction.objectStore("stormtroopers");
    var request = objectStore.openCursor();
    request.onsuccess = function(event) {
        var cursor = event.target.result;
        if(cursor) {
            console.log(cursor);
            // cursor.value contains the current record being iterated through
            // this is where you'd do something with the result
            cursor.continue();
        } else {
            // no more results
            console.log('we are done');
        }
    };
}
```

# Cursor search for specific value:

```
var open = window.indexedDB.open('deathstar2');
var uniqueTrooper;

open.onsuccess = function(event) {
	var db = event.target.result;
	var transaction = db.transaction("stormtroopers", "readonly");
    var objectStore = transaction.objectStore("stormtroopers");
    var request = objectStore.openCursor();
    request.onsuccess = function(event) {
        var cursor = event.target.result;
        if(cursor) {
			
            console.log(cursor);
			if(cursor.value.landingStripAccess == true) {
				arr.push(cursor.value);
            }
            // cursor.value contains the current record being iterated through
            // this is where you'd do something with the result
            cursor.continue();
        } else {
            // no more results
        }
		
    };
}
```