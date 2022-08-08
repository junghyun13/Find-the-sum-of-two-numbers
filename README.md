# Find-the-sum-of-two-numbers
# python
# It receives N numbers and receives the desired number x. Let's find the number of ways to get x by adding 2 out of N numbers! N개의 숫자를 입력받고 원하는 숫자 x를 입력받는다. N개의 숫자들 중 2개를 더해서 x가 되는 경우의 수를 구해보자!
N=int(input())
num=sorted(list(map(int,input().split())))
x=int(input())
left=0
right=N-1
answer=0
while left<right:
    temp=num[left]+num[right]
    if temp==x:
        answer+=1
        left+=1
    elif temp<x:
        left+=1
    elif temp>x:
        right-=1
print(answer)
# c program
#include <stdio.h>
#include <stdlib.h>
void quickSort(int *,int,int);
int inPlacePartition(int *,int,int,int);
int search(int *,int,int);
int main(void){
	int n;
	int x;
	int *arr;
	int temp;
	int i;
	int count=0;
	scanf("%d",&n); //원하는 개수 입력  
	arr=(int *)malloc(sizeof(int)*n); //동적메모리  
	for(i=0;i<n;i++){
		scanf("%d",arr+i); //아무런 n개의 값을 입력  
	}
	scanf("%d",&x); //두개의 함수를 더해서 나와야하는 값  
	quickSort(arr,0,n-1);
	for(i=0;i<n;i++){
		temp=search(arr,n-1,x-arr[i]);
		if(temp!=-1){
			if(arr[i]<temp){
				count++;
			}
		}
	}
	printf("%d",count);
	return 0;
}
void quickSort(int *arr,int l,int r){
	int a,b;
	if(l>=r)
	  return;
	a=b=inplacePartition(arr,l,r,r);
	quickSort(arr,l,a-1);
	quickSort(arr,l+1,r);
}
int inplacePartition(int *arr,int l,int r,int k){
	int p=arr[k];
	int temp;
	int i,j;
	p=arr[k];
	temp=arr[k];
	arr[k]=arr[r];
	arr[r]=temp;
	i=l;
	j=r-1;
	while(i<=j){
		while(i<=j&&arr[i]<=p){
			i++;
		}
		while(j>=i&&arr[j]>=p){
			j--;
		}
		if(i<j){
			temp=arr[i];
			arr[i]=arr[j];
			arr[j]=temp;
		}
	}
	temp=arr[i];
	arr[i]=arr[j];
	arr[j]=temp;
	return i;
}
int search(int *arr,int n,int x){
	int l=0;
	int r=n;
	int m;
	while(l<=r){
		m=(r+l)/2;
		if(x==arr[m])
		  return arr[m];
		if(arr[m]<x)
		  l=m+1;
		else
		  r=m-1; 
	}
	return -1;
}
#input--> 9  5 12 7 10 9 1 2 3 11  13
#result--> 3 (1+12,2+11,3+10)
