# Performance Information for Minecraft Commands

| Command                                                              | Time     |
| :------------------------------------------------------------------- | :------- |
| `/scoreboard players (add \| remove) ...`                            | 130 ns   |
| `/scoreboard players operation ...`                                  | 180 ns   |
| `/function ...`                                                      | 50 ns    |
| `/data modify storage ... set value ...`                             | 410 ns*  |
| `/execute store result score ... run data get storage ...`           | 500 ns   |
| `/execute store result storage ... run scoreboard players get ...`   | 500 ns   |
| `/data modify storage ... append value`                              | 220 ns   |
| `/execute if score ...`                                              | 230 ns   |
| `$...`                                                               | 1700+ ns |
| `/setblock`                                                          | 1200 ns  |

> *Depends on the nesting level of the NBT path. Time taken will approximately increase by 40 ns per level.

## Optimal Decision Tree Parameters

**Optimal branches:**

$$
o = e^{W\left(\frac{\frac{a}{2} + b}{b \cdot e}\right) + 1}
$$

**Average time taken:**

$$
t = \left(\frac{a}{2} \cdot (o + 1) + b\right) \cdot \log(o, n) + c - b
$$

**Where:**
- $a$ = time taken for each comparison
- $b$ = time taken for each function call
- $c$ = time taken for each terminal operation
- $n$ = number of terminal elements
- $W$ = Lambert W function
