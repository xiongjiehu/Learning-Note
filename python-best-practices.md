# Python Best Practices

1. Guess number game

```python
# -*- coding: utf-8 -*-
"""
author: xiongjiehu@qq.com
date: 2024/03/18

"""

import random

def guessNumber():
    """Guess a int number in (100,999)"""
    initialNumber = random.randint(100,999)
    judgeSwitch = True

    while judgeSwitch:
        print("Please enter your guess three-digit int number :")
        inputNumber = int(input())

        if inputNumber > initialNumber:
            print("Your number is too big!")
        elif inputNumber == initialNumber:
            print("Your number is right!")
            return 0
        else:
            print("Your number is too small!")

if __name__ == "__main__":
    guessNumber()
```

2. FizzBuzz

````python
# -*- coding: utf-8 -*-
"""
author: xiongjiehu@qq.com
date: 2024/03/18

"""

def FizzBuzz():
    """[1,100], 3 Fizz, 5 Buzz, 15 FizzBuzz"""
    initNumber = 1
    while initNumber < 101:
        if initNumber % 15 == 0:
            print("FizzBuzz")
            initNumber += 1
            continue
        elif initNumber % 3 == 0:
            print("Fizz")
            initNumber += 1
            continue
        elif initNumber % 5 == 0:
            print("Buzz")
            initNumber += 1
            continue
        else:
            print(initNumber)
            initNumber += 1
    return 0

if __name__ == "__main__":
    FizzBuzz()
```
````

3. AIagent Guess Number

```python
# -*- coding: utf-8 -*-
"""
author: xiongjiehu@qq.com
date: 2024/03/18

"""

import random

def AIagentGuessNumber():
    """ input int X is in [0,9] """
    MIN = 0
    MAX = 10
    count = 1
    #current = (MIN + MAX) // 2
    current = random.randrange(0,9)
    print("Please enter the int number in [0,9]:")
    guessNumber = int(input())
    while current != guessNumber:
        if current > guessNumber:
            MAX = current
            current = (MIN + MAX) // 2
            count += 1
        else:
            MIN = current
            current = (MIN + MAX) // 2
            count += 1
    
    print(f"Guess number is {current}")
    print(f"Guess count is {count}")
    return 0

if __name__ == "__main__":
    AIagentGuessNumber()
```

