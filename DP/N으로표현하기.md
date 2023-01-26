![image](https://user-images.githubusercontent.com/89527573/214772507-58552810-bbc5-4ae1-9af5-9cc63f4c1027.png)

# idea
----
다른 사람의 풀이이다. DP는 어려워서 좀 공부를 해야할 것 같다   
풀이출처 https://school.programmers.co.kr/questions/29313

1.N을 1번 사용, 2번 사용.... 8번 사용을 하면서 나온 수들 중에서 target이 있나 확인   
2.N번 사용한 값은  
1번 사용한 값 & N -1번 사용한 값   
2번 사용한 값 & N -2번 사용한 값   
...
을 연산한 값과 같다. 큰 수를 작은 수로 분해하는 형식   
예로 5로 12를 만드려면 (55+5)/5인데 55는 2번 사용한 값, 55+5는 3번 사용한 값이고   
2번 사용한 값을 이용해서 3번 사용한 값인 60을 만들고 -> 3번 사용한 값인 60을 이용해서 4번 사용한 값인 12가 만들어진다.   

# solution
----
````

def calculate_n(X, Y):
    n_set = set()
    for x in X:
        for y in Y:
            n_set.add(x+y)
            n_set.add(x-y)
            n_set.add(x*y)
            if y != 0:
                n_set.add(x//y)
    return n_set
def solution(N, number):
    answer = -1
    result = {}   
    result[1] = {N} 
    if number == N:
        return 1
    
    for n in range(2, 9):  
        i = 1
        temp_set = {int(str(N)*n)}  
        while i < n:
            temp_set.update(calculate_n(result[i], result[n-i]))
            i += 1
        if number in temp_set:
            answer = n
            break
        result[n] = temp_set
    return answer

