def run(program: list) -> list:
    printed_result = []
    keywords = []
    variables = {chr(i): 0 for i in range(65, 91)}
    end = False
    starting_idx = 0

    # collect the keywords
    for i, val in enumerate(program):
        x = (i, val)
        # keywords are single words
        if " " not in val:
            keywords.append((i, val))

    while not end:
        for idx, i in enumerate(program[starting_idx:]):
            # split the string to get the values
            i = i.split()

            # add variable value to the output
            if i[0] == "PRINT":
                # printing a variable value
                try:
                    printed_result.append(variables[i[1]])
                # printing a raw number
                except KeyError:
                    printed_result.append(int(i[1]))

            # assign value to variables
            elif i[0] == "MOV":
                # When an arguement is a key
                try:
                    variables[i[1]] = int(i[2])
                except ValueError:
                    variables[i[1]] = variables[i[2]]

            # adding
            elif i[0] == "ADD":
                # When an arguement is a key
                try:
                    variables[i[1]] = variables[i[1]] + variables[i[2]]
                except KeyError:
                    variables[i[1]] = variables[i[1]] + int(i[2])

            # subtracting
            elif i[0] == "SUB":
                # when an argument is a key
                try:
                    variables[i[1]] = variables[i[1]] - variables[i[2]]
                except KeyError:
                    variables[i[1]] = variables[i[1]] - int(i[2])

            # multiplying
            elif i[0] == "MUL":
                try:
                    variables[i[1]] = variables[i[1]] * variables[i[2]]
                except KeyError:
                    variables[i[1]] = variables[i[1]] * int(i[2])

            # Moving to new keyword
            elif i[0] == "JUMP":
                for pos, word in keywords:
                    if i[1] + ":" == word:
                        starting_idx = pos
                        break
                break

            # Conditional statements
            elif i[0] == "IF":
                try:
                    var1 = variables[i[1]]
                except KeyError:
                    var1 = i[1]
                try:
                    var2 = variables[i[3]]
                except KeyError:
                    var2 = i[3]

                operand = i[2]
                # compute the comparison
                compare = eval(str(var1) + operand + str(var2))
                jump_to = i[5] + ":"

                # Perform the Jump
                if compare:
                    for pos, word in keywords:
                        if jump_to == word:
                            starting_idx = pos
                            break
                    break

            # End program
            elif i[0] == "END":
                end = True

    return printed_result
