#Реализовать  скрипт,  который  решает  квадратное  уравнение  вида 𝑎𝑥ଶ+𝑏𝑥+𝑐=0. D = b2 − 4ac.
#Параметры квадратного уравнения 𝑎, 𝑏, 𝑐 задаются вводом или через аргументы командной строки.


import math
import sys


def main():
    a = validate_param(('please input "a": '))
    b = validate_param(('please input "b": '))
    c = validate_param(('please input "c": '))
    d = discriminant(a, b, c)
    roots(d, a, b, c)
    square_print(a, b, c, roots(d, a, b, c))

def validate_param(x):
    for i in range (1,4):
        try:
            x = int(input(x))
            return x
        except Exception:
            print("Invalid number, please check the number and try again")
    sys.exit("unable to proceed with invalid number")

def discriminant(a, b, c):
    d = b**2-4*a*c
    print(d)
    return d

def roots(d, a, b, c):
    if d == 0:
        r1 = (-b - math.sqrt(d)) / (2 * a)
        return r1
    elif d>0:
        r1 = (-b - math.sqrt(d)) / (2 * a)
        r2 = (-b + math.sqrt(d)) / (2 * a)
        return round(r1),round(r1)
    else:
        return "no roots available"

def solv_square(a, b, c) -> roots:
    d = discriminant(a, b, c)
    return roots(d, a, b, c)

def square_print(a, b, c, roots):
    print(f"for {a}x*x+{b}x+{c}=0  x={roots}")


if __name__ == "__main__":
    main()
    
    
import unittest
from solv_square_equation import discriminant, roots, solv_square

a = 2
b = 8
c = 1
d = 56
A = -4
B = -567
C = 34
D = 322033
aa = 8
bb = 24
cc = -675
dd = 22176

class MyTestCase(unittest.TestCase):

    def test_discriminant(self):
        self.assertEqual(discriminant(a, b, c), 56)  # add assertion here
        self.assertEqual(discriminant(A, B, C), 322033)
        self.assertEqual(discriminant(aa, bb, cc), 22176)

    def test_roots(self):
        self.assertEqual(roots(d, a, b, c), (-4,-4))
        self.assertEqual(roots(D, A, B, C), (0, 0))
        self.assertEqual(roots(dd, aa, bb, cc), (-11, -11))

    def test_solv_square(self):
        self.assertEqual(solv_square(a, b, c), (-4,-4))
        self.assertEqual(solv_square(A, B, C), (0, 0))
        self.assertEqual(solv_square(aa, bb, cc), (-11, -11))

if __name__ == '__main__':
    unittest.main()
