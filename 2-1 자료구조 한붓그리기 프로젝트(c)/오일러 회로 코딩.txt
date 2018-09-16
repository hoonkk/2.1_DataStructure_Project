#include <stdio.h> 
#define VERTEX 4// 정점의 개수
#define EDGE 6// 간선의 개수
#define START 0//시작점(첫번째 정점으로부터 시작하기 위해)

int success; // 경로 파악 성공 여부
int vtxstack[EDGE + 1]; // 지나가고 있는 간선을 저장할 스택
int n; // 통과한 간선

int a[VERTEX][VERTEX] =
{
	{ 0,1,0,1 },
	{ 1,0,1,2 },
	{ 0,1,0,1 },
	{ 1,2,1,0 }
};

void FindCircuit(int i)
{
	int k;
	vtxstack[n] = i; // 시작점을 찾기 위하여 지정.
	if (n == 0 && i==START) // i의 값, 즉 현재 시작하는 점이 시작부분이라면
	{
		printf("해 %d : ", ++success);
		for (k = 0; k <= EDGE; k++)
			printf("%d ", vtxstack[k]+1);
		printf("\n");
	}
	else
	{
		for (k = 0; k < VERTEX; k++)
		{
			if (a[i][k] != 0) // 간선 존재 여부 판단 ( 간선이 존재한다면! )
			{
				a[i][k]--;    a[k][i]--;
				n--;
				FindCircuit(k);
				a[i][k]++;    a[k][i]++;
				n++;
			}
		}
	}
}

int main()
{
	success = 0; 
	n = EDGE;
	FindCircuit(START);
	if (success == 0)
		printf("오일러 경로가 존재하지 않습니다.\n");
}