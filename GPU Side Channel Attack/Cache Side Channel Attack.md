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