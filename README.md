

## SET 

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
