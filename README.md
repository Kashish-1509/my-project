import random

# Snakes and Ladders: key = start, value = end
snakes = {
    16: 6,
    48: 26,
    49: 11,
    56: 53,
    62: 19,
    64: 60,
    87: 24,
    93: 73,
    95: 75,
    98: 78
}

ladders = {
    1: 38,
    4: 14,
    9: 31,
    21: 42,
    28: 84,
    36: 44,
    51: 67,
    71: 91,
    80: 100
}

# Player positions
positions = {
    "Player 1": 0,
    "Player 2": 0
}

def roll_dice():
    return random.randint(1, 6)

def move_player(player):
    input(f"{player}, press Enter to roll the dice...")
    dice = roll_dice()
    print(f"{player} rolled a {dice}")

    new_position = positions[player] + dice
    if new_position > 100:
        print(f"{player} needs exactly {100 - positions[player]} to win. Try again next turn.")
        return

    print(f"{player} moves from {positions[player]} to {new_position}")
    positions[player] = new_position

    # Check for snakes or ladders
    if positions[player] in snakes:
        print(f"Oops! {player} got bitten by a snake! Goes down from {positions[player]} to {snakes[positions[player]]}")
        positions[player] = snakes[positions[player]]
    elif positions[player] in ladders:
        print(f"Yay! {player} climbed a ladder! Goes up from {positions[player]} to {ladders[positions[player]]}")
        positions[player] = ladders[positions[player]]

def has_won(player):
    return positions[player] == 100

def play_game():
    print("Welcome to Snake and Ladder Game!")
    print("First player to reach position 100 wins!\n")

    turn = 0
    while True:
        current_player = "Player 1" if turn % 2 == 0 else "Player 2"
        move_player(current_player)

        if has_won(current_player):
            print(f"\n🎉 Congratulations! {current_player} wins the game! 🎉")
            break

        print(f"{current_player} is now at position {positions[current_player]}\n")
        turn += 1

# Start the game
if __name__ == "__main__":
    play_game()
