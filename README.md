import random

def generate_question(difficulty):
  """Generates a math question based on the specified difficulty level.

  Args:
      difficulty: An integer representing the difficulty level (1: easy, 2: medium, 3: hard).

  Returns:
      A tuple containing the question string and the correct answer.
  """

  operations = {
      1: "+",
      2: "-",
      3: "*",
  }

  num1 = random.randint(1, 100) if difficulty <= 2 else random.randint(100, 1000)
  num2 = random.randint(1, 100) if difficulty <= 2 else random.randint(100, 1000)
  operation = random.choice(list(operations.values()))

  if operation == "+" and (num1 + num2) > 1000:  # Prevent overflow for addition
    return generate_question(difficulty)

  question = f"{num1} {operation} {num2} = "
  answer = eval(question[:-2])  # Evaluate expression safely
  return question, answer

def play_game():
  """Plays a round of the math game."""

  difficulty = int(input("Choose difficulty level (1: easy, 2: medium, 3: hard): "))
  score = 0
  num_questions = 5

  for _ in range(num_questions):
    question, answer = generate_question(difficulty)
    user_answer = int(input(question))

    if user_answer == answer:
      score += 1
      print("Correct!")
    else:
      print(f"Incorrect. The answer is {answer}.")

  print(f"You scored {score} out of {num_questions} questions.")

if __name__ == "__main__":
  print("Welcome to the Math Game!")
  play_game()

  while True:
    play_again = input("Play again? (y/n): ").lower()
    if play_again != "y":
      break
    play_game()

  print("Thanks for playing!")
