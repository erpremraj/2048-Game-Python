# 2048-Game-Python
2048 Game Python
#2048 game
import random

#logic part lecture
def start_game():
    mat = []
    for i in range(4):
        mat.append([0]*4)
    return mat


def add_new_2(mat):
    r = random.randint(0, 3)
    c = random.randint(0, 3)
    while (mat[r][c] != 0):
        r = random.randint(0, 3)
        c = random.randint(0, 3)
    mat[r][c] = 2
    return mat

#reverse and transpose lecture 
def reversed(mat):
    new_mat = []
    for i in range(4):
        new_mat.append([])
        for j in range(4):
            new_mat[i].append(mat[i][4-j-1])
    return new_mat

#reverse and transpose lecture 
def transpose(mat):
    new_mat = []
    for i in range(4):
        new_mat.append([])
        for j in range(4):
            new_mat[i].append(mat[j][i])
    return new_mat

#merge lecture
#merge and compress rectified lecture
def merge(mat):
    changed = False
    #new
    # for i in range(4):
    #     for j in range(3):
    #         if mat[i][j] == mat[i][j+1] and mat[i][j] != 0:
    #             mat[i][j] = mat[i][j]*2
    #             mat[i][j+1] = 0
    #             changed = True
    # return mat,changed
    #old
    for i in range(4):
        for j in range(3):
            if mat[i][j] == mat[i][j+1] and mat[i][j] != 0:
                mat[i][j] = mat[i][j]*2
                mat[i][j+1] = 0
    return mat

#compress lecture
def compress(mat):
    changed = False
    #new
    # new_mat = []
    # for i in range(4):
    #     new_mat.append([0]*4)

    # for i in range(4):
    #     pos = 0
    #     for j in range(4):
    #         if mat[i][j] != 0:
    #             new_mat[i][pos] = mat[i][j]
    #             if j != pos:
    #                 changed = True
    #             pos += 1
    # return new_mat,changed

    #old
    new_mat = []
    for i in range(4):
        new_mat.append([0]*4)

    for i in range(4):
        pos = 0
        for j in range(4):
            if mat[i][j] != 0:
                new_mat[i][pos] = mat[i][j]
                pos += 1
    return new_mat

#current state lecture 
def get_current_state(mat):
    for i in range(4):
        for j in range(4):
            if (mat[i][j] == 2048):
                return 'WON'
    for i in range(4):
        for j in range(4):
            if (mat[i][j] == 0):
                return 'GAME NOT OVER'

    for i in range(3):
        for j in range(3):
            if mat[i][j] == mat[i+1][j] or mat[i][j] == mat[i][j+1]:
                return 'GAME NOT OVER'
    for i in range(3):
        if mat[3][j] == mat[3][j+1]:
            return 'GAME NOT OVER'
    for i in range(3):
        if mat[i][3] == mat[i+1][3]:
            return 'GAME NOT OVER'

    return "LOST"

#code for each possible move
#changed or not lecture
def move_up(grid):
    #Implement This Function
    #new
    # transposed_grid = transpose(grid)
    # new_grid,changed1 = compress(transposed_grid)
    # new_grid,changed2 = merge(new_grid)
    # changed = changed1 or changed2
    # new_grid = compress(new_grid)
    # final_grid = transpose(new_grid)
    # return final_grid,changed
    #old
    transposed_grid = transpose(grid)
    new_grid = compress(transposed_grid)
    new_grid = merge(new_grid)
    new_grid = compress(new_grid)
    final_grid = transpose(new_grid)
    return final_grid


def move_down(grid):
    #Implement This Function
    #new
    # transposed_grid = transpose(grid)
    # reversed_grid = reversed(transposed_grid)
    # new_grid,changed1 = compress(reversed_grid)
    # new_grid,changed2 = merge(new_grid)
    # changed = changed1 or changed2
    # new_grid = compress(new_grid)
    # final_reversed_grid = reversed(new_grid)
    # final_grid = transpose(final_reversed_grid)
    # return final_grid,changed
    #old
    transposed_grid = transpose(grid)
    reversed_grid = reversed(transposed_grid)
    new_grid = compress(reversed_grid)
    new_grid = merge(new_grid)
    new_grid = compress(new_grid)
    final_reversed_grid = reversed(new_grid)
    final_grid = transpose(final_reversed_grid)
    return final_grid


def move_right(grid):
    #Implement This Function
    #new
    # reversed_grid = reversed(grid)
    # new_grid,changed1 = compress(reversed_grid)
    # new_grid,changed2 = merge(new_grid)
    # changed = changed1 or changed2
    # new_grid = compress(new_grid)
    # final_grid = reversed(new_grid)
    # return final_grid,changed
    #old
    reversed_grid = reversed(grid)
    new_grid = compress(reversed_grid)
    new_grid = merge(new_grid)
    new_grid = compress(new_grid)
    final_grid = reversed(new_grid)
    return final_grid


def move_left(grid):
    #Implement This Function
    #new changes
    # new_grid,changed1 = compress(grid)
    # new_grid,changed2 = merge(new_grid)
    # changed = changed1 or changed2
    # new_grid,temp = compress(new_grid)
    # return new_grid,changed
    #old
    new_grid = compress(grid)
    new_grid = merge(new_grid)
    new_grid = compress(new_grid)
    return new_grid


mat = start_game()
mat[1][3] = 2
mat[2][2] = 2
mat[3][0] = 4
mat[3][1] = 8
mat[2][1] = 4
inputs = [int(ele) for ele in input().split()]
for ele in inputs:
    if ele == 1:
        mat = move_up(mat)
    elif ele == 2:
        mat = move_down(mat)
    elif ele == 3:
        mat = move_left(mat)
    else:
        mat = move_right(mat)
    print(mat)

'''
user ip/op:
ip: 
1 2 4 3 2 4 3 1 4

op:
[[4, 4, 2, 2], [0, 8, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
[[0, 0, 0, 0], [0, 0, 0, 0], [0, 4, 0, 0], [4, 8, 2, 2]]
[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 4], [0, 4, 8, 4]]
[[0, 0, 0, 0], [0, 0, 0, 0], [4, 0, 0, 0], [4, 8, 4, 0]]
[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [8, 8, 4, 0]]
[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 16, 4]]
[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [16, 4, 0, 0]]
[[16, 4, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
[[0, 0, 16, 4], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
'''
