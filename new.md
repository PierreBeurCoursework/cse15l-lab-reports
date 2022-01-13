```py
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
