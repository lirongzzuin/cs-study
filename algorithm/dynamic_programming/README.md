# 동적 프로그래밍 (Dynamic Programming)

## 1. 동적 프로그래밍이란?
동적 프로그래밍(Dynamic Programming, DP)은 **큰 문제를 작은 부분 문제로 나누고, 해당 부분 문제들의 결과를 저장하여 동일한 계산을 반복하지 않도록 최적화하는 알고리즘 기법**이다. 일반적으로 **재귀(Recursion)와 메모이제이션(Memoization)을 활용하여 구현**된다.

### 🔹 동적 프로그래밍의 주요 특징
- **부분 문제 최적화**: 큰 문제를 작은 문제로 나누어 해결
- **중복 계산 방지**: 이전에 계산한 값을 저장하여 다시 활용
- **최적 부분 구조(Optimal Substructure)와 중복 부분 문제(Overlapping Subproblems) 속성 필요**

---

## 2. 동적 프로그래밍 vs 분할 정복
| 특징 | 동적 프로그래밍(DP) | 분할 정복(Divide & Conquer) |
|------|-----------------|-------------------|
| **부분 문제 중복 여부** | 있음 (Overlapping Subproblems) | 없음 |
| **중복 계산 최적화** | 메모이제이션 또는 테이블 저장 | 불필요 |
| **대표 알고리즘** | 피보나치 수열, 배낭 문제, 최장 공통 부분 수열(LCS) | 병합 정렬, 퀵 정렬 |

---

## 3. 동적 프로그래밍 접근 방식
### 🔹 탑다운(Top-Down) (재귀 + 메모이제이션)
- 큰 문제를 작은 문제로 나누고, 결과를 **캐싱하여 저장**
- 재귀 호출을 기반으로 구현
- **예제**: 피보나치 수열 (재귀 + 메모이제이션)

### 🔹 보텀업(Bottom-Up) (반복 + 테이블 저장)
- 작은 문제부터 차례로 해결하며 **결과를 배열이나 테이블에 저장**
- 반복문을 기반으로 구현
- **예제**: 배낭 문제 (테이블 기반 구현)

---

## 4. 코드 예제
### 🔹 피보나치 수열 (동적 프로그래밍 적용)
##### Java (탑다운 & 보텀업)
```java
import java.util.Arrays;

public class FibonacciDP {
    static int[] memo = new int[100];
    
    // 탑다운 방식 (재귀 + 메모이제이션)
    static int fibTopDown(int n) {
        if (n <= 1) return n;
        if (memo[n] != 0) return memo[n];
        return memo[n] = fibTopDown(n - 1) + fibTopDown(n - 2);
    }
    
    // 보텀업 방식 (반복문 사용)
    static int fibBottomUp(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 0; dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
    
    public static void main(String[] args) {
        Arrays.fill(memo, 0);
        System.out.println("탑다운 방식: " + fibTopDown(10));
        System.out.println("보텀업 방식: " + fibBottomUp(10));
    }
}
```

##### JavaScript (탑다운 & 보텀업)
```javascript
// 탑다운 방식 (재귀 + 메모이제이션)
function fibTopDown(n, memo = {}) {
    if (n <= 1) return n;
    if (memo[n]) return memo[n];
    return memo[n] = fibTopDown(n - 1, memo) + fibTopDown(n - 2, memo);
}

// 보텀업 방식 (반복문 사용)
function fibBottomUp(n) {
    let dp = [0, 1];
    for (let i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}

console.log("탑다운 방식:", fibTopDown(10));
console.log("보텀업 방식:", fibBottomUp(10));
```

##### Python (탑다운 & 보텀업)
```python
# 탑다운 방식 (재귀 + 메모이제이션)
def fib_top_down(n, memo={}):
    if n <= 1:
        return n
    if n in memo:
        return memo[n]
    memo[n] = fib_top_down(n - 1, memo) + fib_top_down(n - 2, memo)
    return memo[n]

# 보텀업 방식 (반복문 사용)
def fib_bottom_up(n):
    dp = [0, 1]
    for i in range(2, n + 1):
        dp.append(dp[i - 1] + dp[i - 2])
    return dp[n]

print("탑다운 방식:", fib_top_down(10))
print("보텀업 방식:", fib_bottom_up(10))
```

---

## 5. 동적 프로그래밍 사용 시 고려할 점
- **부분 문제의 중복 여부 확인**: 동일한 부분 문제가 여러 번 호출되는지 확인 필요
- **메모이제이션(캐싱) 사용**: 계산된 값을 저장하여 중복 연산 방지
- **공간 복잡도 최적화 가능 여부**: 보텀업 방식에서 `O(n)`의 공간을 `O(1)`로 줄이는 기법 활용 가능
- **탑다운 vs 보텀업 선택**: 재귀 호출이 깊어지는 경우 스택 오버플로우 방지를 위해 보텀업 방식 고려

---

## 6. 면접 질문 예시 및 답변

### 1️⃣ 동적 프로그래밍이란 무엇이며, 언제 사용되는가?
동적 프로그래밍은 **큰 문제를 작은 부분 문제로 나누고, 부분 문제의 결과를 저장하여 동일한 연산을 반복하지 않는 알고리즘 기법**이다. 피보나치 수열, 최단 경로 문제, 배낭 문제 등에 활용된다.

### 2️⃣ 동적 프로그래밍의 핵심 속성은 무엇인가?
1. **최적 부분 구조(Optimal Substructure)**: 부분 문제의 최적 해가 전체 문제의 최적 해를 구성해야 함.
2. **중복 부분 문제(Overlapping Subproblems)**: 동일한 부분 문제가 여러 번 반복되어 사용됨.

### 3️⃣ 재귀를 사용한 동적 프로그래밍의 단점은?
재귀 호출이 많아질 경우 **스택 오버플로우**가 발생할 수 있으며, 메모이제이션이 없으면 중복 연산이 많아져 성능이 저하될 수 있다.

### 4️⃣ 동적 프로그래밍을 적용할 수 없는 경우는?
부분 문제가 독립적이거나, 최적 부분 구조를 가지지 않는 경우 동적 프로그래밍을 적용하기 어렵다.

### 5️⃣ 보텀업 방식이 탑다운 방식보다 유리한 경우는?
재귀 호출이 과도하게 많아지는 경우, 보텀업 방식이 스택 오버플로우를 방지하고 성능을 향상시킬 수 있다.

### 6️⃣ 0/1 배낭 문제에서 동적 프로그래밍을 어떻게 적용할 수 있는가?
배낭 문제는 **이전 계산된 결과를 저장하면서 최적의 해를 찾는 테이블을 채우는 방식**으로 해결할 수 있다.

### 7️⃣ 동적 프로그래밍의 시간 복잡도는 어떻게 계산되는가?
탑다운과 보텀업 모두 중복 계산을 제거하므로 **일반적으로 O(n) 또는 O(n²)**의 복잡도를 가진다.

---