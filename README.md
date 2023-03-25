## STRING DATA TYPE

SET

Bir string değeri belirtilen anahtarın değeri olarak ayarlar:


```csharp

> SET mykey "hello"
OK

```
GET

Bir string değeri belirtilen anahtarın değerini döndürür:



```csharp
> GET mykey
"hello"

```
APPEND
Bir string değerine belirtilen değeri ekler:


```csharp
> APPEND mykey " world"
12
> GET mykey
"hello world"
```

INCR
Bir sayısal değeri belirtilen anahtarın değerini 1 artırır:


```csharp
> SET counter 1
OK
> INCR counter
2
> INCR counter
3

```
DECR
Bir sayısal değeri belirtilen anahtarın değerini 1 azaltır:


```csharp
> SET counter 3
OK
> DECR counter
2
> DECR counter
1

```
INCRBY
Bir sayısal değeri belirtilen anahtarın değerini belirtilen miktarda artırır:


```csharp
> SET counter 1
OK
> INCRBY counter 5
6
```

DECRBY
Bir sayısal değeri belirtilen anahtarın değerini belirtilen miktarda azaltır:

```csharp

> SET counter 10
OK
> DECRBY counter 3
7

```
GETRANGE
Bir string değerinin belirtilen aralığını döndürür:

```csharp
> SET mykey "This is a string"
OK
> GETRANGE mykey 0 3
"This"
> GETRANGE mykey -6 -1
"string"
```

SETRANGE
Bir string değerinin belirtilen aralığını belirtilen değerle değiştirir:


```csharp
> SET mykey "Hello World"
OK
> SETRANGE mykey 6 "Redis"
OK
> GET mykey
"Hello Redis"
```

STRLEN
Bir string değerinin uzunluğunu döndürür:

```csharp

> SET mykey "Hello World"
OK
> STRLEN mykey
11
```

MGET
Birden fazla anahtarın değerlerini döndürür:


```csharp
> SET key1 "value1"
OK
> SET key2 "value2"
OK
> MGET key1 key2
1) "value1"
2) "value2"
```

MSET
Birden fazla anahtarın değerlerini belirtilen değerlere ayarlar:


```csharp
> MSET key1 "value1" key2 "value2"
OK
> GET key1
"value1"
> GET key2
"value2"

```

APPEND
Bir string değerine belirtilen değeri ekler:

```csharp

> APPEND mykey " world"
12
> GET mykey
"Hello Redis world"
```

SETEX
Bir string değerini belirtilen süre boyunca ayarlar:

```csharp
> SETEX mykey 10 "hello"
OK
> GET mykey
"hello"
> TTL mykey
(integer) 
```

## SET  DATA TYPE

SADD: Bir Set içine bir veya birden fazla eleman ekler. Eğer eleman zaten Set içinde varsa eklenmez.


```csharp
 SADD myset "hello"
1
> SADD myset "world"
1
> SADD myset "hello" "goodbye"
1
> SMEMBERS myset
1) "hello"
2) "world"
2) "goodbye"

```
SREM: Bir Set içindeki bir veya birden fazla elemanı siler. Eğer eleman Set içinde yoksa hiçbir şey yapmaz.

```csharp
> SADD myset "hello" "world" "goodbye"
3
> SREM myset "goodbye" "hello"
2
> SMEMBERS myset
1) "world"
```

SISMEMBER: Bir elemanın Set içinde olup olmadığını kontrol eder. Var ise 1, yoksa 0 döndürür.
```csharp
> SADD myset "hello" "world"
2
> SISMEMBER myset "hello"
1
> SISMEMBER myset "goodbye"
0
```

SCARD: Bir Set'in eleman sayısını döndürür.

```csharp
> SADD myset "hello" "world"
2
> SCARD myset
2

```
SINTER: Birden fazla Set arasındaki kesişim kümesini döndürür.

```csharp

> SADD set1 "a" "b" "c"
3
> SADD set2 "c" "d" "e"
3
> SADD set3 "a" "c" "e"
3
> SINTER set1 set2 set3
1) "c"

```

SUNION: Birden fazla Set arasındaki birleşim kümesini döndürür.


```csharp
> SADD set1 "a" "b" "c"
3
> SADD set2 "c" "d" "e"
3
> SADD set3 "a" "c" "e"
3
> SUNION set1 set2 set3
1) "a"
2) "b"
3) "c"
4) "d"
5) "e"
```

SDIFF: İlk Set'te olan ancak diğer Set'lerde olmayan elemanların fark kümesini döndürür.

```c
> SADD set1 "a" "b" "c"
3
> SADD set2 "c" "d" "e"
3
> SADD set3 "a" "c" "e"
3
> SDIFF set1 set2 set3
1) "b"

```
SMEMBERS: Bir Set'in tüm elemanlarını döndürür.

```csharp
> SADD myset "hello" "world"
2
> SMEMBERS myset
1) "hello"
2) "world"
```

## LIST DATA TYPE

LPUSH

Bir liste başına bir veya daha fazla eleman ekler:


```csharp
> LPUSH mylist "world"
1
> LPUSH mylist "hello"
2
> LRANGE mylist 0 -1
1) "hello"
2) "world"
```

RPUSH
Bir liste sonuna bir veya daha fazla eleman ekler:

```csharp

> RPUSH mylist "hello"
1
> RPUSH mylist "world"
2
> LRANGE mylist 0 -1
1) "hello"
2) "world"
```


LPOP
Bir listenin başındaki elemanı siler ve döndürür:


```csharp
> LPUSH mylist "world"
1
> LPUSH mylist "hello"
2
> LPOP mylist
"hello"
> LRANGE mylist 0 -1
1) "world"
```


RPOP
Bir listenin sonundaki elemanı siler ve döndürür:

```csharp

> RPUSH mylist "hello"
1
> RPUSH mylist "world"
2
> RPOP mylist
"world"
> LRANGE mylist 0 -1
1) "hello"
```


LLEN
Bir listenin eleman sayısını döndürür:


```csharp
> LPUSH mylist "world"
1
> LPUSH mylist "hello"
2
> LLEN mylist
2
```

LRANGE
Bir listenin belirtilen aralığındaki elemanları döndürür:


```csharp
> RPUSH mylist "one"
1
> RPUSH mylist "two"
2
> RPUSH mylist "three"
3
> LRANGE mylist 0 1
1) "one"
2) "two"
```


LINDEX
Bir listenin belirtilen indeksindeki elemanı döndürür:

```csharp

> RPUSH mylist "one"
1
> RPUSH mylist "two"
2
> RPUSH mylist "three"
3
> LINDEX mylist 0
"one"
> LINDEX mylist 1
"two"
```


LSET
Bir listenin belirtilen indeksindeki elemanı belirtilen değerle değiştirir:


```csharp
> RPUSH mylist "one"
1
> RPUSH mylist "two"
2
> RPUSH mylist "three"
3
> LSET mylist 0 "four"
OK
> LRANGE mylist 0 -1
1) "four"
2) "two"
3) "three"
```


LREM
Bir listeden belirtilen değere sahip tüm elemanları siler:

```csharp

> RPUSH mylist "hello"
1
> RPUSH mylist "world"
2
> RPUSH mylist "hello"
3
> LREM mylist -2 "hello"
2
> LRANGE mylist 0 -1
1) "hello"
2) "world"
```


LTRIM
Bir listenin belirtilen aralığındaki elemanları keser:


```csharp
> RPUSH mylist "one"
1
> RPUSH mylist "two"
2
> RPUSH mylist "three"
3
> LTRIM
```

## HASH DATA TYPE


HSET
Bir hash içinde belirtilen alan(ad) ve değeri ekler:


```csharp
> HSET myhash field1 "foo"
1
> HSET myhash field2 "bar"
1
> HGET myhash field1
"foo"
> HGET myhash field2
"bar"
```

HMSET
Bir hash içinde birden çok alan ve değer ekler:


```csharp
> HMSET myhash field1 "hello" field2 "world"
OK
> HGET myhash field1
"hello"
> HGET myhash field2
"world"
```


HGET
Bir hash içinde belirtilen alanın değerini döndürür:


```csharp
> HSET myhash field1 "foo"
1
> HGET myhash field1
"foo"
```

HDEL
Bir hash içinde belirtilen alanı siler:

```csharp

> HMSET myhash field1 "hello" field2 "world"
OK
> HDEL myhash field1
1
> HGET myhash field1
(nil)
```


HEXISTS
Bir hash içinde belirtilen alanın var olup olmadığını kontrol eder:


```csharp
> HSET myhash field1 "foo"
1
> HEXISTS myhash field1
1
> HEXISTS myhash field2
0

```
HGETALL
Bir hash içindeki tüm alanları ve değerlerini döndürür:


```csharp
> HMSET myhash field1 "hello" field2 "world"
OK
> HGETALL myhash
1) "field1"
2) "hello"
3) "field2"
4) "world"
```

HINCRBY
Bir hash içindeki belirtilen alanın değerini belirtilen miktarda arttırır:


```csharp
> HSET myhash mykey 10
1
> HINCRBY myhash mykey 5
15
```


HKEYS
Bir hash içindeki tüm alan(ad)ları döndürür:


```csharp
> HSET myhash field1 "foo"
1
> HSET myhash field2 "bar"
1
> HGET myhash field1
"foo"
> HGET myhash field2
"bar"

```
HVALS
Bir hash içindeki tüm değerleri döndürür:


```csharp
> HMSET myhash field1 "hello" field2 "world"
OK
> HVALS myhash
1) "hello"
2) "world"
```


## SORTED SET DATA TYPE

ZADD
Bir Sorted Set içinde belirtilen skor(score) ve değeri ekler:


```csharp
> ZADD myset 1 "one"
1
> ZADD myset 2 "two"
1
> ZADD myset 3 "three"
1
> ZRANGE myset 0 -1 WITHSCORES
1) "one"
2) "1"
3) "two"
4) "2"
5) "three"
6) "3"
```

ZRANGE
Bir Sorted Set içinde belirtilen indeks aralığındaki değerleri döndürür:


```csharp
> ZADD myset 1 "one"
1
> ZADD myset 2 "two"
1
> ZADD myset 3 "three"
1
> ZRANGE myset 0 -1
1) "one"
2) "two"
3) "three"
```


ZRANK
Bir Sorted Set içinde belirtilen elemanın sıralama indeksini döndürür:

```csharp

> ZADD myset 1 "one"
1
> ZADD myset 2 "two"
1
> ZADD myset 3 "three"
1
> ZRANK myset "two"
1

```
ZREM
Bir Sorted Set içinde belirtilen elemanı siler:


```csharp
> ZADD myset 1 "one"
1
> ZADD myset 2 "two"
1
> ZADD myset 3 "three"
1
> ZREM myset "two"
1
> ZRANGE myset 0 -1
1) "one"
2) "three"
```

ZSCORE
Bir Sorted Set içinde belirtilen elemanın skorunu döndürür:


```csharp
> ZADD myset 1 "one"
1
> ZADD myset 2 "two"
1
> ZADD myset 3 "three"
1
> ZSCORE myset "two"
2
```

ZCOUNT
Bir Sorted Set içinde belirtilen skor aralığındaki eleman sayısını döndürür:



```csharp
> ZADD myset 1 "one"
1
> ZADD myset 2 "two"
1
> ZADD myset 3 "three"
1
> ZCOUNT myset 1 2
2

```

ZINCRBY
Bir Sorted Set içinde belirtilen elemanın skorunu belirtilen miktarda arttırır:


```csharp
> ZADD myset 1 "one"
1
> ZADD myset 2 "two"
1
> ZADD myset 3 "three"
1
> ZINCRBY myset 2 "one"
3
> ZSCORE myset "one"
3
```

ZCARD
Bir Sorted Set içindeki eleman sayısını döndürür:


```csharp
> ZADD myset 1 "one"
1
> ZADD myset 2 "two"
1
> ZADD myset 3 "three"
1
> ZCARD myset
3
```

ZREVRANGE
Bir Sorted Set içinde belirtilen indeks aralığındaki elemanları tersten sıralayarak döndürür:

```csharp

> ZADD myset 1 "one"
1
> ZADD myset 2 "two"
1
> ZADD myset 3 "three"
1
> ZREVRANGE myset 0 -1
1) "three"
2) "two"
3) "one"
```


ZREVRANGEBYSCORE
Bir Sorted Set içinde belirtilen skor aralığındaki elemanları tersten sıralayarak döndürür:


```csharp
> ZADD myset 1 "one"
1
> ZADD myset 2 "two"
1
> ZADD myset 3 "three"
1
> ZREVRANGEBYSCORE myset 3 1
1) "three"
2) "two"
3) "one"
```

ZINTERSTORE
Birden fazla Sorted Set arasındaki kesişimi yeni bir Sorted Set olarak oluşturur:

```csharp

> ZADD myset1 1 "one"
1
> ZADD myset1 2 "two"
1
> ZADD myset2 2 "two"
1
> ZADD myset2 3 "three"
1
> ZINTERSTORE myset3 2 myset1 myset2 WEIGHTS 2 3
1
> ZRANGE myset3 0 -1 WITHSCORES
1) "two"
2) "8"
```


ZUNIONSTORE
Birden fazla Sorted Set arasındaki birleşimi yeni bir Sorted Set olarak oluşturur:

```csharp

> ZADD myset1 1 "one"
1
> ZADD myset1 2 "two"
1
> ZADD myset2 2 "two"
1
> ZADD myset2 3 "three"
1
> ZUNIONSTORE myset3 2 myset1 myset2 WEIGHTS 2 3
1
> ZRANGE myset3 0 -1 WITHSCORES
1) "one"
2) "2"
3) "three"
4) "9"
5) "two"
6) "10"
```





