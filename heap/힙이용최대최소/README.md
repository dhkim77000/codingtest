준호는 처음에 병사 n명을 가지고 있습니다.   
매 라운드마다 enemy[i]마리의 적이 등장합니다.    
남은 병사 중 enemy[i]명 만큼 소모하여 enemy[i]마리의 적을 막을 수 있습니다.      
예를 들어 남은 병사가 7명이고, 적의 수가 2마리인 경우, 현재 라운드를 막으면 7 - 2 = 5명의 병사가 남습니다.    
남은 병사의 수보다 현재 라운드의 적의 수가 더 많으면 게임이 종료됩니다.    
게임에는 무적권이라는 스킬이 있으며, 무적권을 사용하면 병사의 소모없이 한 라운드의 공격을 막을 수 있습니다.    
무적권은 최대 k번 사용할 수 있습니다.    
준호는 무적권을 적절한 시기에 사용하여 최대한 많은 라운드를 진행하고 싶습니다.    

----
준호가 처음 가지고 있는 병사의 수 n    
사용 가능한 무적권의 횟수 k    
매 라운드마다 공격해오는 적의 수가 순서대로 담긴 정수 배열 enemy가 매개변수로 주어집니다    
준호가 몇 라운드까지 막을 수 있는지 return 하도록 solution 함수를 완성해주세요.    

## idea
-----
DFS로 풀어볼수도 있지만 모든 경우의 수를 계산하기 때문에 시간복잡도 측면에서 비효율적   
**무적권은 최대한 병사 수가 많은 라운드에 사용을 해야함**   
heap을 이용해서 기존에 무적권을 사용한 라운드 중 제일 적은 병사 수 vs 이번 라운드 병사 수를 비교하면서 replace

## solution   
-----
 1.무적권이 남아있으면 일단 넣기   
 2.무적권을 다 사용했으면 비교 시작   
 3.새로 들어온 병사가 무적권 최소 병사보다 크면 이 라운드에 무적권을 사용해야하므로 바꿔준다    
 4.남아있는 병사가 더 많으면 병사 소모하고 그렇지 않으면 끝
    
 ----
````
def solution(n, k, enemy):
    answer = 0
    i = 1
    k_left = k
    n_left = n
    k_heap = []
    n_round = 0
    for soldiers in enemy:
        if k_left > 0:
            heapq.heappush(k_heap, soldiers)
            k_left -= 1
        else: 
            k_min = k_heap[0]
            if k_min < soldiers:
                heapq.heappush(k_heap, soldiers)
                soldiers = heapq.heappop(k_heap)
            if n_left >= soldiers:
                n_left -= soldiers
            else: break
        n_round += 1

    return n_round
````


