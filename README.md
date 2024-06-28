#include <iostream>
#include <algorithm>

using namespace std;

int n;
char a[20][20];

bool isSafe(int row,int col)
{
    for(int i=1;i<=row;i++)
    {
        if(a[i][col]=='Q')
        {
            return false;
        }
    }

    int i=row;
    int j=col;

    while(i>=1 && j>=1)
    {
        if(a[i][j]=='Q')
        {
            return false;
        }
        i--;
        j--;
    }

    i=row;
    j=col;

    while(i>=1 && j<=n)
    {
        if(a[i][j]=='Q')
        {
            return false;
        }
        i--;
        j++;
    }

    return true;
}

bool nQueen(int row)
{
    if(row>n)
    {
        return true;
    }

    for(int col=1;col<=n;col++)
    {
        if(isSafe(row,col))
        {
            a[row][col]='Q';

            if(nQueen(row+1))
            {
                return true;
            }

            a[row][col]='.'; //backtracking
        }
    }
    return false;
}

int main()
{
    cin >> n;

    for(int i=1; i<=n; i++)
    {
        for(int j=1; j<=n; j++)
        {
            a[i][j]='.';
        }
    }

    nQueen(1);

    for(int i=1; i<=n; i++)
    {
        for(int j=1; j<=n; j++)
        {
            cout << a[i][j];
        }
        cout << endl;
    }

    return 0;
}
