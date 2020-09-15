## K번째수

### Reference  
 - 프로그래머스 : https://programmers.co.kr/learn/courses/30/lessons/42748?language=java
 - 위키백과 : https://ko.wikipedia.org/wiki/%ED%80%B5_%EC%A0%95%EB%A0%AC

### 문제
<img src = "https://user-images.githubusercontent.com/40849381/93227050-f41af900-f7ae-11ea-907b-c3c9605b86b4.png"/>
 <br><br>

- java
 ```java
  public static int[] solution(int[] array, int[][] commands) {
    int[] answer = new int[commands.length];

    for (int i = 0; i < commands.length; i++) {
      int[] temp = Arrays.copyOfRange(array, commands[i][0] - 1, commands[i][1]);
      Arrays.sort(temp);
      answer[i] = temp[commands[i][2] - 1];
    }
    return answer;
  }
```
- 처음에 간단하게 api를 사용하여 구현하였으나 의미가 없다고 판단하여 
배열을 자르는 것과 sort함수를 구현해서 해보았다.
- Quick Sort 사용
  1. 퀵정렬은 임의의 pivot 값을 기준으로 pivot 의 좌측에는 pivot 보다 작은값을 두고 우측에는 pivot 보다 큰 값을 두고자 한다.
  2. 이 행위는 pivot을 기준으로 좌 우로 이분화 된 리스트를 재귀적으로 반복했을 때 결국 정렬이 완성 된다는 방법 론이다.
  3. 보다 쉽게 설명하면 pivot보다 큰 값을 pivot index 보다 왼쪽에서 찾고 ( 큰 값 이 나타날 때까지 i index 를 증가시키도록 한다.)
  4. pivot 보다 작은 값을 pivot index 보다 오른쪽에서 찾는다 ( 작은 값이 나타날 때까지 j index를 감소시키도록 한다. )
  5. pivot을 기준으로 값 비교가 완료되었다면 index 결과 i , j 를 비교 해본다.
  6. i 값이 j 값 보다 작거나 같다면 분명 pivot 을 기준으로 교환을 해야할 값이 있다는 뜻이 된다.
  7. 교환한 뒤 i 인덱스는 증가 j 인덱스는 감소 연산을 수행한다.
  8. i 인덱스가 j 인덱스보다 작거나 같다면 계속 반복해서 수행한다.
  9. 위 와 같은 과정은 pivot을 기준으로 왼쪽으로 정렬된 list 에서는 최초 Left 값이 감소된 j 보다 작다면 계속 재귀하면되고,
  10. pivot을 기준으로 오른쪽으로 정렬된 list 에서는 최초 Right 값이 증가된 i 값보다 크다면 계속 재귀하면된다.
 
 - java 
 ```java
  public static int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];

          for (int i = 0; i < commands.length; i++) {
                   int start = commands[i][0], end = commands[i][1], k = commands[i][2], index = 0;
                   int[] temp = new int[end - start + 1];

            for (int j = start - 1; j < end; j++) {
                temp[index++] = array[j];
            }
            quickSort(temp,0,temp.length - 1);
            answer[i] = temp[k - 1];
        }
        return answer;
    }
    static void quickSort(int[] data, int start, int end) {
        if (start >= end) return;
        int key = start;
        int i = start + 1, j = end, temp;
        while (i <= j) {
            while (i <= end && data[i] <= data[key]) {
                i++;
            }
            while (j > start && data[j] > data[key]) {
                j--;
            }
            if (i > j) {
                temp = data[j];
                data[j] = data[key];
                data[key] = temp;
            }
            if (i < j) {
                temp = data[j];
                data[j] = data[i];
                data[i] = temp;
            }
        }
        quickSort(data, start, j - 1);
        quickSort(data, j + 1, end);
    }
```