#include <iostream>
#include <locale>
#include <cstdlib>
#include <stdio.h>




using namespace std;

int             LT(int a, int b)
{
    return a < b;
}

void            MMERGE(int A[],int B[], size_t l, size_t m, size_t r)
{
    size_t          i = l;
    size_t          j = m + 1;
    size_t          k = l;
    /* Put the smallest thing into array B */
    while ((i <= m) && (j <= r)) {
        if (LT(A[i], A[j]))
            B[k++] = A[i++];
        else
            B[k++] = A[j++];
    }
    /* Copy leftover (if any) */
    while (i <= m) {
        B[k++] = A[i++];
    }
    while (j <= r) {
        B[k++] = A[j++];
    }
    /* Transfer back to original array */
    for (k = l; k <= r; k++) {
        A[k] = B[k];
    }
}
void            MSORT(int A[],int B[], size_t l, size_t r)
{
    size_t          m;          /* The middle */
    if (l < r) {                /* Cut problem to half size until 1 unit */
        /* Divide partition by 2, sort and merge */
        m = ((l + r) >> 1);
        MSORT(A, B, l, m);
        MSORT(A, B, m + 1, r);
        MMERGE(A, B, l, m, r);  /* A single element is ordered */
    }
}
//пирамидальная сортировка

int             LT(int & a, int & b)
{
    return a < b;
}
int             GT(int & a, int & b)
{
    return a > b;
}
void            SWAP(int & a, int & b)
{
   int           tmp = a;
    a = b;
    b = tmp;
}
void            PERCDOWN(int A[], int i, int N)
{
    int             Child;
    int           Tmp;

    for (Tmp = A[i]; LeftChild(i) < N; i = Child) {
        Child = LeftChild(i);
        if (Child != N - 1 && GT(A[Child + 1], A[Child]))
            Child++;
        if (LT(Tmp, A[Child]))
            A[i] = A[Child];
        else
            break;
    }
    A[i] = Tmp;
}

void            HEAPSORT(int A[], int N)
{
    int             i;

    for (i = N / 2; i >= 0; i--)
        /* BuildHeap */
        PERCDOWN(A, i, N);
    for (i = N - 1; i > 0; i--) {
        SWAP(A[0], A[i]);
        /* DeleteMax */
        PERCDOWN(A, 0, i);
    }
}

//линейные вставки
int             GT(int & a, int & b)
{
    return a > b;
}


void            LINEARINSERTION(int a[], unsigned long n)
{
    unsigned long   i,
                    j;
   int          tmp;

    for (i = 1; i < n; i++)     /* look for insertion point. */
        for (j = i; j > 0 && GT(a[j - 1], a[j]); j--) {
            /* Move the others down and insert it. */
            tmp = a[j];
            a[j] = a[j - 1];
            a[j - 1] = tmp;
        }
}
//метод пузырька 
void puz(int a[], int n) {
	for (int i = n-1; i >=0; i--) {
		for (int j = 0; j < i; j++) {
			if (a[j] > a[j+1]) {
				int temp = a[j];
				a[j]=	a[j + 1] ;
				a[j + 1] = temp;
			}
		}
	}
}
void vivod(int *ar, int n) {
	for (int i = 0; i < n; i++) {
		cout << ar[i] << endl;
	}
}
int main()

{ setlocale (LC_ALL,"RUS");
int  n,l=0;
cout<<"Введите размер массива"<<endl;
cin>>n;
int r=n-1;
    int *ar= new int[n];
     int *B= new int[n];

for (int i=0;i<n; i++)
{
    ar[i]=rand()%100;

}
 cout<<"не отсортированный массив"<<endl;
for (int i=0;i<n; i++)
{
    cout<<ar[i]<<endl;
}
 MSORT(ar,B,  l,  r);
   cout<<"Отсортированный массив"<<endl;
for (int i=0;i<n; i++)
{
    cout<<ar[i]<<endl;
}


    return 0;
}
