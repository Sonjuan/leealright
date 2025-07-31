# Homework1: 함수 체인과 백엔드 업무 흐름

하나의 데이터에 대해 연쇄적으로 **함수(function)** 를 적용하고 결과값을 도출하는 과정은 백엔드 개발에서 자주 등장하는 패턴입니다.

---

## 💼 업무 예시

> **시나리오**: 게임 데이터를 받아, 현재 게임에 참가한 플레이어 중 블랙리스트를 제외하고 가장 딜을 많이 넣은 플레이어에게 보상을 준다.

이를 다음과 같은 **Task**로 나눌 수 있습니다:

1. 게임 데이터 받기
2. 현재 게임에 참가한 플레이어 구하기
3. 블랙리스트 플레이어 제외하기
4. 가장 딜을 많이 넣은 플레이어 찾기
5. 보상 주기

> ⚠️ 코드 예시는 실제 작동하는 코드가 아닌 **이해를 돕기 위한 예시**입니다.

---
## 1. 게임 데이터 받기

### 📦 DB에서 가져오는 경우:

```python
client = MongoClient("mongodb://localhost:27017/")
db = client["your_database"]
collection = db["game_matches"]
raw_data = collection.find_one({"matchID": "a391jfbz0183"})
```
### 🌐 API를 통해 가져오는 경우:

```python
response = requests.get(f"https://api.riotgames.com/lol/summoner/v4/summoners/by-name/{summoner_name}", headers=HEADERS)
raw_data = response.json()
```

### 🔧 전처리 함수:
```python
def trim(data):
    # 데이터 구조를 보기 좋게 정리하거나 필요한 타입으로 가공하는 함수
    전처리 알고리즘
    return processed_data

data = trim(raw_data)
```
---

## 2. 현재 게임에 참가한 플레이어 구하기

```python
def get_players(data):
    res = []
    for d in data:
        res.append(d['players'])
    return res

get_players(trim(raw_data))
```

---

## 3. 블랙리스트 플레이어 제외
```python
def filter_blacklist(data):
    return list(filter(filter_functionX, data)) # 미리 정의된 블랙리스트 필터 사용
filter_blacklist(get_players(trim(raw_data)))
```    
---
## 4. 딜을 가장 많이 넣은 플레이어 찾기

```python
def find_most_deadly_player(data):
    # damage 값을 기준으로 정렬하고 가장 높은 딜을 넣은 플레이어 반환
    return sorted(data, key=lambda x: x['damage'], reverse=True)[0]

find_most_deadly_player(filter_blacklist(get_players(trim(raw_data))))
```  
---

## 5. 보상 주기
```python
def reward(player):
    """선정된 플레이어에게 보상 제공"""
    try:
        if 상자주기코드():
            return 1  # 성공
        print("보상 지급 실패: 상자주기코드에서 False 반환")
        return 0  # 실패
    except Exception as e:
        print(f"보상 지급 중 오류 발생: {e}")
        return 0  # 예외 발생
```       
파이프라인 실행
```python
final_result = 
    reward(
        find_most_deadly_player(
            filter_blacklist(
                get_players(
                    trim(raw_data)
                )
            )
        )
    )
```
---

## 🧠 핵심 개념 요약

이러한 프로세스를 통해 백엔드의 로직은 다음과 같은 **데이터 처리 흐름**을 따릅니다:

```
[데이터]
   ↓
함수1(데이터)
   ↓
함수2(데이터)
   ↓
함수3(데이터)
   ↓
[원하는 결과]
   ↓
API 응답 or 프론트엔드에 전달
```
이 예시는 가독성을 위해 최적화/재사용성 등의 요소를 고려하지 않았으며, 실제 구현에서는 에지 케이스 처리와 성능 최적화가 필요합니다.