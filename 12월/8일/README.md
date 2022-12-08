# TIL

https://school.programmers.co.kr/learn/courses/30/lessons/118667

 
프로그래머스

코드 중심의 개발자 채용. 스택 기반의 포지션 매칭. 프로그래머스의 개발자 맞춤형 프로필을 등록하고, 나와 기술 궁합이 잘 맞는 기업들을 매칭 받으세요.

programmers.co.kr
새롭게 알게 된 것

벡터 원소 더하기

#include <numeric>

accumulate(v.begin(), v.end(), 0);

삽질을 많이 했다.

첫번째는 큐 1과 큐 2 내에서 절반이 있는 경우를 찾고 그다음은 이어져서 있는 경우를 찾으려고 했는데

복잡하고 매번 합을 구해야 해서(O(n)) 시간 초과가 났다. 

그래서 sum을 미리 구하고 빼고 더하는 방식(O(1))으로 바꾸려고 했는데 

모든 경우의수를 구해서 절반이 되는지 체크하는 방식으로 하니까 복잡해진 것 같다.

정답 풀이

더 큰 큐의 원소를 빼서 더 작은 원소의 큐로 넣어주면 처음 답을 찾은 것이 최소가 되기 때문에 이렇게 해야한다.참고한 블로그는 빼고 더해줄 때마다 cnt를 증가해주었다. 나는 여기다가 index를 이용해서 정답을 계산해 보았다.


참고 한 블로그

https://velog.io/@jiyehyeon/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EB%91%90-%ED%81%90-%ED%95%A9-%EA%B0%99%EA%B2%8C-%EB%A7%8C%EB%93%A4%EA%B8%B0

 
[프로그래머스] 두 큐 합 같게 만들기 (C++)

프로그래머스 Lv2. 두 큐 합 같게 만들기

velog.io
참고해서 푼 풀이

#include <string>
#include <vector>
#include <numeric>
using namespace std;

int solution(vector<int> queue1, vector<int> queue2) {
    int answer = -2;
    int size1=queue1.size();
    int size2=queue2.size();
    
    long long sum1=accumulate(queue1.begin(), queue1.end(), 0);
    long long sum2=accumulate(queue2.begin(), queue2.end(), 0);
    int index1=0,index2=0;
    long long sum=sum1+sum2;
    if(sum%2)
        return -1;
    int temp=0;
    int cnt=0;
    while(cnt<size1+size2+10)
    {
        if(sum1==sum2)
        {
            return cnt;   
        }
        else{
        if(sum1>sum2)
        {
            temp=index1<size1 ?queue1[index1]:queue2[index1-size1];
            index1++;
            sum1-=temp;
            sum2+=temp;
            cnt++;
        }
        else
        {
            temp=index2<size2 ?queue2[index2]:queue1[index2-size2];
            index2++;
            sum2-=temp;
            sum1+=temp;
            cnt++;
        }
        }
    }
    
    return -1;
}
cnt 안쓰고 index 활용하게 고친 풀이

#include <string>
#include <vector>
#include <numeric>
using namespace std;

int solution(vector<int> queue1, vector<int> queue2) {
    int answer = -2;
    int size1=queue1.size();
    int size2=queue2.size();
    int size=size1+size2+10;
    long long sum1=accumulate(queue1.begin(), queue1.end(), 0);
    long long sum2=accumulate(queue2.begin(), queue2.end(), 0);
    int index1=0,index2=0;
    long long sum=sum1+sum2;
    if(sum%2)
        return -1;
    int temp=0;
    
    while(size--)
    {
        if(sum1==sum2)
        {
            
            return (index1+index2);   
        }
        else{
        if(sum1>sum2)
        {
            temp=index1<size1 ?queue1[index1]:queue2[index1-size1];
            index1++;
            sum1-=temp;
            sum2+=temp;
           
        }
        else
        {
            temp=index2<size2 ?queue2[index2]:queue1[index2-size2];
            index2++;
            sum2-=temp;
            sum1+=temp;
           
        }
        }
    }
    
    return -1;
}
삽질 코드

#include <stdio.h>
#include <stdbool.h>
#include <stdlib.h>

// queue1_len은 배열 queue1의 길이입니다.
// queue2_len은 배열 queue2의 길이입니다.
int solution(int queue1[], size_t queue1_len, int queue2[], size_t queue2_len) {
    long long answer = 9000000;
    int temp=0;
    int size=queue1_len+queue2_len;
    long long sum=0,sum1=0,sum2=0;
    bool check=false;
    long long half=0;
    for(int i=0;i<queue1_len;i++)
        sum1+=queue1[i];
    for(int i=0;i<queue2_len;i++)
        sum2+=queue2[i];
     sum=sum1+sum2;
     half=sum/2;  
  //  printf("half :%d",half);
        
//    for(int k=0;k<size;k++)
//    {
//        //queue1
//       for(int i=k;i<queue1_len;i++) {
//            temp+=queue1[i];
//            if(temp==15)
//            {//횟수 구하기

//             //최솟값 비교
//            }
//            else if(temp>15)
//            {
//                //다시
//                temp=0;
//                break;
//            }
//       }
//        //queue2
//        for(int j=0;j<queue2_len;j++){
//         temp+=queue1[i];
//            if(temp==15)
//            {//횟수 구하기

//             //최솟값 비교
//            }
//            else if(temp>15)
//            {
//                //다시
//                temp=0;
//                break;
//            }
        
//     }
//    }   
    //queue1안에서 절반 되는 경우
    int sumT=sum1;
    for(int i=0;i<queue1_len;i++)
    {
        for(int j=queue1_len-1;j>i;j--)
        { 
            sumT-=queue1[j];
            if(sumT==half)
           {//횟수 구하기
                check=true;
                temp=(j+1)+queue2_len+i;
            //최솟값 비교
               if(temp<answer)
               {
                   answer=temp;
               }
           }
          
        }
        sumT=sum1-queue1[i];
    }
    //queue2안에서 절반 되는 경우
    sumT=sum2;
    for(int i=0;i<queue2_len;i++)
    {
        for(int j=queue2_len-1;j>i;j--)
        { 
            sumT-=queue2[j];
            if(sumT==half)
           {//횟수 구하기
                check=true;
                temp=(j+1)+queue1_len+i;
            //최솟값 비교
               if(temp<answer)
               {
                   answer=temp;
               }
           }
          
        }
        sumT=sum1-queue2[i];
    }
    
//     for(int i=0;i<queue1_len;i++)
//     {
//         //sum=0;
//         for(int j=i;j<queue1_len;j++){
//          sumT+=queue1[i];
         
//            if(sum==half)
//            {//횟수 구하기
//                 check=true;
//                 temp=(j+1)+queue2_len+i;
//             //최솟값 비교
//                if(temp<answer)
//                {
//                    answer=temp;
//                }
//            }
//            else if(sum>half)//다시
//                break;
//         }
//     }   
//     //queue2안에서 15가 되는 경우
//     for(int i=0;i<queue2_len;i++)
//     {
//         sum=0;
//         for(int j=i;j<queue2_len;j++){
//          sum+=queue2[j];
//            if(sum==half)
//            {//횟수 구하기
//                check=true;
//                 temp=(j+1)+queue1_len+i;
//             //최솟값 비교
//                if(temp<answer)
//                {
//                    answer=temp;
//                }
//            }
//            else if(sum>half)//다시
//                break;
//         }
//     }   
    //queue1과 queueu2가 이어지는 경우
//     for(int i=0;i<queue1_len;i++)
//     {
//         sum=0;
//         for(int j=i;j<queue1_len;j++)
//         {
//             sum+=queue1[j];
//            if(sum==half)//이어져야 하므로
//                break;
//         }
//         for(int j=0;j<queue2_len;j++)
//         {
//             sum+=queue2[j];
//            if(sum==half)
//            {
//                check=true;
//                //횟수 구하기
//                temp=(i)+(j+1);
//                // printf("temp%d", temp);
//                // printf("i : %d %d", i,j);
//                //최솟값 비교
//                if(temp<answer)
//                    answer=temp;
//            }
//            else if(sum>half)//다시
//                break;
          
//         }
//     }
    // if(!check)
    //     answer=-1;
    // if(answer>size)
    //     answer=-1;
   
    return answer;
}
