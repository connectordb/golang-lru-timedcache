# golang-lru-timedcache
Simple wrapper for golang-lru which allows time based expiration of keys.

The cache is indexed by both an key and an id.

```go

//Cache of size 20,000 with expiration set to 60,000ms (1 min)
tc, err := NewTimedCache(20000, 60000, nil)

keyid := 5
tc.Set("stringkey",keyid, "value")

//v is "value"
v, ok := tc.GetByName("stringkey")
v, ok = tc.GetByID(5)

//Removing can be done by ID or by name - removing by one automatically
//removes the other, so no need to call both
tc.RemoveID(5)
tc.RemoveName("stringkey")

//Since there is both an id and an index, we can set a value only knowing
//its id (or update only knowing id)
tc.SetID(3,"secondvalue")

//To change a value by ID without changing associated string key, use Update
tc.Update(3,"thirdvalue")

//Clears the cache
tc.Purge()
```
