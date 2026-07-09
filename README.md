# stackslib

A simple Python implementation of the UNO card game.

## Installation

```bash
git clone https://github.com/workonfire/stackslib.git
cd stackslib
python -m pip install -e .
```

## Multiplayer server

Start a local multiplayer server:

```bash
stackslib-server
```

Server options:

```bash
stackslib-server --host 127.0.0.1 --port 8765 --starting-cards 7
```

Use `--disable-card-stacking` to start rooms with card stacking disabled.

## API Preview
These are just **examples**.
- Inspecting a card
```python
card = Card(CardType.CARD_6, CardColor.BLUE)
other_card = Card.from_str('7 RED')
if card.playable(other_card):
    print("This card is playable with the other card.")
```

- Generating a deck
```python
deck = Deck(size=50)
cards: list[Card] = deck.draw(15)
```

- Inspecting a player
```python
player = Player('wzium')
if player.is_computer:
    print("The player is a computer.")
if len(player.hand) == 0:
    print("The player does not have any card.")
```

- Working with the table
```python
players: list[Player] = [Player('Wzium'), Player('Computer')]
# Custom rules (W.I.P.)
rules: dict[str, Any] = {'starting_cards': 7,
                         'cheats': False,
                         'card_stacking': True}

table = Table(players, rules)
table.play(table.turn.hand[0], table.turn) # Gets the user to play the first card 
print(table.last_played_card) # Get the last player card
table.deal_card(table.next_turn, 5) # Gives 5 cards to the player in next turn
```

- Operating with the game
```python
game = Game(players, rules)
while game.active:
    if game.get_winner() is not None:
        game.win(game.get_winner())
```

- Handling a turn
```python
turn = Turn(table)
print(turn.playable_cards) # gets all currently playable cards
print(turn.most_reasonable_color) # selects the appriopriate color based on how many times it appears
print(turn.get_result()) # Prints a card to play with
```
