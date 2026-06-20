# PRAKTIKUM-KOMNUM-KEL-11

### PRAKTIKUM 1 (PPT 2)
<img width="812" height="306" alt="image" src="https://github.com/user-attachments/assets/4e713a00-f6dc-48c1-b652-de0edd5300b5" />

- Kode Program
```
import numpy as np
import matplotlib.pyplot as plt

def regula_falsi_method(func, a, b, tol=1e-5, max_iter=100):
    if func(a) * func(b) >= 0:
        print("Error: f(a) dan f(b) harus beda tanda")
        return None

    print(f"{'Iterasi':<10} | {'a':<10} | {'b':<10} | {'c (akar)':<10} | {'f(c)':<15}")
    print("-" * 65)

    for i in range(1, max_iter + 1):
        fa = func(a)
        fb = func(b)

        c = (a * fb - b * fa) / (fb - fa)
        fc = func(c)

        print(f"{i:<10} | {a:<10.5f} | {b:<10.5f} | {c:<10.5f} | {fc:<15.5f}")

        if abs(fc) < tol:
            print("-" * 65)
            print(f"Akar ditemukan pada x = {c:.5f} setelah {i} iterasi.")
            return c

        if fa * fc < 0:
            b = c
        else:
            a = c

    return c

    def plot_function(func, a, b, root):
    x_vals = np.linspace(a - 1, b + 1, 400)
    y_vals = func(x_vals)

    plt.plot(x_vals, y_vals, label='f(x)')
    plt.axhline(0, linestyle='--')

    if root:
        plt.plot(root, func(root), 'ro', label=f'Akar (x={root:.4f})')

    plt.title("Grafik Metode Regula Falsi")
    plt.legend()
    plt.grid()
    plt.show()

    def f(x):
    return np.exp(-x) - x

    a = 0
    b = 1

    akar = regula_falsi_method(f, a, b)

    if akar:
    plot_function(f, a, b, akar)
```

- Output
<img width="728" height="282" alt="image" src="https://github.com/user-attachments/assets/ee267278-f45e-42fe-adf5-bf8cabbb5fc7" />

- Grafik Fungsi
<img width="640" height="480" alt="WhatsApp Image 2026-04-29 at 16 12 21" src="https://github.com/user-attachments/assets/dcca1b6c-3314-4a6b-af80-8f7f0b5dd5f4" />







### TUGAS PRAKTIKUM #1 (PPT 3)
<img width="815" height="320" alt="image" src="https://github.com/user-attachments/assets/466a71f3-5716-4b5b-8ea3-c4fddd46a9e7" />

- Kode Program
  ```
  import sympy as sp

    def cetak_header():
    print("=" * 65)
    print("       PRAKTIKUM KOMNUM: METODE SECANT PENCARI AKAR       ")
    print("=" * 65)
    print("Cara penulisan fungsi:")
    print(" - Pangkat      : gunakan ** (contoh: x**3)")
    print(" - Eksponensial : gunakan exp(x)")
    print(" - Trigonometri : gunakan sin(x), cos(x)")
    print("-" * 65)

    def metode_secant(str_fungsi, x_min1, x_i, toleransi, maks_iter=100):
    x = sp.Symbol('x')
    
    try:
        ekspresi = sp.sympify(str_fungsi)
        f = sp.lambdify(x, ekspresi, 'math')
    except Exception as e:
        print(f"\n[!] ERROR: Fungsi tidak valid. Detail: {e}")
        return

    print("\n[+] Memulai proses iterasi...")
    print("-" * 80)
    print(f"{'Iterasi':<8} | {'x_i':<15} | {'f(x_i)':<15} | {'Error Relatif (%)':<15}")
    print("-" * 80)

    for i in range(1, maks_iter + 1):
        f_x_min1 = f(x_min1)
        f_x_i = f(x_i)

        if f_x_i - f_x_min1 == 0:
            print("\n[!] Komputasi dihentikan: Pembagian dengan nol terdeteksi.")
            break

        x_baru = x_i - (f_x_i * (x_min1 - x_i)) / (f_x_min1 - f_x_i)
        
        if x_baru != 0:
            error = abs((x_baru - x_i) / x_baru) * 100
        else:
            error = 0

        print(f"{i:<8} | {x_baru:<15.6f} | {f(x_baru):<15.6f} | {error:<15.6f}")

        if error < toleransi:
            print("-" * 80)
            print(f"\n[★] SUKSES! Akar ditemukan pada iterasi ke-{i}")
            print(f"    Nilai Akar     : {x_baru:.8f}")
            print(f"    Error Relatif  : {error:.8f} %")
            return

        x_min1 = x_i
        x_i = x_baru

    print("-" * 80)
    print(f"\n[-] Batas maksimum iterasi ({maks_iter}) tercapai tanpa konvergensi sempurna.")
    print(f"    Taksiran terakhir: {x_i:.8f}")

    if __name__ == "__main__":
    cetak_header()
    
    try:
        input_fungsi = input("[?] Masukkan fungsi f(x) (contoh: exp(-x) - x): ")
        input_x_min1 = float(input("[?] Masukkan tebakan awal 1 (x_i-1)         : "))
        input_x_i    = float(input("[?] Masukkan tebakan awal 2 (x_i)           : "))
        input_tol    = float(input("[?] Masukkan toleransi error (%) (cth: 0.01): "))
        
        metode_secant(input_fungsi, input_x_min1, input_x_i, input_tol)
    except ValueError:
        print("\n[!] ERROR: Input tebakan/toleransi harus berupa angka!")
  ```

  - Output
  <img width="829" height="595" alt="WhatsApp Image 2026-04-30 at 00 59 31" src="https://github.com/user-attachments/assets/1f35bde3-d410-4452-998a-f78a6afde85b" />



  ### TUGAS PRAKTIKUM #3 (PPT 6)
<img width="837" height="465" alt="image" src="https://github.com/user-attachments/assets/d51dda11-64a3-4db9-845c-02fe4a972573" />

- Kode Program
```
import math
    import ipywidgets as widgets
    from IPython.display import display, clear_output
    import matplotlib.pyplot as plt
    import numpy as np
```



```
# ================================
# Fungsi evaluasi
# ================================
def f(x, expr):
    fungsi = {
        "x": x,
        "sin": math.sin,
        "cos": math.cos,
        "tan": math.tan,
        "sqrt": math.sqrt,
        "log": math.log,
        "exp": math.exp,
        "pi": math.pi,
        "e": math.e
    }
    return eval(expr, {"__builtins__": None}, fungsi)

# ================================
# Metode Trapesium
# ================================
def trapezoid(expr, a, b, n):
    h = (b - a) / n
    total = f(a, expr) + f(b, expr)

    for i in range(1, n):
        total += 2 * f(a + i*h, expr)

    return total * h / 2

# ================================
# Metode Romberg
# ================================
def romberg(expr, a, b, level):
    R = [[0]*level for _ in range(level)]

    for i in range(level):
        n = 2**i
        R[i][0] = trapezoid(expr, a, b, n)

    for i in range(1, level):
        for j in range(1, i+1):
            R[i][j] = R[i][j-1] + \
                (R[i][j-1]-R[i-1][j-1])/(4**j-1)

    return R

# ================================
# Grafik
# ================================
def tampilkan_grafik(expr, a, b):

    x = np.linspace(a, b, 400)
    y = [f(i, expr) for i in x]

    plt.figure(figsize=(6,4))
    plt.plot(x, y, label='f(x)')
    plt.axhline(0,color='black')
    plt.grid(True)
    plt.legend()
    plt.title("Grafik Fungsi")
    plt.show()

# ================================
# Widget
# ================================
fungsi = widgets.Text(
    value='sin(x)',
    description='f(x):'
)

bawah = widgets.FloatText(
    value=0,
    description='a:'
)

atas = widgets.FloatText(
    value=3.1415926535,
    description='b:'
)

level = widgets.IntText(
    value=5,
    description='Level:'
)

tombol = widgets.Button(
    description="Hitung",
    button_style="success"
)

output = widgets.Output()

# ================================
# Tombol Hitung
# ================================
def klik(b):

    with output:
        clear_output()

        try:

            hasil = romberg(
                fungsi.value,
                bawah.value,
                atas.value,
                level.value
            )

            print("========== TABEL ROMBERG ==========\n")

            for i in range(level.value):
                for j in range(i+1):
                    print(f"{hasil[i][j]:12.8f}", end=" ")
                print()

            print("\n===================================")
            print("Hasil Integral =", hasil[level.value-1][level.value-1])

            tampilkan_grafik(
                fungsi.value,
                bawah.value,
                atas.value
            )

        except Exception as e:
            print("Error :", e)

tombol.on_click(klik)

display(fungsi)
display(bawah)
display(atas)
display(level)
display(tombol)
display(output)
```


- Input
<img width="570" height="212" alt="image" src="https://github.com/user-attachments/assets/9c30e0af-25a9-4135-a0f7-427b10628e91" />

  - Output
 <img width="727" height="672" alt="image" src="https://github.com/user-attachments/assets/7ccf02b9-c226-4e34-88d6-4d8e50c94de5" />


  

 
