import tkinter as tk
from tkinter import ttk, messagebox
from translate import Translator

def translate_text():
    try:
        source_text = input_text.get("1.0", tk.END).strip()
        if not source_text:
            messagebox.showwarning("Input Error", "Please enter text to translate.")
            return
        
        src_lang_code = src_lang.get()
        dest_lang_code = dest_lang.get()

        translator = Translator(from_lang=src_lang_code, to_lang=dest_lang_code)
        translated = translator.translate(source_text)
        output_text.delete("1.0", tk.END)
        output_text.insert(tk.END, translated)
    except Exception as e:
        messagebox.showerror("Translation Error", str(e))

# Initialize the main window
root = tk.Tk()
root.title("Language Translation Tool")
root.geometry("400x300")

# Create and place widgets
tk.Label(root, text="Input Text:").pack(pady=5)
input_text = tk.Text(root, height=5, width=50)
input_text.pack(pady=5)

tk.Label(root, text="Source Language Code:").pack(pady=5)
src_lang = ttk.Combobox(root, values=["auto", "en", "ge", "fr", "hi", "si", "ur"])
src_lang.pack(pady=5)
src_lang.set("auto")

tk.Label(root, text="Destination Language Code:").pack(pady=5)
dest_lang = ttk.Combobox(root, values=["en", "hi", "fr", "pa", "ar", "ur"])
dest_lang.pack(pady=5)
dest_lang.set("en")

translate_button = tk.Button(root, text="Translate", command=translate_text)
translate_button.pack(pady=10)

tk.Label(root, text="Translated Text:").pack(pady=5)
output_text = tk.Text(root, height=5, width=50)
output_text.pack(pady=5)

# Start the main event loop
root.mainloop()

