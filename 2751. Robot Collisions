class Solution:
    def survivedRobotsHealths(self, positions, healths, directions):
        robots = sorted([(positions[i], healths[i], directions[i], i) for i in range(len(positions))])
        stack = []

        robots = [list(r) for r in robots]

        for i in range(len(robots)):
            if robots[i][2] == 'R':
                stack.append(i)
            else:
                while stack and robots[i][1] > 0:
                    j = stack[-1]
                    if robots[j][1] < robots[i][1]:
                        stack.pop()
                        robots[i][1] -= 1
                        robots[j][1] = 0
                    elif robots[j][1] > robots[i][1]:
                        robots[j][1] -= 1
                        robots[i][1] = 0
                        break
                    else:
                        robots[j][1] = 0
                        robots[i][1] = 0
                        stack.pop()
                        break

        res = sorted([(r[3], r[1]) for r in robots if r[1] > 0])
        return [h for _, h in res]
