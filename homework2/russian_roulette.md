# 러시안 룰렛

운이 생사를 가르는 복불복 게임.  
6발이 장전 가능한 리볼버에 단 하나의 총알만 넣은 뒤, 실린더를 무작위로 돌립니다.  
이후 플레이어들은 번갈아 가며 총구를 자신의 머리에 겨누고 방아쇠를 당깁니다.

러시안 룰렛 프로그램을 작성해봅시다.

---

## 🔫 조건 및 설명

- `0`은 빈 약실, `1`은 총알이 들어 있는 약실을 의미합니다.

```python
bullets = [0, 0, 0, 0, 0, 1]
```

- `random` 패키지를 사용해 실린더를 무작위로 돌립니다.
- 총알은 왼쪽에서 오른쪽으로 순서대로 발사됩니다.
- `player1`부터 시작하며, 두 플레이어는 번갈아 가며 방아쇠를 당깁니다:  
  `player1` → `player2` → `player1` → ...
- 총알이 발사될 때까지 게임을 진행하고, 총에 맞은 플레이어의 이름을 출력한 뒤 게임을 종료합니다.

---

## 💻 출력 예시

```
player1 자기 머리에 총을 겨눕니다
총알이 격발되지 않았습니다
player2 자기 머리에 총을 겨눕니다
총알이 격발되지 않았습니다
player1 자기 머리에 총을 겨눕니다
총알이 발사되었습니다
player1 사망
게임 종료
```

---
