# 1주차 
### Chapter 1\~3 (p.1\~p.44)
["알고리즘 트레이닝 프로그래밍 대회 입문 가이드"](https://book.naver.com/bookdb/book_detail.nhn?bid=14829160)를 스터디 북으로 정하고 진도에 맞춰 공부 후 공유를 하는 방식으로 스터디를 진행하기로 했다.<br/><br/>
1주차 공부를 한 후 이책에 대한 전반적인 느낌은 아래와 같다.<br/>
이 책은 알고리즘 대회를 준비하는 책이다. 때문에 [종만북](https://book.naver.com/bookdb/book_detail.nhn?bid=7058764)과 같이 알고리즘 기법에 대한 설명이라기 보다, 알고리즘 기법은 따로 공부를 해야하고 어떻게 사고하는가에 대한 공유를 하는 느낌이었다.<br/>
결론은 책의 목차를 참고를 하되, 알고리즘 공부는 알아서 해야 한다.<br/>
마지막으로 이 책은 C++ 기반으로 되어 있었기 때문에 나에게는 비교적 거부감이 많이 없었다.<br/><br/>

첫주차에는 책을 읽고 정리하는 과정이기 때문에 책 내용 자체를 정리하기 보다는, 좀 더 알았으면 하는 내용을 적는 것을 하려고 한다.

1. 들어가며
    - 프로그래밍 대회의 대한 간단한 소개를 해 놓은 챕터이기 때문에 사실상 정리 할 내용이 없다.<br/><br/>
2. 프로그래밍 기법
    1. 언어적 특성<br/>
    C++ 관련 입출력 방식에 대한 설명이 나온 챕터이다.<br/>
    이 챕터는 아래와 같이 C++로 알고리즘 문제를 풀때 가장 기초적인 설정에 대한 내용이었다.<br/>
        1. 알고리즘 문제는 보통 입력 값을 받은 후 생각한 대로 문제를 푼 후 출력값을 제출하여 채점하는 방식으로 이뤄진다.<br/>
        때문에 C++을 사용할 때 입/출력에 대한 패널티를 알지 못하면, 결과를 제출(출력) 하지 못해 0점 처리 되는 문제도 종종 발생한다.<br/><br/>
        특히 C++의 경우 std::cout, std::cin(나는 namespace에 std를 선언하는 것을 좋아하지 않는다.)의 경우 ios::sync_with_stdio(false), cin.tie(NULL)에 대한 설명이 간단하게 적혀있는데 한번 인지하고 지나가야 하는 개념이라고 생각한다.<br/><br/>
            - ios::sync_with_stdio(false)<br/>
            ios::sync_with_stdio 옵션을 false로 설정하는 것은 c++ 표준인 iostream과 c 표준인 stdio의 동기화를 끊어주는것을 의미 한다.<br/>
            기본적으로 표준 입출력 방식은 iostream(c++), stdio(c)의 버퍼를 동기화해 사용한다. 때문에 c++ code에서 cin&cout과 printf&scanf를 혼용해서 쓰더라도 순서에 맞게 Thread safe하게 동작하는 것이다.<br/>
            하지만 동기화를 끊는다면 c++의 iostream만의 독립적인 버퍼를 생성하여 사용한다. 이는 곧 c의 표준 입출력 버퍼와 동기화를 하지 않는 것을 의미하고, 버퍼 수가 줄기 때문에 실행 속도 자체는 향상한다. 이 옵션의 단점은 c++의 표준 입출력만 사용해야 하고, Thread safe하지 않게 된다는 점이다.<br/>
            마지막으로 이 옵션은 Thread safe하지 않는 이유 때문에 실무에서는 거의 사용할 일이 없다고 생각한다. 하지만 알고리즘 대회는 보통 Single thread 환경에서 개발이 진행되기 때문에 사용하는 옵션인 것 같다.<br/><br/>
            - cin.tie(NULL)<br/>
            cin.tie 옵션을 NULL로 설정하는 것은 cin을 cout으로부터 untie 하는것을 의미한다.<br/>
            stream을 tie하면 다른 stream에서 입출력 요청이 오기 전에 stream을 flash 시킨다.<br/>
            즉 tie 된 상태에서는 "입력값에 대한 안내문을 출력(cout)"하고 "사용자의 입력(cin)"을 기다리는 상황에서 출력(output buffer를 flush) 후 입력을 기다리는것을 의미한다.<br/>
            untie 된 상태에서는 "입력값에 대한 안내문을 출력(cout)"하고 "사용자의 입력(cin)"을 기다리는 상황에서 출력(output buffer를 flush)되지 않은 상태에서 입력을 기다리는것을 기다리게 된다.<br/>
            이 옵션과 관련되서 인지하고 있어야 하는 것은 아래와 같다.<br/>
            기본적으로 Output buffer가 가득차거나 수동으로 Output buffer를 flush하는 상황(std::endl 등)이 되지 않으면 출력되지 않는다.<br/>
            그러므로 cin과 cout을 untie하면, cin으로 입력을 받기 전에 cout 출력을 하고싶으면 명시적으로 cout buffer를 flush 해주어야 한다.<br/><br/>
        2. 언어적 특성에는 수 처리에 대한 이야기도 나온다. 이 부분에서는 변수의 오버플로우에 대한 이야기가 나오는데, 실제로 업무를 할때 long long 대신 int형으로 자료를 받아 쓰레기 값으로 처리되는 경우를 종종 보게 된다. 때문에 모든 변수를 처리할때 입력/출력/계산 과정에서 오버플로우가 나지 않는 넉넉한(?) 자료형을 사용해야 한다.<br/>
        그리고 실수부 부동 소수점에는 계산의 오차가 있기 때문에 == 연산자를 사용하는데 주의 해야 하는 말도 와닿는다.<br/>
        컴퓨터는 소수를 표현하기 위해 대표적으로 두가지 방법을 사용한다.<br/>
            - 고정소수점
            일정 비트는 정수값, 나머지 비트는 소수점 아래의 값을 저장하도록 하여 10진수 변환을 할 때 공간을 기준으로 변환처리를 한다.<br/>
            고정소수점은 정확도는 높지만 큰 수를 표현하기 위해서는 많은 메모리가 사용된다는 단점이 있다.
            - 부동소수점
            부동 소수점은 실수를 컴퓨터상에서 근사하여 표현할 때 소수점의 위치를 고정하지 않고, 그 위치를 나타내는 수를 따로 적은것으로 가수(유효숫자를 나타냄)와 지수(소수점의 위치를 풀이함)으로 나누워서 표현한다. 부동소수점에 대한 자세한 설명은 이곳에 적기는 어려우니 링크 걸어놓은 위키백과를 확인하길 바란다. : [부동소수점](https://ko.wikipedia.org/wiki/%EB%B6%80%EB%8F%99%EC%86%8C%EC%88%98%EC%A0%90#32%EB%B9%84%ED%8A%B8_%EC%BB%B4%ED%93%A8%ED%84%B0%EC%97%90%EC%84%9C%EC%9D%98_%EB%B6%80%EB%8F%99%EC%86%8C%EC%88%98%EC%A0%90_%EB%B0%A9%EC%8B%9D)<br/>
            개인적으로 부동소수점을 이해하기 어렵다면, C로 구현해보는것을 추천한다. 인도에서 공부할때 인도 강사가 입력받은 실수부를 부동소수점으로 변환하여 출력하는 콘솔 프로그램을 과제로 내준적이 있다. 이때 개념 자체를 이해하면 구현 자체는 쉬우나, 실수부를 double형으로 받으면 결과가 이상하게 틀어지는것을 볼 수 있다. 그 이유는 하나하나 찍어보면 알게 될 것이다.<br/><br/>
        3. 마지막으로 typedef로 자료형을 짧게 만드는 부분에 대한 이야기가 나오는데, 나는 이 부분에 대해서는 자료형을 짧게 만들어야 한다는 의견에는 반대한다.<br/>
        물론 긴 자료형을 쓰는 일은 귀찮은 일이지만, 긴 자료형을 typedef 처리 후 짧게 사용하다 보면 유지보수할때 실수가 발생할 수도 있기 때문이다.<br/>
        비슷한 이유로 매크로의 사용도 선호하지 않는다.<br/>
        매크로가 때에 따라서는 편하게 동작하기는 하지만, 전처리 과정에서 define 된 부분을 코드를 복사해놓기 때문에 실행파일 크기 자체가 늘어난다.<br/>
        또한 스택 프레임을 사용할 수 없기 때문에 재귀 구조를 가져갈 수 없다는 단점도 있다.<br/><br/>
    2. 재귀적 알고리즘
    재귀 함수는 DFS등의 알고리즘 기법을 사용 할 때 자주 사용하게 되는 기법이다.<br/>
    재귀함수 자체는 매우 편리하 방법이긴 하지만, 반대로 사용하기 까다로운 기법이다.<br/>
    그 이유는 재귀함수 탈출에 대한 룰이 엄격하게 정해지지 않으면 무한의 공간으로 빠질 수 있고, 또한 Stack overflow 에러를 발생할 수 있기 때문이다.<br/>
    그렇기 때문에 재귀 함수를 만들때는 항상 탈출 조건부터 먼저 정의하고 개발을 해야 한다.<br/>
    그리고 재귀함수를 사용하면 Thread 못지 않게 디버깅을 하기 매우 어렵다는 단점도 있다.(브레이크 포인트를 찍어도 역추적이 힘듦)<br/><br/>
    3. 비트 연산
    비트 연산은 개인적으로 시프트 연산과 마스크에서 자주 사용한다.<br/>
    Bit 연산의 가장 큰 장점은 적은 양의 메모리 사용으로 많은 정보를 담을 수 있고, 또 속도가 빠르다는 점이다.<br/>
    때문에 많은 양의 데이터를 사용해야 하는 환경에서 메모리를 아껴야 할 때, 그리고 임베디드 환경에서 많이 쓴다.<br/>
    다만 단점은 한번에 알아보기 힘들고 비트 연산 코드를 보면 한번 생각을 해야 이해를 할 수 있다는 점이다.<br/><br/>
3. 효율성
    1. 시간 복잡도
    시간 복잡도는 전공 과정에서 매우 짧게 배우지만 알고리즘을 풀 때는 강력한 힌트 중 하나다.<br/>
    보통 알고리즘 문제는 문제를 보고 구현을 하는 방식도 있지만, BFS, DFS, DP의 기법을 써서 풀어야 하는 문제도 많이 있다.<br/>
    특히 문제를 읽다 보면 "어? 이거 BFS, DFS 문제다" 라고 생각이 들지만 실제로는 BFS, DFS를 사용해서 풀면 Time over가 나는 경우가 많이 있었다.<br/>
    이를 방지하기 위해서는 입력값을 기준으로 어느정도의 복잡도가 나와야 이 문제가 풀리겠구나 역으로 힌트를 얻어야 한다.<br/>
    이 챕터 내용중 가장 마음에 들었던 나용은 아래와 같이 1초를 기준으로 입력의 크기와 추정 시간복잡도를 정리해주었다는 점이다.<br/>
    물론 이 복잡도가 무조건 이 시간을 보장하는것은 아니지만, 최소한 알고리즘 문제를 읽고 해법 구상을 할 때 충분히 도움을 받을 수 있는 점이기 때문에 알고리즘 문제 풀이에 꼭 필요한 개념이라고 생각한다.<br/>
        - n <= 10           O(n!)
        - n <= 20           O(2^n)
        - n <= 500          O(n^3)
        - n <= 5000         O(n^2)
        - n <= 10^6         O(nlongn) or O(n)
        - n이 매우 클때     O(1) or O(logn)<br/><br/>
    2. 예제문제
        - 최대 부분 배열 합
        이 문제는 연속된 배열의 방을 더한 수가 가장 큰 경우를 찾는 문제에 대한 설명이다.<br/>
        보통 깊은 생각을 하지 않고 문제를 읽으면 책에서 소개한대로 O(n^3)이나 O(n^2)의 경우로 문제를 생각하기 쉽다.<br/>
        하지만 이런 경우 보통 위의 복잡도로 문제를 풀게되면 Time over되는 경우가 많이 있다.<br/>
        때문에 O(n^3)이나 O(n^2)의 복잡도로 문제를 고민하고 코드를 작성 할 시간을 아껴서 문제를 좀 더 생각해보고 파해법을 찾느냐를 보는 문제인 것 같다.<br/>
        이런 문제의 핵심은 문제에서 "연속된"이라는 힌트를 주었기 때문에 한번 더 생각해볼 수 있는 기회가 있다고 생각한다.<br/>
        - 두 퀸 문제
        백트래킹에 대한 설명에 나온 문제와 같은 문제다. 그런데 점화식을 구해 O(1)로 문제를 푸는 방식을 왜 소개했는지 잘 모르겠다.(이해가 안감)
4. Code
    - 2.2 재귀적 알고리즘 : 부분집합 생성하기
    ```c++
    #include <iostream>
    #include <vector>

    std::vector<int> subset;
    int totalDepth;
    int nowCount;

    void Search(int nowDepth)
    {
        if (nowDepth == totalDepth + 1)
        {
            // Handling subsets -> Print
            std::cout << nowCount++ << (nowCount < 10? "  : " : " : ");
            if (subset.size() == 0)
            {
                std::cout << "Empty set";
            }
            else
            {
                for (auto item : subset)
                {
                    std::cout << item << " ";
                }
            }
            std::cout << std::endl;
        }
        else
        {
            // Include "depth" in the subset.
            subset.push_back(nowDepth);
            Search(nowDepth + 1);
            subset.pop_back();
            Search(nowDepth + 1);
        }
    }

    int main()
    {
        nowCount = 1;
        totalDepth = 0;

        std::cout << "Enter the Total depth of subset : ";
        std::cin >> totalDepth;

        Search(1);
        
        return 0;
    }
    ```    
    - 2.2 재귀적 알고리즘 : 순열 생성하기
    ```c++
    #include <iostream>
    #include <vector>

    #define MAX_INPUT_VAL 100 // Maximum number of arrays (specified arbitrarily)

    std::vector<int> permutation;
    bool chosen[MAX_INPUT_VAL];
    int inputVal;
    int nowCount;

    void Search()
    {
        if (permutation.size() == inputVal)
        {
            // Handling permutation -> Print
            std::cout << nowCount++ << (nowCount < 10 ? "  : " : " : ");
            for (auto item : permutation)
            {
                std::cout << item << " ";
            }
            std::cout << std::endl;
        }
        else
        {
            for (int index = 1; index <= inputVal; index++)
            {
                if (chosen[index])
                {
                    continue;
                }

                chosen[index] = true;
                permutation.push_back(index);
                Search();
                chosen[index] = false;
                permutation.pop_back();
            }
        }
    }

    int main()
    {
        memset(chosen, MAX_INPUT_VAL, false);
        inputVal = 0;
        nowCount = 1;

        std::cout << "Enter the Maximum number of permutation : ";
        std::cin >> inputVal;

        Search();

        return 0;
    }
    ```    
    - 2.3 재귀적 알고리즘 : 퇴각검색(백트레킹) - 퀸 배치 방법
    ```c++
    #include <iostream>

    #define MAX_ARRAY_INDEX 100 // Maximum number of arrays (specified arbitrarily)

    int inputVal;
    int count;
    int col[MAX_ARRAY_INDEX];
    int diag1[MAX_ARRAY_INDEX];
    int diag2[MAX_ARRAY_INDEX];

    void Search(int y)
    {
        if (y == inputVal)
        {
            count++;
            return;
        }

        for (int x = 0; x < inputVal; x++)
        {
            if (!col[x] || !diag1[x + y] || !diag2[x - y + inputVal - 1])
            {
                continue;
            }
            col[x] = diag1[x + y] = diag2[x - y + inputVal - 1] = 1;
            Search(y + 1);
            col[x] = diag1[x + y] = diag2[x - y + inputVal - 1] = 0;
        }
    }

    int main()
    {
        inputVal = 0;
        count = 0;
        memset(col, 0, MAX_ARRAY_INDEX);
        memset(diag1, 0, MAX_ARRAY_INDEX);
        memset(diag2, 0, MAX_ARRAY_INDEX);

        std::cout << "Enter the Number of Queen : ";
        std::cin >> inputVal;

        if (inputVal > 10 || inputVal < 4)
        {
            std::cout << "Out of range(4 ~ 10)" << std::endl;
            return 0;
        }

        Search(0);

        std::cout << "Result : " << count << std::endl;

        return 0;
    }
    ```
    - 3.2 예제문제 : 최대 부분 배열 합
    ``` c++
    #include <iostream>
    #include <algorithm>

    #define MAX_ARRAY_INDEX 100

    int main()
    {
        int count = 0;
        int myArray[MAX_ARRAY_INDEX] = { 0 };
        int best = 0, sum = 0;

        std::cout << "Input number of array : ";
        std::cin >> count;

        std::cout << "Input data of array : ";
        for (int index = 0; index < count; index++)
        {
            std::cin >> myArray[index];
        }


        for (int index = 0; index < count; index++)
        {
            sum = std::max(myArray[index], sum + myArray[index]);
            best = std::max(best, sum);
        }

        std::cout << best << std::endl;

        return 0;
    }
    ```
