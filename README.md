import math

def minimax(d, i, is_max, scores, depth):
    if d == depth:
        return scores[i]
    fn = max if is_max else min
    return fn(minimax(d+1, i*2, not is_max, scores, depth),
              minimax(d+1, i*2+1, not is_max, scores, depth))

scores = [3, 5, 2, 9, 12, 5, 23, 23]
depth = int(math.log2(len(scores)))

print("The optimal value is:", minimax(0, 0, True, scores, depth))
