from tkinter import *
import json
from tkinter import ttk, messagebox
from tkinter import Button
#function note
#window( window2(create note), windowStu(create study note), windowDia(create diary note)
#window( 
    #create function
#save button
#function to load notes

notes = {}
#load the notes from the library
try:
    with open("notes.json", "r") as f:
        notes = json.load(f)
except FileNotFoundError:
    pass
    
#create note table
def CreateNote():
    window2 = Toplevel() #secondary window
    window2.title("Create Note")
    window2.geometry("500x500")
    window2.configure(bg = "lightblue")
    labelCat = Label(window2, text = "select category")

#create category
    buttonStu =Button(window2, text = "study note",fg = "yellow", bg = "green", command = StudyNote) #create study note
    buttonDia =Button(window2, text = "diary note",fg = "yellow", bg = "green", command = CreateDiary) #create diary note
    buttonSmall =Button(window2, text = "create small note",fg = "yellow", bg = "green", command= small_note ) #create small note
    

#do pack create notes
    labelCat.pack()
    buttonStu.pack()
    buttonDia.pack()
    buttonSmall.pack()


#create study note page
#all the tab function(notebook) copy from here
def StudyNote():
    window_study = Toplevel()
    window_study.title("Study Notes")
    window_study.geometry("500x400")

    notebook = ttk.Notebook(window_study)
    notebook.pack(expand=True, fill="both")

    # Initial frame for a new study note
    frame = ttk.Frame(notebook)
    notebook.add(frame, text="New Study Note")

    Label(frame, text="Enter Title:").grid(row=0, column=0, sticky=W, padx=10, pady=5)
    title_entry = Text(frame, wrap="word", width=40, height=2, font=("Times New Roman", 12))
    title_entry.grid(row=0, column=1, padx=10, pady=5)

    Label(frame, text="Enter Notes:").grid(row=1, column=0, sticky=NW, padx=10, pady=5)
    note_box = Text(frame, wrap="word", width=30, height=10, font=("Times New Roman", 12))
    note_box.grid(row=1, column=1, padx=10, pady=5)

    Button(frame, text="Save", command=lambda: save_study_func(title_entry, note_box, notebook)).grid(
        row=2, column=1, sticky=E, pady=10
    )

    load_study_notes(notebook)

    # Add Note Button for Study Notes
    def add_study_note():
        new_tab = ttk.Frame(notebook)
        notebook.add(new_tab, text=f"Study Note {len(notebook.tabs())}")

        Label(new_tab, text="Enter Title:").grid(row=0, column=0, sticky=W, padx=10, pady=5)
        new_title = Text(new_tab, wrap="word", width=40, height=2, font=("Times New Roman", 12))
        new_title.grid(row=0, column=1, padx=10, pady=5)

        Label(new_tab, text="Enter Notes:").grid(row=1, column=0, sticky=NW, padx=10, pady=5)
        new_note = Text(new_tab, wrap="word", width=30, height=10, font=("Times New Roman", 12))
        new_note.grid(row=1, column=1, padx=10, pady=5)

        Button(new_tab, text="Save", command=lambda: save_study_func(new_title, new_note, notebook)).grid(
            row=2, column=1, sticky=E, pady=10
        )

    add_but = Button(window_study, text="Add Study Note", command=add_study_note)
    add_but.pack(pady=10)


def CreateDiary():
    window_diary = Toplevel()
    window_diary.title("Diary Notes")
    window_diary.geometry("500x400")

    notebook = ttk.Notebook(window_diary)
    notebook.pack(expand=True, fill="both")

    # Initial frame for a new diary note
    frame2 = ttk.Frame(notebook)
    notebook.add(frame2, text="New Diary Note")

    Label(frame2, text="Enter Title:").pack(pady=5)
    title_entry = Text(frame2, wrap="word", width=50, height=1, font=("Times New Roman", 12))
    title_entry.pack(pady=5)

    Label(frame2, text="Enter Notes:").pack(pady=5)
    note_box = Text(frame2, wrap="word", width=50, height=10, font=("Times New Roman", 12))
    note_box.pack(pady=5)

    Button(frame2, text="Save", command=lambda: save_diary_func(title_entry, note_box, notebook)).pack(pady=10)

    load_diary_notes(notebook)

    # Add Note Button for Diary Notes
    def add_diary_note():
        new_tab = ttk.Frame(notebook)
        notebook.add(new_tab, text=f"Diary Note {len(notebook.tabs())}")

        Label(new_tab, text="Enter Title:").pack(pady=5)
        new_title = Text(new_tab, wrap="word", width=50, height=1, font=("Times New Roman", 12))
        new_title.pack(pady=5)

        Label(new_tab, text="Enter Notes:").pack(pady=5)
        new_note = Text(new_tab, wrap="word", width=50, height=10, font=("Times New Roman", 12))
        new_note.pack(pady=5)

        Button(new_tab, text="Save", command=lambda: save_diary_func(new_title, new_note, notebook)).pack(pady=10)

    add_but = Button(window_diary, text="Add Diary Note", command=add_diary_note)
    add_but.pack(pady=10)


def small_note():
    window_small = Toplevel()
    window_small.title("Small Notes")
    window_small.geometry("600x400")

    notebook = ttk.Notebook(window_small)
    notebook.pack(expand=True, fill="both")

    # Initial frame for a new small note
    frame3 = ttk.Frame(notebook)
    notebook.add(frame3, text="New Small Note")

    Label(frame3, text="Enter Title:").pack(pady=5)
    title_entry = Text(frame3, wrap="word", width=50, height=1, font=("Times New Roman", 12))
    title_entry.pack(pady=5)

    Label(frame3, text="Enter Notes:").pack(pady=5)
    note_box = Text(frame3, wrap="word", width=50, height=10, font=("Times New Roman", 12))
    note_box.pack(pady=5)

    Button(frame3, text="Save", command=lambda: save_small_func(title_entry, note_box, notebook)).pack(pady=10)

    load_small_notes(notebook)

    # Add Note Button for Small Notes
    def add_small_note():
        new_tab = ttk.Frame(notebook)
        notebook.add(new_tab, text=f"Small Note {len(notebook.tabs())}")

        Label(new_tab, text="Enter Title:").pack(pady=5)
        new_title = Text(new_tab, wrap="word", width=50, height=1, font=("Times New Roman", 12))
        new_title.pack(pady=5)

        Label(new_tab, text="Enter Notes:").pack(pady=5)
        new_note = Text(new_tab, wrap="word", width=50, height=10, font=("Times New Roman", 12))
        new_note.pack(pady=5)

        Button(new_tab, text="Save", command=lambda: save_small_func(new_title, new_note, notebook)).pack(pady=10)

    add_but = Button(window_small, text="Add Small Note", command=add_small_note)
    add_but.pack(pady=10)



#save function
def save_study_func(title_entry, note_box, notebook):
    global notes

    title = title_entry.get("1.0", "end").strip()
    content = note_box.get("1.0", "end").strip()

    if not title or not content:
        messagebox.showwarning("Error", "Title and content cannot be empty!")
        return

    if title in notes:
        messagebox.showwarning("Duplicate Title", "A note with this title already exists!")
        return

    notes[title] = content

    try:
        with open("study_notes.json", "w") as f:
            json.dump(notes, f)
    except Exception as e:
        messagebox.showerror("Error", f"Failed to save notes: {e}")
        return

    new_tab = ttk.Frame(notebook)
    notebook.add(new_tab, text=title)

    notes_content = Text(new_tab, wrap="word", width=40, height=10, font=("Times New Roman", 12))
    notes_content.insert(END, content)
    notes_content.config(state="disabled")
    notes_content.pack(expand=True, fill="both")

    title_entry.delete("1.0", "end")
    note_box.delete("1.0", "end")
    title_entry.focus()

    messagebox.showinfo("Success", "Note saved successfully!")

def load_study_notes(notebook):
    global notes

    try:
        with open("study_notes.json", "r") as f:
            notes = json.load(f)
    except FileNotFoundError:
        print("No saved study notes found. Starting fresh.")
        return
    except Exception as e:
        messagebox.showerror("Error", f"Failed to load study notes: {e}")
        return

    for title, content in sorted(notes.items()):
        new_tab = ttk.Frame(notebook)
        notebook.add(new_tab, text=title)

        notes_content = Text(new_tab, wrap="word", width=40, height=10, font=("Times New Roman", 12))
        notes_content.insert(END, content)
        notes_content.config(state="disabled")
        notes_content.pack(expand=True, fill="both")


def save_diary_func(title_entry, note_box, notebook):
    global notes

    title = title_entry.get("1.0", "end").strip()
    content = note_box.get("1.0", "end").strip()

    if not title or not content:
        messagebox.showwarning("Error", "Title and content cannot be empty!")
        return

    if title in notes:
        messagebox.showwarning("Duplicate Title", "A note with this title already exists!")
        return

    notes[title] = content

    try:
        with open("diary_notes.json", "w") as f:
            json.dump(notes, f)
    except Exception as e:
        messagebox.showerror("Error", f"Failed to save notes: {e}")
        return

    new_tab = ttk.Frame(notebook)
    notebook.add(new_tab, text=title)

    notes_content = Text(new_tab, wrap="word", width=40, height=10, font=("Times New Roman", 12))
    notes_content.insert(END, content)
    notes_content.config(state="disabled")
    notes_content.pack(expand=True, fill="both")

    title_entry.delete("1.0", "end")
    note_box.delete("1.0", "end")
    title_entry.focus()

    messagebox.showinfo("Success", "Note saved successfully!")

def load_diary_notes(notebook):
    global notes

    try:
        with open("diary_notes.json", "r") as f:
            notes = json.load(f)
    except FileNotFoundError:
        print("No saved diary notes found. Starting fresh.")
        return
    except Exception as e:
        messagebox.showerror("Error", f"Failed to load diary notes: {e}")
        return

    for title, content in sorted(notes.items()):
        new_tab = ttk.Frame(notebook)
        notebook.add(new_tab, text=title)

        notes_content = Text(new_tab, wrap="word", width=40, height=10, font=("Times New Roman", 12))
        notes_content.insert(END, content)
        notes_content.config(state="disabled")
        notes_content.pack(expand=True, fill="both")


def save_small_func(title_entry, note_box, notebook):
    global notes

    title = title_entry.get("1.0", "end").strip()
    content = note_box.get("1.0", "end").strip()

    if not title or not content:
        messagebox.showwarning("Error", "Title and content cannot be empty!")
        return

    if title in notes:
        messagebox.showwarning("Duplicate Title", "A note with this title already exists!")
        return

    notes[title] = content

    try:
        with open("small_notes.json", "w") as f:
            json.dump(notes, f)
    except Exception as e:
        messagebox.showerror("Error", f"Failed to save notes: {e}")
        return

    new_tab = ttk.Frame(notebook)
    notebook.add(new_tab, text=title)

    notes_content = Text(new_tab, wrap="word", width=40, height=10, font=("Times New Roman", 12))
    notes_content.insert(END, content)
    notes_content.config(state="disabled")
    notes_content.pack(expand=True, fill="both")

    title_entry.delete("1.0", "end")
    note_box.delete("1.0", "end")
    title_entry.focus()

    messagebox.showinfo("Success", "Note saved successfully!")

def load_small_notes(notebook):
    global notes

    try:
        with open("small_notes.json", "r") as f:
            notes = json.load(f)
    except FileNotFoundError:
        print("No saved small notes found. Starting fresh.")
        return
    except Exception as e:
        messagebox.showerror("Error", f"Failed to load small notes: {e}")
        return

    for title, content in sorted(notes.items()):
        new_tab = ttk.Frame(notebook)
        notebook.add(new_tab, text=title)

        notes_content = Text(new_tab, wrap="word", width=40, height=10, font=("Times New Roman", 12))
        notes_content.insert(END, content)
        notes_content.config(state="disabled")
        notes_content.pack(expand=True, fill="both")

# Main GUI
window = Tk()
window.title("Hello Notes")
window.attributes("-fullscreen" , False
                  ) # modify size of main window
window.configure(bg = "lightblue")
icon = PhotoImage (file='C:\\Users\\Alvey\\OneDrive\\Desktop\\python\\note.png')
window.iconphoto(True,icon)


#design main GUI
#but = button
#lbl= label

#exit function 
def exitWin():
    window.destroy()

lbl1 = Label(window, text = "NOTACALB", font = ("Times New Roman", 30), width = 60, height = 2, fg = "black", bg = "yellow")
but_CreateNote = Button(window, text = "create notes",  fg = "white", bg = "green", width = 30 , height = 5,  command = CreateNote)
but_Exit = Button(window, text = "exit", width = 10, height = "1", pady = 5, command = exitWin)

#pack all
lbl1.pack(pady = 0)
but_CreateNote.pack(pady = 20)
but_Exit.pack(pady = 20)


#start vent loop which nanages all tkinter window
window.mainloop()
 
