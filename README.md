# pomodoro-timer
## Challenge: Build a pomodoro timer using tkinter library in Python
## Solutions
1. Reset timer
```
def reset_timer():
    window.after_cancel(timer)
    # timer_text 00:00
    canvas.itemconfig(timer_text, text="00:00")
    # title_label "Timer"
    title_label.config(text="Timer", fg=GREEN)
    # reset check_marks
    check_marks.config(text="")
    global reps
    reps = 0
```
2. Timer mechanism
```
def start_timer():
    global reps
    reps += 1
    work_sec = WORK_MIN * 60
    short_break_sec = SHORT_BREAK_MIN * 60
    long_break_sec = LONG_BREAK_MIN * 60

    # If it's the 8th rep
    if reps % 8 == 0:
        count_down(long_break_sec)
        title_label.config(text="Break", fg=RED)
    # If it's the 2nd/4th/6tth rep
    elif reps % 2 == 0:
        count_down(short_break_sec)
        title_label.config(text="Break", fg=PINK)
    # If it's the 1st/3rd/5th/7th rep (remember computers count from '0')
    else:
        count_down(work_sec)
        title_label.config(text="Work", fg=GREEN)
```
3. UI Setup
```
window = Tk()
window.title("Pomodoro")
window.config(padx=100, pady=50, bg=YELLOW)

# Labels
title_label = Label(text="Timer", bg=YELLOW, fg=GREEN, font=(FONT_NAME, 50, "bold"))
title_label.grid(row=0, column=1)

# Canvas for the image of pomodoro
canvas = Canvas(width=200, height=224, bg=YELLOW, highlightthickness=0)
tomato_img = PhotoImage(file="tomato.png")
canvas.create_image(100, 112, image=tomato_img)
timer_text = canvas.create_text(100, 130, text="00:00", fill="white", font=(FONT_NAME, 35, "bold"))
canvas.grid(row=1, column=1)

# Buttons
# calls start() when pressed
start_button = Button(text="Start", command=start_timer, highlightthickness=0)
start_button.grid(row=2, column=0)

# calls reset() when pressed
reset_button = Button(text="Reset", command=reset_timer, highlightthickness=0)
reset_button.grid(row=2, column=2)

# Checkmarks
check_marks = Label(bg=YELLOW, fg=GREEN, font=(FONT_NAME, 50, "bold"))
check_marks.grid(row=3, column=1)

window.mainloop()
```
