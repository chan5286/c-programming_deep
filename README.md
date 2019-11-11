# c-programming_deep

### 리스트

* 리스트의 특징

1. 데이터를 나란히 저장하며 중복된 데이터의 저장이 가능한 자료구조

2. 스택, 큐, 덱과 같은 선형 자료구조

3. 구현 방법에 따라 배열 리스트와 연결 리스트로 나뉨

* 리스트의 종류

1. Array List : 배열을 기반으로 구현한 리스트

2. Linked List : 메모리 동적 할당을 기반으로 구현한 리스트

* 예시코드

#include <stdio.h>
#include <stdlib.h>
typedef struct list {
 int d;
 struct list* p;
} LIST;
LIST* root = NULL;
LIST* last = NULL;
int main(void){
 LIST* r = (LIST*)malloc(sizeof(LIST));
 r->d = 35;
 r->p = NULL; 
 root = r;
 last = r;
 
 r = (LIST*)malloc(sizeof(LIST));
 last->p = r;
 r->d = 40;
 r->p = NULL;
 last = r;
 
 r = (LIST*)malloc(sizeof(LIST));
 last->p = r;
 r->d = 45;
 r->p = NULL;
 last = r;
 
 while(root){
  printf("%d\n", root->d);
  root = root->p;
 }
}

### 트리

* 트리의 특징

1. 루트노드로부터 노드들이 이어지는 방식으로 구성.

2. 반드시 두 개의 노드 사이에 한 경로밖에 존재하지 않기 때문에 하나의 노드는 하나의 노드를 가리킬 수밖에 없음.

* 트리의 종류

1. 이진트리

 -1 완전이진트리

 -2 포화이진트리

 -3 편향이진트리

 -4 정이진트리

2. 이진탐색트리

* 예시코드

#include <stdlib.h>    
typedef struct Tree {
    struct Tr *l, *r;
    int d;
} T;
void print(T* p){
   printf("%d\n", p->d);
   if(p->l) print(p->l);
   if(p->r) print(p->r);    
}
T* mem(){
 T* p=(T*)malloc(sizeof(T));
 p->l=p->r=NULL;
 return(p);
}
int main(void){
    T *r, *r1, *r2, *l1;
    l1= (T*)mem(); l1->d=3; 
    r2= (T*)mem(); r2->d=8; 
    r1= (T*)mem(); r1->d=7; r1->r=r2;
    r= (T*)mem(); r->d=5; r->l=l1;  r->r=r1;
    print(r);
}

### 그래프

* 그래프의 특징

1. vertex와 edge로 이루어진 한정된 자료구조

2. vertex는 정점을 의미하고 edge는 정점과 정점을 연결하는 간선을 의미

* 그래프의 종류

1.방향그래프

2.무방향그래프

* 예시코드

#include <stdio.h>
#include <stdlib.h>
#include <memory.h>
 
typedef struct{
    int vn; 
    int **matrix;
} Graph;
 
 
Graph *NewGraph(int max_vertex);
void DeleteGraph(Graph *graph);
void AddEdge(Graph *graph, int start, int goal);
void ViewGraph(Graph *graph);
void ViewIndegree(Graph *g);
void ViewOutdegree(Graph *g);
 
int main(void)
{        
    Graph *graph;
    graph = NewGraph(6);
    AddEdge(graph, 0, 1);
    AddEdge(graph, 3, 1);
    AddEdge(graph, 2, 4);
    AddEdge(graph, 4, 2);
    ViewGraph(graph);
    ViewIndegree(graph); 
    ViewOutdegree(graph);  
    DeleteGraph(graph);
    return 0;    
}
 
Graph *NewGraph(int max_vertex)
{
    int i = 0;
    Graph *graph = (Graph *)malloc(sizeof(Graph));
    graph->vn = max_vertex;
    graph->matrix = (int **)malloc(sizeof(int *)*max_vertex);
    for (i = 0; i < max_vertex; i++)
    {
        graph->matrix[i] = (int *)malloc(sizeof(int)*max_vertex);
        memset(graph->matrix[i], 0, sizeof(int)*max_vertex);
    }
    return graph;
}
void DeleteGraph(Graph *graph)
{
    int i = 0;
    
    for (i = 0; i < graph->vn; i++)
    {
        free(graph->matrix[i]);
    }
    free(graph->matrix);
    free(graph);
}
void AddEdge(Graph *graph, int start, int goal)
{
    graph->matrix[start][goal] = 1;
}
void ViewGraph(Graph *graph)
{
    int i =0;
    int j =0;
    for(i=0;i<graph->vn;i++)
    {
        printf("%d 에서 갈 수 있는 정점:",i);
        for(j=0;j<graph->vn;j++)
        {
            if(graph->matrix[i][j])
            {
                printf("%d ",j);
            }
        }
        printf("\n");
    }
}
void ViewIndegree(Graph *g)
{
    int i, j;
    int degree;
    printf("In-degree\n");
    for (i = 0; i < g->vn; i++)
    {
        degree = 0;
        for (j = 0; j < g->vn; j++)
        {
            if (g->matrix[j][i])
            {
                degree++;
            }
        }
        printf("%d ", degree);
    }
    printf("\n");
 
}
void ViewOutdegree(Graph *g)
{
    int i, j;
    int degree;
    printf("Out-degree\n");
    for (i = 0; i < g->vn; i++)
    {
        degree = 0;
        for (j = 0; j < g->vn; j++)
        {
            if (g->matrix[i][j])
            {
                degree++;/
            }
        }
        printf("%d ", degree);
    }
    printf("\n");
}

### 소감
 이번 과제를 통해서 수업시간에 조금 이해하기 힘들었던 자료구조에 대해 더 깊이 알아볼 수 있었습니다. 이후의 기말고사에서
더 좋은 성적을 받기 위해서라도 리스트와 트리에 대해 완벽하게 외우겠습니다.
