---
layout:single
title:"greedy"
date:2020-04-26

---

# 그리디알고리즘





**그리디 알고리즘이란?**

(,탐욕,욕심쟁이 알고리즘, Greedy Algorithm)이란 "매 선택에서 **지금 이 순간 당장 최적인 답**을 선택하여 적합한 결과를 도출하자" 라는 모토를 가지는 알고리즘 설계 기법



예를 들어 설명하면  5개의 도시를 모두 한번씩만 거쳐서 여행하는 경로 중 기름값을 아끼기 위해 가능하면 짧은 경로를 이용하고 싶다고 가정하자.                                        1



이 문제를 해결하기 위해 몇가지 전략을 사용할 수 있다. 

오래걸리지만 가능한 120가지의 조합을 모두 살펴봐서 그중 가장 짧은 경로를 선택하는 것도 하나의 전략이 될 것이다. 

그러한 다양한 방법 중, 그리디 알고리즘을 사용한다는 것은 "지금 내가 있는 도시에서 고를 수 있는 도로 중 가장 짧은 도로를 선택한다"라는 방법이 될 수 있다.

**단, 그리디 알고리즘을 사용하면 매 선택이 그 순간에 대해서는 최적이지만 그걸 종합적으로 봤을 땐 최적이라는 보장은 절대 없다는 것을 명심해야 한다.** 

매 만약 순간 최적을 따라가면 1-1-1-100라는 순서로 가는데, 중간에 1-1-10-10으로 움직이는 것이 전체적으로 더 짧은 길이 될 수 있으니 말이다.



그러므로 **장단점은 효율적이긴하나 최적해를 보장해주지 못한다는 것이다.**



# 문제

### **그리디 알고리즘 사용 예시**

- AI에 있어서 결정 트리 학습법(Decision Tree Learning)
- 활동 선택 문제(Activity selection problem)
- **거스름돈 문제**
- 최소 신장 트리 (Minimum spanning tree)
- 제약조건이 많은 대부분의 문제
- [다익스트라 알고리즘](https://blog.tomclansys.com/63)
- 하프만 코딩
-  크러스컬 알고리즘

등 그리디알고리즘을  대표하는 문제들이있다 

이중 거스름돈 문제를 보도록 하자!

**최소동전의 수를 알고 싶다면?**

간단히 소스코드를 작성해보았다.

	public static void main(String[] args) {
		Scanner scanner= new Scanner(System.in);
	 
		int W;
		System.out.print("입력값");
		int n =scanner.nextInt();
		int target = scanner.nextInt();
		int result=0;//
		int[] coin = new int[5];
		W=n-target;
		System.out.print(" 잔돈은"+ W+"" + "원입니다. ");
		while(W>=500)
		{
			W=W-500;
			coin[0]++;
		}
		
		while(W>=100)
		{
			W=W-100;
			coin[1]++;
		}
		
		while(W>=50)
		{
			W=W-50;
			coin[2]++;
		}
		
		while(W>=10)
		{
			W=W-10;
			coin[3]++;
		}
		
		while(W>=1)
		{
			W=W-1;
			coin[4]++;
		}
		result=coin[0]+coin[1]+coin[2]+coin[3]+coin[4];
		System.out.print("500원의 갯수=" + coin[0]+" ");
		
		System.out.print("100?원의 갯수=" + coin[1]+" ");
		
		System.out.print("50원의 갯수=" + coin[2]+" ");
		
		System.out.print("10원의 갯수=" + coin[3]+" ");
		
		System.out.print("1원의 갯수=" + coin[4]+" ");
		
		System.out.print("최소동전의수는="+ result);
		scanner.close();
	}

생각해보자

 큰가치의 화폐로 최대하 계산면 동전의 수가 작아질것이다

각 while문안에 있는 내용을 보면 지정 화폐단위로 계산할수있는 최대값까지 계산하고

남은값은 한 단계 작은화폐단위계산으로넘어간다. 

![](C:\Users\User\Pictures\캡처.PNG)