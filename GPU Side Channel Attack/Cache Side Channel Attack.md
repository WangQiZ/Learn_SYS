# Flush + Reload Attack
## requirements
1. Share identical read-only memory pages
2. flush instruction
##
1. Attacker flushes a cached memory location
2. Victim accesses/does not access
3. Attacker re-accesses memory location
<br>
Attacker could select the set to occupy -> no flush instruction

# Prime + Probe Attack
No shared memory pages
<br>
occupy all the set and test time

##
One example: Attacker could retrieve information from Montgomery ladder RSA by using the list method

# countermeasure
1. Design Cache Leakage Free Code
2. Page coloring
3. Cache Allocation tech 
4. Behavior detection

# MIT6.858
之前Side Channel被认为不存在于threat model -- 很难实现
<br>
在cypto implementations可能会存在side channel
<br>
private key的任何bit都不能泄漏
<br>
直到Spectre出来，才真正意识到这个问题

## Spectre
Spectre breaks isolation

1. application 不应该 read/refer kernel的memory
2. through timing channel, attacker can read secret
3. 在cache line中泄漏一些indirect information

Side Channel attack work 的原因：
1. shared cache
2. speculaive execution

```
if (off < size) {

}
如果size不在cache line，processor需要等待读取再执行下一步，但是为了效率，speculative execution会猜测执行。当size从mem读到，如果miss prediction，processor会回溯--将CPU state恢复，但是例如L3 caches不能真正回滚。
```

```
char secret[10];
if (off < sz) {
    v = array1[off];
    v1 = array2[v];
}
1. size不在cache
2. 训练branch predictor进入branch，与offset无关
3. control off -> pick large value -> array1[off] 和secret位置相同

v得到secret的值，用来索引arrya2。array1 cached， array2 not。array2[v]将会从mem读入保存cache。之后sz读入，猜测错误，但是cache仍包含array2[v]，然后访问array2[0-255 ]，根据时间判断。
```

### Challenges
1. array2需要在不同cache line 否则无法从访问时间上区分
2. train brancg predictor
3. evict size
4. evict array2
5. read array2
6. find gadgets in the kernel
7. noise

### real world?

Project zero
