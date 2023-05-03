# test_5_3
#include <stdio.h>
//字符串的模式匹配
//朴素模式匹配
//顺序存储
#define MAXLEN 255
typedef struct{
	char ch[MAXLEN];
	int length;
}SString;
//堆分配存储
typedef struct{
	char *ch;
	int length;
}HString;
//链式存储
typedef struct StringNode{
	char ch;
	struct StringNode* next;
}StringNode,*String;
//基本操作
bool SubString(SString &Sub,SString S,int pos,int len)
{
	if(pos+len-1>S.length)
		return false;
	for(int i=pos;i<pos+len;i++)
		Sub.ch[i-pos+1] = S.ch[i];
	Sub.length = len;
	return true;
}
//串的比较
int Strcompare(SString S,SString T)
{
	for(int i=1;i<S.length && i<T.length;i++)
	{
		if(S.ch[i] != T.ch[i])
			return S.ch[i]-T.ch[i];
	}
	return S.length - T.length;
}
//定位操作
int Index(SString S,SString T)
{
	int i=1,n=Strlength(S),m=Strlength(T);
	SString Sub;
	while(i<=n-m+1)
	{
		SubString(Sub,S,i,m);
		if(Strcompare(Sub,T) != 0)
			++i;
		else
			return i;
	}
	return 0;
}

int Index(SString S,SString T)
{
	int i=1,j=1;
	while(i<=S.length && j<=T.length)
	{
		if(S.ch[i] == T.ch[j])
		{
			i++;
			j++;
		}
		else
		{
			i=i-j+2;
			j=1;
		}
	}
	if(j>T.length)
		return i-T.length;
	else
		return 0;
}
//KMP算法
int Index(SString S,SString T,int next[])
{
	int i=1,j=1;
	while(i<=S.length && j<=T.length)
	{
		if(j==0 || S.ch[i] == T.ch[j])
		{
			i++;
			j++;
		}
		else
		{
			j=next[j];
		}
	}
	if(j>T.length)
		return i-T.length;
	else
		return 0;
}
int main()
{

	SString S,T;
	Strlength(S,T);
	return 0;
}
