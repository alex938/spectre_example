# SPECTRE EXAMPLE



# define some garbage data

```
data = [1, 2, 3]
```

# create a variable larger than the len of data, we'll use this trigger speculative execution

```
i = 10
```

# force speculative execution

```
if len(data) > i:
    password = data[i] # this is available in CPU cache now :-( important to note here, the CPU 'undoes' the operation but the value of data[10] i.e. password remains in CPU cache!
```

# guess the value of password using a time based attack

1. Create a reference array to compare with

```x = ['a', 'b', 'c', 'd', 'e', 'f'... 'z']```

2. Load first value into the CPU cache

```x[0]```

3. Now read value of x[password] 

```x[password]``` time this operation, for example it takes 1ms (severely over exaggerated)

# must flush cpu cache and start again!

4. Load second value into the CPU cache

```x[1]```

5. Now read value of x[password] 

```x[password]``` operation takes 1ms

# must flush cpu cache and start again!

6. Load second value into the CPU cache

```x[2]```

7. Now read value of x[password] 

```x[password]``` operation takes 0.2ms! the value was IN the CPU cache!

value in memory at x[password] is x[2]
