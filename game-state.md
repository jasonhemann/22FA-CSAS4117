# A Specification of Game States

Author: Jason & Hemann
Repo: Elephant 

## The Relevant Information 

A game state for the Fish game must record the following pieces of information:

- the state of the board, which is a composition of
  - hexagonal tiles with fish images on them plus
  - holes (where players may have been or where the referee decided holes would look "cool")
- knowledge about the external player
  - the player's assigned avatar
  - the locations of the player's penguins
  - the player's score, i.e., number of fish collected so far
- the order in which players take turns
- the phase of the game (xor):
  - the phase of placing penguins on boards
  - the phase of taking turns moving an owned penguin from one place to another.


## The Use Cases

A data representation of the state of the game is useful for both the
referee and the AI player.

A referee may use the state of the game to decide

- which player to call next,
- what action to execut on behalf of a player, 
- whose score to increase,
- how to change the order of turns.

An AI player may use the state

- to decide
  - where to place a penguin 
  - which of its penguins can move and where they can move to 
- to inspect the situation of other players
- to evaluate the potential of scoring.

## The External Interface

The interface of a game state must accommodate both referees and players.

A `state` combines data about the current state of the `board` (see
previous assignment) and knowledge about `internal players`.

An `internal player` combines data about the current `score` (a
natural number), the current `places` of penguins, the assigned
`avatar` (see previous assignment). The knowledge should include a
field that abstractly represents how to call the AI player. 


A `position` is a [row, column] combination; both are natural numbers.  

```
create-state
   ;; create an initial state for `n` players with a `rows` x `columns` board 
   ;; optionally with fixed # of fish
   ;; returns  state 

score-of
   ;; determine the score of the specifid player in this `state`


next-player
   ;; proceed in player order in this `state` 
   ;; returns state 

place-avatar
   ;; place a penguin for specified `player` at given `position` in this `state
   ;; returns state 

take-turn
   ;; execute a move from `old` to `new` on behalf of the first player in this `state`
   ;; players go to end of line
   ;; return state 
  
all-possible-actions 
   ;; list all possible actions that the first player in this `state` may take:
   ;; returns a list of potential player moves, a collection of pairs of `positions`

delete-player
   ;; terminate the specified player from this `state`
   ;; returns state 

render-state
   ;; render this state into a graphical context 
```


