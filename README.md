# Mục lục

## [1. Tổ chức & Mô tả](#1)

## [2. Ví dụ sử dụng](#2)

<hr>
<br>

# Nội dung  

<a name = "1"></a>
## 1. Tổ chức & Mô tả

```
itptit
|
|___common
|   |___math
|   |   |___...
|   |
|   |___random
|   |   |___Random
|   |   |___...
|   |
|   |___exceptions
|       |___...
|
|___generator
|   |___TestCaseFamily
|   |___Inerator
|   |___Outerator
|
|___judge
    |___SingleJudge
    |___MultiJudge
    |___...
```

### **Mô tả**

Nội dung các class và function sẽ được mô tả bởi python docstring.

<a name = "2"></a>
## 2. Ví dụ sử dụng

### 2.1. Problem

Tính tổng các số có trong dãy `n` phần tử với 2 ≤ `n` ≤ 3.

| Input | Output |
|:-----:|:------:|
|  1 2  |    3   |
| 1 2 3 |    6   |

### 2.1. Files

- #### **real_solution.py**

``` python
ans = 0
for i in input().split():
    ans += int(i)
print(ans)
```

- #### **submitted_solution.cpp**

``` cpp
#include <iostream>
using namespace std;

int main(){
    int x, y;
    cin >> x >> y;
    cout << x + y;
    return 0;
}
```

- #### **gen_test_case.py**

``` python
from itptit.common.math import *
from itptit.common.random import *
from itptit.generator import TestCaseFamily, Inerator, Outerator
from itptit.judge import SingleJudge

def _2_numbers(x, y):
    print(x, y)

def _3_numbers(x, y, z):
    print(x, y, z)


# Create TestCaseFamily

tcf1 = TestCaseFamily(
    gen_func=_2_numbers,
    number_of_test_cases=2,
    args_list=[
        [1, 2],
        [2, 3]
    ]
)

tcf2 = TestCaseFamily(
    gen_func=_3_numbers,
    number_of_test_cases=3,
    args_list=[
        [1, 2, 3],
        [2, 3, 4],
        [3, 4, 5]
    ],
    name='3 numbers'                # Optional argument
)

# Generate input

ig = Inerator(
    'test/input',
    tcf1,
    tcf2,
    file_extension='itqh'           # Optional argument
)

ig.start()

# Generate output

og = Outerator(
    'test/input',
    'real_solution.py',
    'test/output',
    input_file_extension='itqh',    # Optional argument
    file_extension='otqh'           # Optional argument
)

og.start()

# Judgement

judge = SingleJudge(
    'test/input',
    'test/output',
    'submitted_solution.cpp', 
    time_limit=1,                   # Optional argument
    input_extension='itqh',         # Optional argument
    output_extension='otqh'         # Optional argument
)

judge.start()
```

- #### **Run "gen_test_case.py"**

``` console
Start generating input for test cases:
- New: Created file "0.itqh" successfully in 0.00000s!
- New: Created file "1.itqh" successfully in 0.00000s!
- New: Created file "2.itqh" successfully in 0.00000s!
- New: Created file "3.itqh" successfully in 0.00000s!
- New: Created file "4.itqh" successfully in 0.00050s!
All test case's inputs have been generated.

Start generating output for test cases:
- New: Created file "0.otqh" successfully in 0.07481s!
- New: Created file "1.otqh" successfully in 0.10607s!
- New: Created file "2.otqh" successfully in 0.07828s!
- New: Created file "3.otqh" successfully in 0.06917s!
- New: Created file "4.otqh" successfully in 0.07155s!
All test case's outputs have been generated.

Start judgment:
- Testcase 0."0": Accepted (AC) in 0.063s.
- Testcase 1."1": Accepted (AC) in 0.082s.
- Testcase 2."2": Wrong answer (WA).
- Testcase 3."3": Wrong answer (WA).
- Testcase 4."4": Wrong answer (WA).
  > Result: Partial (2/5).
```