# Tugas-Program-Komnum-A05

|	NRP 	|  	Name  	|
| :--------: | :------------: |
| 5025241106 | Joaquin Fairuz Nawfal Ismono |
| 5025241107 | Muhammad Zahran Rizki Primanda |
| 5025241112 | Dafa Kumara Sahasika |
| 5025241114 | Hasan Abdurrahman |

# Nomor Soal: 21

**Langkah Pengerjaan Soal No. 21:**

1. Import fungsi-fungsi yang ada di library `numpy`, dan juga `sympy` untuk memanipulasi simbol-simbol polinomial dan aljabar.

```
import numpy as np
from sympy import *
```
2. Buat fungsi `factorisation_method` dengan parameter `f` dan `max_iter = 4` sesuai arahan soal.

```
def factorisation_method(f, max_iter=4):
```

3. Definisikan semua variabel untuk fungsi `x`, semua koefisien nya, dan inisialisasi `a0` sebagai `0`.

```
x = symbols('x')
a0 = 0.0
poly = Poly(f, x)
coeffs = poly.all_coeffs()
```

4. Melakukan proses iterasi untuk faktorisasi selama 4 kali dan tampilkan hasil dari `b0`, `a1`, dan `a0` untuk setiap iterasi.

```
print("Fungsi f(x) = ", f, "\n")
print("Faktorisasi orde 3:\n")

A = np.array(coeffs, dtype=float)

for i in range(max_iter):
    A0 = A[3]
    A1 = A[2]
    A2 = A[1]

    if a0 == 0:
        b0 = 0
    else:
        b0 = round(A0 / a0, 2)

    a1 = round(A2 - b0, 2)
    a0 = round(A1 - b0 * a1, 2)

    print(f"Iterasi ke-{i+1}:")
    print(f"  b0 = A0 / a0 = {A0} / {a0} = {b0:.2f}")
    print(f"  a1 = A2 - b0 = {A2} - {b0} = {a1:.2f}")
    print(f"  a0 = A1 - a1 * b0 = {A1} - {a1} * {b0} = {a0:.2f}\n")
```

5. Bulatkan hasil iterasi dan simpan sebagai `f(x) = (x + b0)(x^2 + a1x + a0)`
```
b0_res = round(b0)
a1_res = round(a1)
a0_res = round(a0)

factor1 = f"(x {'+' if b0_res > 0 else '-'} {abs(b0_res)})"

a1_sign = '+' if a1_res >= 0 else '-'
a0_sign = '+' if a0_res >= 0 else '-'
quadratic = f"(x^2 {a1_sign} {abs(a1_res)}x {a0_sign} {abs(a0_res)})"

print("Hasil Akhir :") 
print(f"f(x) = {factor1}{quadratic}")
```

6. Cari akar-akar dari persamaan tersebut
```
roots = np.roots([1, a1_res, a0_res])

x1 = -b0_res
x2 = round(roots[0])
x3 = round(roots[1])

def format_factor(x):
    return f"(x - {x})" if x >= 0 else f"(x + {abs(x)})"

factors = [x1, x2, x3]
factors_str = "".join([format_factor(x) for x in factors])

print(f"     = {factors_str}\n")
print(f"x1 = {x1}")
print(f"x2 = {x2}")
print(f"x3 = {x3}")
```

7. Terima inputan dari pengguna, lalu gunakan fungsi untuk menghitung hasil (untuk soal 21, ada di command `#Example Usage`)
```
f = input("Enter the function f(x) in terms of x: ")
f = sympify(f)

factorisation_method(f)
```
