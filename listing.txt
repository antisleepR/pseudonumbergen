import random
import tkinter as tk
from tkinter import messagebox


class Application(tk.Frame):
    def __init__(self, master=None):
        super().__init__(master)
        self.master = master
        self.grid()
        self.create_widgets()

    def create_widgets(self):
        # Діапазон цифр
        self.range_label = tk.Label(self, text="Діапазон цифр:    від")
        self.range_label.grid(row=0, column=0)

        self.range_min = tk.Entry(self)
        self.range_min.grid(row=0, column=1)

        self.range_to_label = tk.Label(self, text="до")
        self.range_to_label.grid(row=0, column=2)

        self.range_max = tk.Entry(self)
        self.range_max.grid(row=0, column=3)

        # Кількість символів
        self.length_label = tk.Label(self, text="Кількість символів:")
        self.length_label.grid(row=1, column=0)

        self.length_entry = tk.Entry(self)
        self.length_entry.grid(row=1, column=1)

        # Кнопки
        self.generate_button = tk.Button(self, text="Згенерувати", command=self.generate)
        self.generate_button.grid(row=2, column=0)

        self.clear_button = tk.Button(self, text="Очистити", command=self.clear)
        self.clear_button.grid(row=2, column=1)

        # Результат
        self.result_label = tk.Label(self, text="")
        self.result_label.grid(row=3, column=0, columnspan=4)

    def generate(self):
        # Перевірка вхідних даних
        try:
            range_min = int(self.range_min.get())
            range_max = int(self.range_max.get())
            length = int(self.length_entry.get())
        except ValueError:
            messagebox.showerror("Помилка", "Введіть коректні дані")
            return

        # Перевірка діапазону цифр
        if range_min >= range_max:
            messagebox.showerror("Помилка", "Діапазон цифр введено некоректно")
            return

        # Генерація псевдовипадкового числа
        number = ""
        for i in range(length):
            number += str(random.randint(range_min, range_max))

        # Виведення результату
        self.result_label.configure(text=number)

    def clear(self):
        # Очищення полів вводу та результату
        self.range_min.delete(0, tk.END)
        self.range_max.delete(0, tk.END)
        self.length_entry.delete(0, tk.END)
        self.result_label.configure(text="")


# Створення вікна програми
root = tk.Tk()
root.title("Генератор псевдовипадкових чисел")

# Запуск програми
app = Application(master=root)
app.mainloop()