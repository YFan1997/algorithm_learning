##calculate distance of each pair of points
points_x=[3,9,11,12,13,15,26,45]
points_y=[2,10,40,-40,7,35,3,12]
#import math function for caculation
import math

def distance(x1,x2,y1,y2):
    return math.sqrt((x1-x2)**2+(y1-y2)**2)

#to check tables
def print_table (r):
    for row in r:
        for item in row:
            print(f"{item:2}", end=' | ')
        print()

#sort these points by x-value
#find the max X value and corresponding point,
#and let the min X value as start point
###rearrange the distance based on the sorted x-axis
points= list(zip(points_x,points_y))
sorted_points =sorted(points,key=lambda point: point[0])
sorted_points_x,sorted_points_y = zip(*sorted_points)
# here get sorted points based on ascending x value,
# create a distance table for each pair of points
def calculation_distance(sorted_points_x,sorted_points_y):
    n = len(sorted_points_x)
    d = [[0 for _ in range(n)] for _ in range(n)]
    for i in range (0,n):
        for j in range (0,i+1):
            d[i][j] = distance(sorted_points_x[i],sorted_points_x[j],
                               sorted_points_y[i],sorted_points_y[j])
            d[j][i] = d[i][j]
    return d

# print table out and round the table for more direct view and check
dp = calculation_distance(sorted_points_x,sorted_points_y)
rounded_table_d = [[round(value, 2) for value in row] for row in dp]
print_table(rounded_table_d)
#find btsp route by partition points into four part
def btsp (x,y,dp):
    max_x = max(x)
    min_x = min(x)
    middle_x = min_x + 1 / 2 * (max_x - min_x)
    middle_y = min(y[0], y[-1]) + (1 / 2 * abs(y[-1] - y[0]))
    a = []
    b = []
    c = []
    d = []
    for p in range(0, len(x)):
        if x[p] <= middle_x and y[p] >= middle_y:
            a.append(p)
        if x[p] > middle_x and y[p] > middle_y:
            b.append(p)
        if x[p] >= middle_x and y[p] <= middle_y:
            c.append(p)
        if x[p] < middle_x and y[p] < middle_y:
            d.append(p)
    route = a+b+sorted(c,reverse=True)+sorted(d,reverse=True)
    if route[0] != 0:
        route.insert(0,0)
    if route[-1] != 0:
        route.append(0)
    dist = 0
    k = 0
    while k < len(route)-2:
        dist = dist+ dp[route[k]][route[k+1]]
        k = k+1
    return route,dist
route, dist = btsp(sorted_points_x,sorted_points_y,dp)
print('the optimal btsp route is:',route)
print('the optimal btsp distance is:',dist)
