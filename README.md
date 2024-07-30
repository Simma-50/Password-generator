# Password-generator
A password generator is a tool or program designed to create strong, random passwords to enhance security. These passwords typically include a combination of letters (uppercase and lowercase), numbers, and special characters, making them difficult to guess or crack. Password generators can be configured to meet specific requirements, such as minimum length and the inclusion of specific character types, to suit various security needs. They are commonly used to improve the security of online accounts, databases, and other systems requiring secure access credentials.


import random
import string
def generate_password(min_length, numbers=True, special_characters=True):
    letters = string.ascii_letters
    digits = string.digits
    special = string.punctuation
    characters = letters

    if numbers:
        characters += digits
    if special_characters:
        characters += special

    pwd = ""
    meets_criteria = False
    has_numbers = False
    has_special = False

    while not meets_criteria or len(pwd) < min_length:
        new_char = random.choice(characters)
        pwd += new_char

        if new_char in digits:
            has_numbers = True
        elif new_char in special:
            has_special = True

        meets_criteria = True
        if numbers:
            meets_criteria = meets_criteria and has_numbers
        if special_characters:
            meets_criteria = meets_criteria and has_special

    return pwd

try:
    min_length = int(input("Enter the minimum length: "))
    has_number = input("Do you want to have numbers (y/n): ").lower() == "y"
    has_special = input("Do you want to have special characters (y/n): ").lower() == "y"
    pwd = generate_password(min_length, has_number, has_special)
    print("The generated password is:", pwd)
except ValueError:
    print("Invalid input. Please enter a valid number for the minimum length.")
