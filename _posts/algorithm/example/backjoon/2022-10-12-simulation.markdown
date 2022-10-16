---
layout: posts
title:  "Simulation"
date:   2022-10-12 07:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
  - series
---

# Introduction

## 로봇 청소기
https://www.acmicpc.net/problem/14503

{% highlight python %}
def robot_clean(locations,robot_loc):
    locations[robot_loc[0]][robot_loc[1]] = 2
    return locations

def check_clean(locations,robot_loc,robot_pos):
  # search
    if robot_pos == 0:
        loc = locations[robot_loc[0]-1][robot_loc[1]]
    elif robot_pos == 1:
        loc = locations[robot_loc[0]][robot_loc[1]+1]
    elif robot_pos == 2:
        loc = locations[robot_loc[0]+1][robot_loc[1]]
    elif robot_pos == 3:
        loc = locations[robot_loc[0]][robot_loc[1]-1]
  # check
    if loc == 0:  res = True
    else:         res = False
    return res

def robot_go(robot_loc,robot_pos):
    if robot_pos == 0:    robot_loc[0] -= 1
    elif robot_pos == 1:  robot_loc[1] += 1
    elif robot_pos == 2:  robot_loc[0] += 1
    elif robot_pos == 3:  robot_loc[1] -= 1
    return robot_loc

def robot_left(robot_pos):
    if robot_pos == 0:    robot_pos = 3
    elif robot_pos == 1:  robot_pos = 0
    elif robot_pos == 2:  robot_pos = 1
    elif robot_pos == 3:  robot_pos = 2
    return robot_pos

def robot_back(robot_loc,robot_pos):
    if robot_pos == 0:    robot_loc[0] += 1
    elif robot_pos == 1:  robot_loc[1] -= 1
    elif robot_pos == 2:  robot_loc[0] -= 1
    elif robot_pos == 3:  robot_loc[1] += 1
    return robot_loc

def print_location(locations):
    for i in range(len(locations)):
        print(locations[i])

N, M = map(int,input().split())
r, c, d = map(int,input().split())
locations = []
for _ in range(N):
    loc = list(map(int,input().split()))
    locations.append(loc)

#print("-- location --")
#print_location(locations)
# (r,c), (x,y)
# d==0 왼쪽, d==1 아래, d==2 오른쪽, d==3 위

robot_loc = [r,c]
robot_pos = d
result = 0
do = True
while(do):
    locations = robot_clean(locations,robot_loc)
    result += 1
    #print("-- state{} --".format(result))
    #print_location(locations)
    cnt = 0
    flag = True
    while(flag):
        cnt += 1
        robot_pos = robot_left(robot_pos)
        check = check_clean(locations,robot_loc,robot_pos)
        if check == True:
            #print("--- step 1: go ---")
            robot_loc = robot_go(robot_loc,robot_pos)
            flag = False
        elif check == False and cnt<4:
            #print("--- step 2: left ---")
            pass
        elif check == False and cnt==4:
            #print("--- step 3: back ---")
            robot_loc = robot_back(robot_loc,robot_pos)
            cnt = 0
            if locations[robot_loc[0]][robot_loc[1]] == 1:
                #print("--- stop ---")
                flag = False
                do = False
    #if result == 100:
    #  flag = False
    #  do = False
print(result)
{% endhighlight %}