SUID (Simple Unique Identifier)
====
Simple Unique Identifier, influenced by [ObjectId](http://api.mongodb.org/java/2.0/org/bson/types/ObjectId.html), is a lightweight [GUID](http://en.wikipedia.org/wiki/Globally_unique_identifier)/[UUID](http://en.wikipedia.org/wiki/Universally_unique_identifier) implementation. 

### Spec:


```
    timestamp + increment + instanceId
    +-----------+--------------+------------+
    | 63...32   | 31...8       | 7...0      |
    +-----------+--------------+------------+
    | timestamp | increment    | instanceId |
    +-----------+--------------+------------+

```


### Exmaple:

```
	System.out.println("\n--- get id");
	System.out.println(toStringLong(id()));
	System.out.println(toStringLong(id()));

	System.out.println("\n--- get id by app id");
	System.out.println(toStringLong(id(13)));
	System.out.println(toStringLong(id(13)));

	System.out.println("\n--- duplication test ...");
	long id = 0, ts = System.currentTimeMillis();
	Set<Long> set = new HashSet<Long>();
	for (int i = 0; i < 1000000; i++) {
		id = id(i & 1);
		if (!set.add(id))
			System.out.println("!!!!!! duplication found:" + toStringLong(id));
	}
	System.out.println("--- duplication test passed, cost " + (System.currentTimeMillis() - ts) + "ms");
```
