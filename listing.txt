import tkinter as tk
import random
import pyperclip

class RandomNumberGenerator(tk.Frame):
    def __init__(self, master=None):
        super().__init__(master)
        self.master = master
        self.master.title("Генератор псевдовипадкових чисел")

        self.create_widgets()

    def create_widgets(self):
        # Number of digits label and entry
        self.digits_label = tk.Label(self.master, text="Кількість символів:")
        self.digits_label.grid(row=0, column=0, sticky="W")

        self.digits_entry = tk.Entry(self.master)
        self.digits_entry.grid(row=0, column=1, sticky="W")

        # Range of digits label and entry (from)
        self.range_from_label = tk.Label(self.master, text="Цифри від:")
        self.range_from_label.grid(row=1, column=0, sticky="W")

        self.range_from_entry = tk.Entry(self.master)
        self.range_from_entry.grid(row=1, column=1, sticky="W")

        # Range of digits label and entry (to)
        self.range_to_label = tk.Label(self.master, text="Цифри до:")
        self.range_to_label.grid(row=2, column=0, sticky="W")

        self.range_to_entry = tk.Entry(self.master)
        self.range_to_entry.grid(row=2, column=1, sticky="W")

        # Generate button
        self.generate_button = tk.Button(self.master, text="Згенерувати", command=self.generate)
        self.generate_button.grid(row=3, column=0, sticky="W")

        # Clear button
        self.clear_button = tk.Button(self.master, text="Очистити", command=self.clear)
        self.clear_button.grid(row=3, column=1, sticky="W")

        # Result text
        self.result_text = tk.Text(self.master)
        self.result_text.grid(row=4, column=0, columnspan=2)

        # Scrollbar
        self.scrollbar = tk.Scrollbar(self.master)
        self.scrollbar.grid(row=4, column=2, sticky="NS")

        self.result_text.config(yscrollcommand=self.scrollbar.set)
        self.scrollbar.config(command=self.result_text.yview)

    def generate(self):
        # Get input values
        try:
            num_digits = int(self.digits_entry.get())
            range_from = int(self.range_from_entry.get())
            range_to = int(self.range_to_entry.get())
        except ValueError:
            self.result_text.insert(tk.END, "Invalid input\n")
            return

        # Validate input values
        if num_digits <= 0 or range_from >= range_to:
            self.result_text.insert(tk.END, "Invalid input\n")
            return

        # Generate random numbers
        numbers = []
        for i in range(num_digits):
            numbers.append(str(random.randint(range_from, range_to)))
        result = "".join(numbers)

        # Display result
        self.result_text.insert(tk.END, result + "\n")

    def clear(self):
        self.digits_entry.delete(0, tk.END)
        self.range_from_entry.delete(0, tk.END)
        self.range_to_entry.delete(0, tk.END)
        self.result_text.delete('1.0', tk.END)

root = tk.Tk()
app = RandomNumberGenerator(master=root)
app.mainloop()
