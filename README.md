Puzzle 0:
A says, “I am both a knight and a knave.”
•	A cannot be both a knight and a knave (logical contradiction).
•	If A is a knight, their statement must be true, but the statement is inherently false.
•	Therefore, A must be a knave.
from logic import *

# Puzzle 0
knowledge0 = And(
    Or(AKnight, AKnave),           # A must be either a knight or a knave
    Not(And(AKnight, AKnave)),     # A cannot be both a knight and a knave
    Biconditional(AKnight, And(AKnight, AKnave))  # A's statement
)
Puzzle 1:
A says, “We are both knaves.”
B says nothing.
•	If A is a knight, their statement must be true, meaning both A and B are knaves. But if A is a knight, they cannot be a knave, leading to a contradiction.
•	Therefore, A must be a knave, making their statement false.
•	If A’s statement is false, it means not both A and B are knaves. Since A is a knave, B must be a knight.
Knowledge Base:
# Puzzle 1
knowledge1 = And(
    Or(AKnight, AKnave),           # A must be either a knight or a knave
    Or(BKnight, BKnave),           # B must be either a knight or a knave
    Not(And(AKnight, AKnave)),     # A cannot be both
    Not(And(BKnight, BKnave)),     # B cannot be both
    Biconditional(AKnight, And(AKnave, BKnave))  # A's statement
) Puzzle 2:
A says, “We are the same kind.”
B says, “We are of different kinds.”
•	If A is a knight, their statement is true, meaning A and B are the same kind.
•	If B is a knight, their statement is true, meaning A and B are different kinds.
•	These statements are contradictory, so one of them must be lying.
Knowledge Base:
# Puzzle 2
knowledge2 = And(
    Or(AKnight, AKnave),           # A must be either a knight or a knave
    Or(BKnight, BKnave),           # B must be either a knight or a knave
    Not(And(AKnight, AKnave)),     # A cannot be both
    Not(And(BKnight, BKnave)),     # B cannot be both
    Biconditional(AKnight, Biconditional(AKnight, BKnight)),  # A's statement
    Biconditional(BKnight, Not(Biconditional(AKnight, BKnight)))  # B's statement
)
Puzzle 3:
A says either “I am a knight.” or “I am a knave.” (you don’t know which).
B says, “A said ‘I am a knave.’” and “C is a knave.”
C says, “A is a knight.”
•	If A is a knight, their statement "I am a knight" is true.
•	If B is a knight, their statements must both be true, meaning A said "I am a knave" and C is a knave.
•	If C is a knight, their statement "A is a knight" must be true.
•	Use logical constraints to resolve conflicts.
Knowledge Base:
# Puzzle 3
knowledge3 = And(
    Or(AKnight, AKnave),           # A must be either a knight or a knave
    Or(BKnight, BKnave),           # B must be either a knight or a knave
    Or(CKnight, CKnave),           # C must be either a knight or a knave
    Not(And(AKnight, AKnave)),     # A cannot be both
    Not(And(BKnight, BKnave)),     # B cannot be both
    Not(And(CKnight, CKnave)),     # C cannot be both

    # A's statement (either "I am a knight" or "I am a knave")
    Biconditional(AKnight, AKnight),

    # B's statements
    Biconditional(BKnight, Biconditional(AKnight, AKnave)),  # B says A said "I am a knave"
    Biconditional(BKnight, CKnave),                         # B says C is a knave

    # C's statement
    Biconditional(CKnight, AKnight)  # C says A is a knight
)
