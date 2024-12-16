# Rock, Paper, Scissors Game 🎮

This is a simple GUI-based Rock, Paper, Scissors game built using Python and the Tkinter library.

## Features
- Play Rock, Paper, Scissors against the computer.
- Displays scores for user wins, computer wins, and draws.
- Option to reset scores or play again after a session.
- User-friendly GUI.

## Requirements
- Python 3.x
- Tkinter (comes pre-installed with Python)

## Code

from tkinter import *
import random

#Function for the game logic
def play_game(user_choice):
    global user_wins, computer_wins, draws

    computer_choice = random.choice(["Rock", "Paper", "Scissors"])
    computer_choice_label.config(text=f"Computer chose: {computer_choice}")

    if user_choice == computer_choice:
        result_label.config(text="It's a Draw!", fg="blue")
        draws += 1
    elif (user_choice == "Rock" and computer_choice == "Scissors") or \
         (user_choice == "Paper" and computer_choice == "Rock") or \
         (user_choice == "Scissors" and computer_choice == "Paper"):
        result_label.config(text="You Win!", fg="green")
        user_wins += 1
    else:
        result_label.config(text="Computer Wins!", fg="red")
        computer_wins += 1

    #Update score labels
    user_score_label.config(text=f"Your Wins: {user_wins}")
    computer_score_label.config(text=f"Computer Wins: {computer_wins}")
    draw_score_label.config(text=f"Draws: {draws}")

#Function to show results and declare final winner
def show_results():
    if user_wins > computer_wins:
        result_label.config(text="Congratulations!! You are the Winner!", fg="green")
    elif computer_wins > user_wins:
        result_label.config(text="Oops :(  Computer Rocks!", fg="red")
    else:
        result_label.config(text="Nice Try :) It's a Draw!", fg="blue")

    # Hide unnecessary labels
    computer_choice_label.pack_forget()
    user_score_label.pack_forget()
    computer_score_label.pack_forget()
    draw_score_label.pack_forget()

    # Hide main buttons and show Play Again/Quit
    rock_button.pack_forget()
    paper_button.pack_forget()
    scissors_button.pack_forget()
    results_button.pack_forget()
    reset_button.pack_forget()

    play_again_button.pack(pady=10)
    quit_button.pack(pady=10)

# Function to reset the game
def reset_game():
    global user_wins, computer_wins, draws
    user_wins = 0
    computer_wins = 0
    draws = 0
    result_label.config(text="")
    user_score_label.config(text="Your Wins: 0")
    computer_score_label.config(text="Computer Wins: 0")
    draw_score_label.config(text="Draws: 0")
    computer_choice_label.config(text="")

# Function to play again
def play_again():

    reset_game()

    # Hide Play Again and Quit buttons
    play_again_button.pack_forget()
    quit_button.pack_forget()

    # Show the main buttons and labels
    rock_button.pack(side=LEFT, padx=10)
    paper_button.pack(side=LEFT, padx=10)
    scissors_button.pack(side=LEFT, padx=10)

    computer_choice_label.pack(pady=10)
    user_score_label.pack()
    computer_score_label.pack()
    draw_score_label.pack()

    results_button.pack_forget()
    reset_button.pack_forget()
    results_button.pack(side=LEFT, padx=10)
    reset_button.pack(side=LEFT, padx=10)

#Initialize scores
user_wins = 0
computer_wins = 0
draws = 0

#main Tkinter window
root = Tk()
root.title("Rock, Paper, Scissors")
root.geometry("900x600")

#Title
Label(root, text="Rock, Paper & Scissors Game", font=("Arial", 20)).pack(pady=20)

# Buttons for user choices
button_frame = Frame(root)
button_frame.pack(pady=10)

rock_button = Button(button_frame, text="ROCK",fg="red", font=("Times new roman", 17,"bold"), command=lambda: play_game("Rock"),bg="lightblue", width=10)
rock_button.pack(side=LEFT, padx=10)
paper_button = Button(button_frame, text="PAPER",fg="red", font=("Times new roman", 17,"bold"), command=lambda: play_game("Paper"),bg="lightblue", width=10)
paper_button.pack(side=LEFT, padx=10)
scissors_button = Button(button_frame, text="SCISSORS",fg="red", font=("Times new roman", 17,"bold"), command=lambda: play_game("Scissors"),bg="lightblue", width=10)
scissors_button.pack(side=LEFT, padx=10)

# Display computer's choice
computer_choice_label = Label(root, text="", font=("Arial", 14))
computer_choice_label.pack(pady=10)

# Display result
result_label = Label(root, text="", font=("Arial", 18), fg="blue")
result_label.pack(pady=10)

# Display scores
user_score_label = Label(root, text="Your Wins: 0", font=("Arial", 14))
user_score_label.pack()
computer_score_label = Label(root, text="Computer Wins: 0", font=("Arial", 14))
computer_score_label.pack()
draw_score_label = Label(root, text="Draws: 0", font=("Arial", 14))
draw_score_label.pack()

# Results and Reset Buttons
control_frame = Frame(root)
control_frame.pack(pady=10)

results_button = Button(control_frame, text="Final Result", font=("Arial", 14), command=show_results, bg="lightgreen",width=10)
results_button.pack(side=LEFT, padx=13, pady=15)

reset_button = Button(control_frame, text="Reset", font=("Arial", 14), command=reset_game, bg="lightgray",width=10)
reset_button.pack(side=LEFT, padx=13, pady=15)

# Play Again and Quit Buttons
play_again_button = Button(root, text="Play Again!", font=("Arial", 14), command=play_again, bg="lightgreen",width=10)
quit_button = Button(root, text="Quit :(", font=("Arial", 14), command=root.quit, bg="lightcoral",width=10)

root.mainloop()

