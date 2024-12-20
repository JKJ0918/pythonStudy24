# pythonStudy24
파이썬 ai 기초 학습용

MBC 아카데미 컴퓨터 교육센터 수원점에서 AI기초 학습으로 파이썬 학습 진행용

https://wikidocs.net/book/1

```
while study 미션 코드

# 미션
# 관리자가 커피가격과 커피명을 정하고 개수를 입력한다.
# 소비자가 커피를 구매하는데 잔돈이 나와야 함
# 판매 종료 후 관리자가 커피 판매한 총액을 파악해야 함.


# 음료 데이터 저장할 리스트
vending_machine = []

# 등록할 음료의 종류 수 입력받기
num_drinks = int(input("등록할 음료 종류의 수를 입력하세요: "))

# 음료 정보 입력받기
i = 0
while i < num_drinks:
    print(f"\n{i+1}번째 음료 등록")
    name = input("음료 이름을 입력하세요: ")

    # 가격 입력 및 숫자 확인
    while True:
        price_input = input("음료 가격을 입력하세요 (숫자): ")
        if price_input.isdigit():  # 숫자인지 확인
            price = int(price_input)  # 정수로 변환
            break
        else:
            print("가격은 숫자만 입력 가능합니다. 다시 입력해주세요.")

    while True:
        quantity_input = input("판매 수량을 입력하세요 (숫자): ")
        if quantity_input.isdigit():  # 숫자인지 확인
            quantity = int(quantity_input)  # 정수로 변환
            break
        else:
            print("수량은 숫자만 입력 가능합니다. 다시 입력해주세요.")

    # 음료 정보 저장
    vending_machine.append({"name": name, "price": price, "quantity": quantity})
    i += 1


# 등록된 음료 출력
print("\n등록된 음료 목록:")
for drink in vending_machine:
    print(f"이름: {drink['name']}, 가격: {drink['price']}원, 수량: {drink['quantity']}개")

# drink 변수는 for 반복문 안에서 자동으로 생성된 변수
# for 루프를 사용할 때 반복 대상의 각 요소를 임시로 참조할 변수를 지정할 수 있는데,
# 여기서 그 변수가 바로 drink


# 소비자 구매

total_sales = 0  # 총 판매 금액
while True:
    pick_name = input("\n구매하실 음료의 이름을 적어주세요 (종료: '끝') : ")
    if pick_name == "끝":
        break

    # 음료 찾기
    selected_drink = next((drink for drink in vending_machine if drink["name"] == pick_name), None)
     # [<결과값> for <변수> in <리스트> if <조건>]
     # None 위 코드에서 None은 next() 함수의 **기본값(default value)**으로 설정
     # 조건에 맞는 음료를 찾지 못했을 때 selected_drink에 None을 할당
     # "값이 없음을 명확히 표현"하기 위해, 안전한 기본값, 에러 방지(StopIteration 예외가 발생)
     # next(iterator, default_value)
    if not selected_drink:
        print("존재하지 않는 음료입니다. 다시 선택해주세요.")
        continue
        # continue를 쓰지 않을 경우 selected_drink가 None값으로 아래 수량 입력으로 진행 될 수 있음
        # continue의 역할은 다음 반복을 강제로 시작


    # 수량 입력 및 확인 while
    while True:
        pick_amount = int(input("수량을 입력해 주세요 : "))
        if pick_amount > selected_drink["quantity"]:
            print(f"죄송합니다. 재고가 부족합니다. 남은 수량: {selected_drink['quantity']}개")
        # if 문을 충족하지 수량 입력 및 확인 while로 감
        else:
            break

    # 금액 입력 및 잔돈 계산
    total_price = selected_drink["price"] * pick_amount
    print(f"총 금액은 {total_price}원입니다.")
    while True:
        paid = int(input("지불할 금액을 입력해주세요: "))
        if paid < total_price:
            print(f"금액이 부족합니다. {total_price - paid}원을 더 지불해주세요.")
        else:
            change = paid - total_price
            print(f"거스름돈: {change}원")
            break

    # 재고 차감 및 총 판매 금액 계산
    selected_drink["quantity"] -= pick_amount
    total_sales += total_price
    print(f"{pick_amount}개의 {selected_drink['name']}을 구매하셨습니다. 남은 수량: {selected_drink['quantity']}개")

# 판매 종료 후 총액 출력
print(f"\n판매 종료. 총 판매 금액은 {total_sales}원입니다.")




```
