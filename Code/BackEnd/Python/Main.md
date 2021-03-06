# Python

## Notes

### 数据结构
- dict
通过dict提供的get()方法，如果key不存在，可以返回None，或者自己指定的value：
```python
d = {'Jack':0}
>>>d.get('Thomas')
None
>>>d.get('Thomas', -1)
-1
```

### 迭代器

- 遍历迭代器时不能在内部再次调用迭代器
```python
a = (x for x in range(10))
b = (x for x in range(10))
for x in a:
    print(a.__next__())
    print(b.__next__())

# 结果 a 和 b 不同
```

### 内置函数

- python3 filter返回 filter 对象,需要用list()转换

### 多线程

- ai程序可以用多线程也可以用socket

### BUG
- 栈溢出
```python
# 递归层数太多
import sys
sys.setrecursionlimit(1000000)
```


### 代码

- 经过深度思考的代码
```python
def award_generator(self):
    award_pot = {}
    for player in self.game.players:
        award_pot[player.id] = self.get_player_total_chips(player)
    while True in [chips > 0 for chips in award_pot.values()]:
        yield self.award_assigner(award_pot)

# generator
def award_assigner(self,award_pot):
    max_chips = 0
    next_max_chips = 0
    for player in self.game.players:
        if award_pot[player.id] > max_chips:
            max_chips = award_pot[player.id]

    for player in self.game.players:
        if award_pot[player.id] < max_chips and award_pot[player.id] > next_max_chips:
            next_max_chips = award_pot[player.id]

    participants = []
    award_chips = 0
    for player in self.game.players:
        if self.get_player_total_chips(player) == max_chips:
            participants.append(player)
            award_pot[player.id] = next_max_chips
            award_chips += max_chips - next_max_chips

    return participants,award_chips
```

