# HW3-1

# 初始環境設定
from collections import deque

player_gold = 150
barracks_A = deque()
barracks_B = deque()
length_A = len(barracks_A)
length_B = len(barracks_B)
# 玩家送來的一批訂單 (包含單位名稱與花費)
orders = [
    {"unit": "劍士", "cost": 20},
    {"unit": "弓手", "cost": 30},
    {"unit": "騎士", "cost": 50},
    {"unit": "投石車", "cost": 40}
]

for round_num, order in enumerate(orders):
    print(f"\n--- 第 {round_num} 回合 ---") # 方便看輸出結果
    # TODO
    if order == {} :
        print("玩家本回合無動作，單純推進時間")
        continue
    if round_num%2 :
        if player_gold > order["cost"] :
            if length_A<=2 or length_B<=2 :
                if length_A>length_B : 
                    barracks_B.append(order["unit"])
                    length_B += 1
                    print(f"{order['unit']} 分派至 B廠",end="")
                else:
                    barracks_A.append(order["unit"])
                    length_A += 1
                    print(f"{order['unit']} 分派至 A廠",end="")
                player_gold-=order["cost"]
                print(f"剩餘黃金({player_gold})")
            else :
                print(f"產線全滿！ {order["unit"]}訂單拒絕")
    else :
        if length_A>0 :
            print(f"A 廠生產完成 :{barracks_A.popleft()}出列")
            length_A -= 1
        else :
            print("A 廠沒東西可做(underflow 防護成功)")
        if length_B>0 :
            print(f"B 廠生產完成 :{barracks_B.popleft()}出列")
            length_B -= 1
        else :
            print("B 廠沒東西可做(underflow 防護成功)")
        if player_gold > order["cost"] :
            if length_A<=2 or length_B<=2 :
                if length_A>length_B : 
                    barracks_B.append(order["unit"])
                    length_B += 1
                    print(f"{order['unit']} 分派至 B廠",end="")
                else:
                    barracks_A.append(order["unit"])
                    length_A += 1
                    print(f"{order['unit']} 分派至 A廠",end="")
                player_gold-=order["cost"]
                print(f"剩餘黃金({player_gold})")
            else :
                print(f"產線全滿！ {order["unit"]}訂單拒絕")
    print(f"A: {list(barracks_A)} | B: {list(barracks_B)}")

    
