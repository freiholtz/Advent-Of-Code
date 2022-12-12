# Advent-Of-Code
A coding Christmas calendar 🎄🎅🏼🌟  https://adventofcode.com/

## 2022

---

### [Day 1: Calorie Counting](https://adventofcode.com/2022/day/1)

```python

# get the data
with open('1.txt') as f:
    data = f.read()
elfs = data.split("""

""")

most_calories = sorted([sum(map(int, elf.splitlines())) for elf in elfs])

print(most_calories[-1])
print(sum(most_calories[-3:]))

```

---

### [Day 2: Rock Paper Scissors](https://adventofcode.com/2022/day/1)

```python

# get the data
with open('2.txt') as f:
    data = f.read()
rounds = [round.split(" ") for round in  data.splitlines()]

first = {'A' : 'Rock', 'B' : 'Paper', 'C' : 'Scissors'}
second = {'X' : 'Rock', 'Y' : 'Paper', 'Z' : 'Scissors'}


win = {
    'Rock': {'Rock': 0, 'Paper': -1, 'Scissors': 1},
    'Paper': {'Rock': 1, 'Paper': 0, 'Scissors': -1},
    'Scissors': {'Rock': -1, 'Paper': 1, 'Scissors': 0}
}


score = {'Rock': 1, 'Paper': 2, 'Scissors': 3, '-1': 0, '0': 3, '1': 6}

# Part 1

total = 0
for round in rounds:
    opponent = first[round[0]] 
    you = second[round[1]]
    total += score[you] +  score[str(win[you][opponent])]

print(total)

# Part 2

second_2 = {'X' : 'Lose', 'Y' : 'Draw', 'Z' : 'Win'}

win_2 = {
    'Lose': {'Rock': 'Scissors', 'Paper': 'Rock', 'Scissors': 'Paper', 'Score': 0},
    'Draw': {'Rock': 'Rock', 'Paper': 'Paper', 'Scissors': 'Scissors', 'Score': 3},
    'Win': {'Rock': 'Paper', 'Paper': 'Scissors', 'Scissors': 'Rock', 'Score': 6}
}

total = 0
for round in rounds:
    opponent = first[round[0]] 
    you = second_2[round[1]]
    you_draw = win_2[you][opponent]
    total += score[you_draw] +  win_2[you]['Score']

print(total)

```

---

### [Day 3: Rucksack Reorganization](https://adventofcode.com/2022/day/3)

```python

# get the data
with open('3.txt') as f:
    data = f.read()
rows = data.splitlines()


def c_value(c):
    if ord(c) <= ord('a'):
        return ord(c) - ord('A') + 27
    else:
        return ord(c) - ord('a') + 1

# Part 1

priority_sum = 0
for row in rows:
    dublets = {}
    comp_size = int(len(row)/2)
    comp_1 = row[0:comp_size]
    comp_2 = row[comp_size:]


    for c in comp_1:
        if c in comp_2:
            if not c in dublets:
                dublets[c] = c_value(c)
    priority_sum += sum(dublets.values())

print(priority_sum)

# Part 2

# chunk the data into 3 rows
groups = [rows[i:i+3] for i in range(0, len(rows), 3)]

badges = []
for group in groups:
    badges += set(group[0]).intersection(*group)

badges_sum = sum(map(c_value, badges))

print(badges_sum)

```

---

