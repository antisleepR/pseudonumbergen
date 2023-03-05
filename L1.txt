import random
import tkinter as tk
from tkinter import messagebox

class NumberGenerator:
    def __init__(self, master):
        self.master = master
        master.title("Генератор псевдовипадкового числа")

        # Кількість символів
        self.label1 = tk.Label(master, text="Кількість символів:", bg='white')
        self.label1.place(relx=0.5, rely=0.3, anchor='center')

        self.entry1 = tk.Entry(master)
        self.entry1.place(relx=0.5, rely=0.35, anchor='center')

        # Мінімальне значення
        self.label2 = tk.Label(master, text="Цифри від:", bg='white')
        self.label2.place(relx=0.5, rely=0.4, anchor='center')

        self.entry2 = tk.Entry(master)
        self.entry2.place(relx=0.5, rely=0.45, anchor='center')

        # Максимальне значення
        self.label3 = tk.Label(master, text="Цифри до:", bg='white')
        self.label3.place(relx=0.5, rely=0.5, anchor='center')

        self.entry3 = tk.Entry(master)
        self.entry3.place(relx=0.5, rely=0.55, anchor='center')

        # Кнопка "Згенерувати"
        self.button = tk.Button(master, text="Згенерувати", command=self.generate_random_number, bg='white')
        self.button.place(relx=0.5, rely=0.65, anchor='center')

    def generate_random_number(self):
        try:
            num_digits = int(self.entry1.get())
            min_digit = int(self.entry2.get())
            max_digit = int(self.entry3.get())
        except ValueError:
            messagebox.showerror("Помилка", "Будь ласка, введіть коректні дані.")
            return

        if min_digit > max_digit:
            messagebox.showerror("Помилка", "Мінімальне значення не може бути більше максимального.")
            return

        if num_digits <= 0:
            messagebox.showerror("Помилка", "Кількість символів повинна бути більше нуля.")
            return

        random_number = ""
        for i in range(num_digits):
            random_number += str(random.randint(min_digit, max_digit))

        messagebox.showinfo("Результат", f"Псевдовипадкове число: {random_number}")

root = tk.Tk()
my_gui = NumberGenerator(root)
root.mainloop()