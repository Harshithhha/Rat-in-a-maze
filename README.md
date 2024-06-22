# Rat-in-a-maze
```
#include<stdio.h>
#include<stdlib.h>
//we maintain 3 2-D arrays 
//1.Maze
//2.Stack for temporary storage
//3.paths for finalized path where we only push no pop operation is required 

int stack[100][2]={0};
int top=-1,stop=-1;
int paths[100][2];
int maze[10][10]={
	{1,1,0,1,0,1,0,0,1,0},
	{0,1,1,1,0,0,1,0,0,0},
	{0,1,1,0,1,0,0,1,0,0},
	{0,1,1,1,1,0,0,0,0,0},
	{0,1,0,0,0,1,0,0,0,1},
	{0,1,0,0,0,1,0,0,1,0},
	{0,1,1,1,1,1,0,1,0,0},
	{0,1,0,0,0,1,1,0,1,0},
	{0,0,1,0,0,0,1,0,0,0},
	{0,1,0,1,0,0,1,1,1,1}
	};
int visitedmaze[10][10]={0};
int posx=0,posy=0,n;
int flag=0;
void spush(int px,int py)
{
	stop=stop+1;
	paths[stop][0]=px;
	paths[stop][1]=py;

}
void push(int px,int py)
{
	top=top+1;
	stack[top][0]=px;
	stack[top][1]=py;

}
void pop()	
{
	int dummyx,dummyy;
	
	posx=stack[top][0];
	posy=stack[top][1];
	top--;

}
void path()
{
	
	int i=0;
	
	if(stop>=0)
	{
		printf("\n path followed:\n");
	while(i<=stop)
	{
		printf("(%d,%d)",paths[i][0],paths[i][1]);
		if(i!=stop) printf("-->");
		i++;
	}
    }
    else 
      printf("NO path found!!");
}
void print(int maze[n][n])
{
	int i=0,j;
	for(i=0;i<n;i++)
	{
			for(j=0;j<n;j++)
		{
	
			printf("%d ",maze[i][j]);
		}
		printf("\n");
	}
}
void createmaze()
{
	print(maze);
	}

void mdown()
{
	int dposx=posx+1;
	push(dposx,posy);
	
}
void mright()
{
	int dposy=posy+1;
	push(posx,dposy);
}
void mleft()
{
	int dposy=posy-1;
	push(posx,dposy);
}
void mup()
{
	int dposx=posx-1;
	push(dposx,posy);
}


void traverse(int dx,int dy)
{
	int i,j;
	//initially pushing the starting position i.e (0,0) we can also change 
	push(posx,posy);
	
		
  while(top != -1&&(posy!=dy||posx!=dx))
  {
     pop();
    
     if(visitedmaze[posx][posy]==1)
     	visitedmaze[posx][posy]=0;
     	//to avoid a case where it needs to backtrack and change its path 
     else{
	 if (maze[posx+1][posy]==1 && visitedmaze[posx+1][posy]==0 )
     	push(posx+1,posy);
     if (maze[posx][posy+1]==1 && visitedmaze[posx][posy+1]==0 )
     	push(posx,posy+1);
     visitedmaze[posx][posy]=1;
     spush(posx,posy);
     
    
      if(maze[posx+1][posy]==1&&visitedmaze[posx+1][posy]==0)
      {
		mdown();
      }
     
      if(maze[posx-1][posy]==1&&visitedmaze[posx-1][posy]==0)
      {
		mup();
      }
     
	  if(maze[posx][posy+1]==1&&visitedmaze[posx][posy+1]==0)
      {
		mright();
      }
    
	  if(maze[posx][posy-1]==1&&visitedmaze[posx][posy-1]==0)
      {
		mleft();
      }
       
}
  }
  /*
	for(i=0;i<n;i++)
	{
			for(j=0;j<n;j++)
		{
	
			printf("%d ",visitedmaze[i][j]);
		}
	
	}*/
  
}
	

int main()
{
	int dx,dy;
	printf("enter the size of maze\n");
	scanf("%d",&n);
	createmaze();
	printf("enter the postion of food\n");
	scanf("%d %d",&dx,&dy);
	if (maze[dx][dy]!=0)
		traverse(dx,dy);
	if (top!= -1)
	path();
	else
	printf("No path found");
	return 0;
}
```
