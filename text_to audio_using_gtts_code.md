import tkinter as tk
from tkinter import filedialog, messagebox
from gtts import gTTS
import os

def convert_and_save():
    text = text_input.get("1.0", tk.END).strip()
    if not text:
        messagebox.showwarning("Warning", "Please enter some text.")
        return

    # Ask where to save the file
    file_path = filedialog.asksaveasfilename(
        defaultextension=".mp3",
        filetypes=[("MP3 files", "*.mp3")],
        title="Save speech as..."
    )

    if not file_path:
        return  # User cancelled

    try:
        tts = gTTS(text=text, lang='en')
        tts.save(file_path)
        messagebox.showinfo("Success", f"Speech saved successfully:\n{file_path}")
    except Exception as e:
        messagebox.showerror("Error", f"An error occurred:\n{e}")

# GUI setup
root = tk.Tk()
root.title("Text to Speech Converter")
root.geometry("500x300")
root.config(bg="#fefefe")

label = tk.Label(root, text="Enter your text:", font=("Arial", 12), bg="#fefefe")
label.pack(pady=10)

text_input = tk.Text(root, height=8, width=55, font=("Arial", 11))
text_input.pack(pady=5)

convert_button = tk.Button(root, text="Convert and Save as MP3", font=("Arial", 12),
                           bg="#007ACC", fg="white", command=convert_and_save)
convert_button.pack(pady=20)

root.mainloop()
