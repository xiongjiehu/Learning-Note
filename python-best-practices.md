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