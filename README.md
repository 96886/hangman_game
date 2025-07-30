import random

def hangman():
    words = ['python', 'hangman', 'challenge', 'programming', 'openai']
    word = random.choice(words)
    word_letters = set(word)        # unique letters in the word to guess
    guessed_letters = set()         # letters guessed by the player
    attempts = 6                   # number of wrong attempts allowed

    print("Welcome to Hangman!")
    print(f"The word has {len(word)} letters.")

    # Game loop
    while attempts > 0 and word_letters:
        # Display the current guessed state
        display_word = [letter if letter in guessed_letters else '_' for letter in word]
        print('Word:', ' '.join(display_word))
        print(f"Attempts left: {attempts}")
        guess = input("Guess a letter: ").lower()

        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single alphabetical letter.\n")
            continue

        if guess in guessed_letters:
            print("You already guessed that letter. Try again.\n")
            continue

        if guess in word_letters:
            word_letters.remove(guess)
            guessed_letters.add(guess)
            print("Good guess!\n")
        else:
            attempts -= 1
            guessed_letters.add(guess)
            print("Wrong guess.\n")

    if not word_letters:
        print(f"Congratulations! You guessed the word: {word}")
    else:
        print(f"Sorry, you ran out of attempts. The word was: {word}")

# Run the game
hangman()
