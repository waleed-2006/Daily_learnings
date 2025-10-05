**write  a program to find the roots of a quadratic equation**

import cmath
a, b, c = map(float, input("Enter a, b, c: ").split())
d = cmath.sqrt(b**2 - 4*a*c)
print(f"Roots: {(-b + d)/(2*a)}, {(-b - d)/(2*a)}")


**Write a program to accept a number ‘n’ and a. Check if ’n’ is prime b. Generate all prime numbers till ‘n’ c. Generate first ‘n’ prime numbers This program may be done using functions**

def is_prime(n):
    return n > 1 and all(n % i for i in range(2, int(n**0.5) + 1))
def primes_till_n(n):
    return [i for i in range(2, n+1) if is_prime(i)]
def first_n_primes(n):
    primes, num = [], 2
    while len(primes) < n:
        if is_prime(num): primes.append(num)
        num += 1
    return primes
n = int(input("Enter n: "))
print("a. Prime?", is_prime(n))
print("b. Primes till n:", primes_till_n(n))
print("c. First n primes:", first_n_primes(n))


**Write a program to create a pyramid of the character ‘*’ and a reverse pyramid**
def pyramid(n):
    for i in range(1, n + 1):
        print(' ' * (n - i) + '* ' * i)
def reverse_pyramid(n):
    for i in range(n, 0, -1):
        print(' ' * (n - i) + '* ' * i)  
rows = int(input("Enter number of rows: "))
print("\nPyramid:")
pyramid(rows)
print("\nReverse Pyramid:")
reverse_pyramid(rows)


**. Write a program that accepts a character and performs the following: 
a. print whether the character is a letter or numeric digit or a special character.  
b. if the character is a letter, print whether the letter is uppercase or lowercase 
c. if the character is a numeric digit, prints its name in text (e.g., if input is 9, output is 
NINE**

def digit_to_text(d):
    names = ["ZERO", "ONE", "TWO", "THREE", "FOUR", 
             "FIVE", "SIX", "SEVEN", "EIGHT", "NINE"]
    return names[int(d)]
ch = input("Enter a single character: ")
if ch.isalpha():
    print("It is a letter.")
    if ch.isupper():
        print("It is uppercase.")
    else:
        print("It is lowercase.")
elif ch.isdigit():
    print("It is a numeric digit.")
    print("Digit in words:", digit_to_text(ch))
else:
    print("It is a special character.")


**Write a program to perform the following operations on a string  
a. Find the frequency of a character in a string.  
b. Replace a character by another character in a string.  
c. Remove the first occurrence of a character from a string.  
d. Remove all occurrences of a character from a string.**

#Input string
text = input("Enter a string: ")

#a. Frequency of a character
ch = input("\na. Enter character to find frequency: ")
print(f"Frequency of '{ch}' is: {text.count(ch)}")

#b. Replace character
old = input("\nb. Enter character to replace: ")
new = input("Enter new character: ")
replaced = text.replace(old, new)
print("String after replacement:", replaced)

#c. Remove first occurrence
rem = input("\nc. Enter character to remove (first occurrence): ")
first_removed = text.replace(rem, "", 1)
print("After removing first occurrence:", first_removed)

#d. Remove all occurrences
rem_all = input("\nd. Enter character to remove (all occurrences): ")
all_removed = text.replace(rem_all, "")
print("After removing all occurrences:", all_removed)


**Write a program to swap the first n characters of two strings.**
#Input
s1 = input("Enter first string: ")
s2 = input("Enter second string: ")
n = int(input("Enter number of characters to swap: "))

#Check if n is valid
if n > len(s1) or n > len(s2):
    print("Error: n is larger than one of the strings.")
else:
    # Swap the first n characters
    new_s1 = s2[:n] + s1[n:]
    new_s2 = s1[:n] + s2[n:]

    # Output
    print("\nAfter swapping first", n, "characters:")
    print("String 1:", new_s1)
    print("String 2:", new_s2)

  **Write a function that accepts two strings and returns the indices of all the occurrences of the 
second string in the first string as a list. If the second string is not present in the first string then 
it should return -1.**
def find_all_occurrences(text, pattern):
    indices = []
    start = 0

    while True:
        pos = text.find(pattern, start)
        if pos == -1:
            break
        indices.append(pos)
        start = pos + 1  # Continue searching after this position

    return indices if indices else -1


#Example usage:
text = input("Enter the text: ")
pattern = input("Enter the pattern to search: ")

result = find_all_occurrences(text, pattern)
print("Occurrences at indices:", result)

**Write a program to create a list of the cubes of only the even integers appearing in the input 
list (may have elements of other types also) using the following: 
a. 'for' loop  
b. list comprehension**
#Input list with mixed types
input_list = [1, 2, 'a', 4.5, 6, 3, 8, 'hello', 10]

#a. Using for loop
cubes_for = []
for item in input_list:
    if isinstance(item, int) and item % 2 == 0:
        cubes_for.append(item ** 3)

print("Cubes using for loop:", cubes_for)

#b. Using list comprehension
cubes_lc = [x ** 3 for x in input_list if isinstance(x, int) and x % 2 == 0]

print("Cubes using list comprehension:", cubes_lc)

**Write a program to read a file and  
a. Print the total number of characters, words and lines in the file.  
b. Calculate the frequency of each character in the file. Use a variable of dictionary type 
to maintain the count.  
c. Print the words in reverse order.  
d. Copy even lines of the file to a file named ‘File1’ and odd lines to another file named 
‘File2’.**
def process_file(fname):
    with open(fname) as f:
        lines = f.readlines()

    chars = sum(len(line) for line in lines)
    words = sum(len(line.split()) for line in lines)
    print(f"Characters: {chars}, Words: {words}, Lines: {len(lines)}")

    freq = {}
    for line in lines:
        for ch in line:
            freq[ch] = freq.get(ch, 0) + 1

    all_words = [w for line in lines for w in line.split()]
    print("\nWords in reverse order:")
    print(' '.join(all_words[::-1]))

    with open('File1', 'w') as f1, open('File2', 'w') as f2:
        for i, line in enumerate(lines, 1):
            (f1 if i % 2 == 0 else f2).write(line)

    print("\nCharacter frequencies:")
    for ch, count in sorted(freq.items()):
        print(f"'{ch if ch != '\\n' else '\\\\n'}': {count}")


filename = input("Enter filename: ")
try:
    process_file(filename)
except FileNotFoundError:
    print("File not found.")

**Write a program to define a class Point with coordinates x and y as attributes. Create 
relevant methods and print the objects. Also define a method distance to calculate the distance 
between any two point objects.**

import math

class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __str__(self):
        return f"Point({self.x}, {self.y})"
    def distance(self, other):
        return math.sqrt((self.x - other.x)**2 + (self.y - other.y)**2)

**Write a function that prints a dictionary where the keys are numbers between 1 and 5 and 
the values are cubes of the keys.**
def print_cubes():
    cubes = {i: i**3 for i in range(1, 6)}
    print(cubes)
print_cubes()


**Consider a tuple t1=(1, 2, 5, 7, 9, 2, 4, 6, 8, 10). Write a program to perform following 
operations:  
a. Print half the values of the tuple in one line and the other half in the next line.  
b. Print another tuple whose values are even numbers in the given tuple.  
c. Concatenate a tuple t2=(11,13,15) with t1.  
d. Return maximum and minimum value from this tuple**


#Given tuple
t1 = (1, 2, 5, 7, 9, 2, 4, 6, 8, 10)

#a. Print half the values in one line, other half in next line
mid = len(t1) // 2
print("First half:", t1[:mid])
print("Second half:", t1[mid:])

#b. Print another tuple with only even numbers
even_tuple = tuple(x for x in t1 if x % 2 == 0)
print("Even numbers tuple:", even_tuple)

#c. Concatenate t1 with t2
t2 = (11, 13, 15)
concatenated_tuple = t1 + t2
print("Concatenated tuple:", concatenated_tuple)

#d. Return maximum and minimum values
max_value = max(t1)
min_value = min(t1)
print("Maximum value:", max_value)
print("Minimum value:", min_value)

**WAP to accept a name from a user. Raise and handle appropriate exception(s) if the text entered 
by the user contains digits and/or special characters.**
# Function to accept valid name
def get_name():
    try:
        name = input("Enter your name: ")
        if not name.isalpha():
            # Raise exception if name contains digits or special characters
            raise ValueError("Name should only contain letters!")
        print("Valid name entered:", name)
    except ValueError as ve:
        print("Error:", ve)

get_name()







