text

*Italic*

**Bold**

~~Strikethrough~~

# Heading 1

text

## Heading 2

text

### Heading 3

text

---

[Week 2 Lab](https://ucsd-cse15l-w22.github.io/week/week2/)

![Jellyfish](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Jelly_cc11.jpg/640px-Jelly_cc11.jpg)

> Blockquote

* List 1
* List 2
* List 3

1. One
2. Two
3. Three

---

`python calculator` below

```python
import operator
ops = { '+' : operator.add, '-' : operator.sub, '*' : operator.mul,
        '/' : operator.truediv, '^' : operator.pow, '%' : operator.mod }

print('Welcome to this calculator!')
print('It can add, subtract, multiply, divide, exponentiate, and modulus 64 bit floats')
a = float(input('Please choose your first number: '))
op = input('What do you want to do? +, -, *, /, ^, %: ')
b = float(input('Please choose your second number: '))

print(f"{a}{op}{b} = {ops[op](a, b)}")

print("Thanks for using this calculator, goodbye :)")
```
