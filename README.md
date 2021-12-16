# Exams
excercise 1:
import collections

n = int(input())
d = collections.OrderedDict()

for i in range(n):
    word = input()
    if word in d:
        d[word] += 1
    else:
        d[word] = 1

print(len(d))

for k, v in d.items():
    print(v, end="\n")

excercise 2:

def bigger_is_greater(w):
    array = list(w)
    T = len(array) - 1
    
    while T > 0 and array[T - 1] >= array[T]:
        T -= 1
    if T <= 0:
        return "No answer"
    
    i = len(array) - 1
    while array[i] <= array[T - 1]:
        i -= 1
        
        
    array[T - 1], array[i] = array[i], array[T - 1]
    array[T:] = array[len(array) - 1: T - 1: -1]
    return  ' '.join(array)

for a in range(int(input())):
    print(bigger_is_greater(input()))


excercise 3:

import os

def bomberMan(n, grid):
    if n in [0, 1]:
        return grid
    elif n % 2 == 0:
        return ['O' * len(x) for x in grid]
    else:
        grid = [x.replace('O', '2') for x in grid]
        grid = [x.replace('.', '0') for x in grid]
        grid = [list(map(int, list(x))) for x in grid]

        R = len(grid)
        C = len(grid[0])
        t = 1
        while t < 4 + n % 4:
            t += 1
            destroyed = []
            for r in range(R):
                for c in range(C):
                    if grid[r][c] > 0:
                        grid[r][c] -= 1
                    if t % 2 == 0 and grid[r][c] == 0:
                        grid[r][c] = 3
                    elif grid[r][c] == 0:
                        destroyed.append([r, c])
                        if r < R - 1:
                            destroyed.append([r + 1, c])
                        if r > 0:
                            destroyed.append([r - 1, c])
                        if c < C - 1:
                            destroyed.append([r, c + 1])
                        if c > 0:
                            destroyed.append([r, c - 1])
            if destroyed:
                grid = [[2] * len(x) for x in grid]
                for r, c in destroyed:
                    grid[r][c] = 0
        grid = [''.join(list(map(str, x))) for x in grid]
        grid = [x.replace('2', 'O') for x in grid]
        grid = [x.replace('0', '.') for x in grid]

        return grid


if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')
    rcn = input().split()
    r = int(rcn[0])
    c = int(rcn[1])
    n = int(rcn[2])

    grid = []

    for _ in range(r):
        grid_item = input()
        grid.append(grid_item)

    result = bomberMan(n, grid)

    fptr.write('\n'.join(result))
    fptr.write('\n')

    fptr.close()
    
    
API:

import requests


api_key = "ca08497023ee898260bae6c99585beed42e23"
url = input("Enter your URl: ")
api_url = f"https://cutt.ly/api/api.php?key={api_key}&short={url}"

data = requests.get(api_url).json()["url"]

if len(url) > 250:
    print("Please insert the url at least with 250 characters")


if data["status"] == 7:
    shortened_url = data["shortLink"]
    print("Shortened URL:", shortened_url)
else:
    print("[!] Error Shortening URL:", data)
