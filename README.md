#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
#define RESET 0


int sudokuSolver();
int findEmptyCell();
int isValid();
void printGrid();
void inputGrid();

int grid[9][9]= {
        {0, 0, 0, 0, 6, 8, 0, 3, 0},
        {1, 9, 0, 0, 0, 0, 0, 0, 0},
        {8, 0, 3, 1, 0, 0, 2, 0, 0},
        {4, 0, 0, 0, 5, 1, 0, 6, 0},
        {7, 0, 0, 0, 2, 0, 0, 0, 4},
        {0, 0, 0, 0, 7, 0, 8, 0, 0},
        {0, 1, 0, 0, 0, 5, 0, 0, 7},
        {0, 0, 4, 0, 0, 0, 0, 0, 0},
        {0, 5, 0, 0, 3, 0, 1, 0, 0}
        };



int row,col;
long int totalNumOfCalls=0;

void main()
{

    int i,j,solution=0;


    printf("You can change the puzzle before running the program \nby changing the values in the \"grid\" array\n\n");
    printf("The Entered Sudoku puzzle is: \n");
    printGrid();

    solution=sudokuSolver();
    if(solution){
 printf("\nThe Solved Sudoku is: \n\n");
 printGrid();
    }
    else
    printf("\nNo Possible Solution!!\n\n");
    getch();
    }



int findEmptyCell(){
 int i,j;

 for(i=row;i<=8;i++)
     for(j=0;j<=8;j++){
  if(grid[i][j]==0)
   {
   row=i;col=j;
   return 1;
   }
     }
   return 0;

}

int isValid(int cellRow, int cellCol, int num){
   int i,j,trow,tcol,trow1,tcol1;
     int rowStart = (cellRow/3) * 3;
    int colStart = (cellCol/3) * 3;


   for(j=0;j<=8;j++){
       if(grid[cellRow][j]==num)
    return 0;
       if(grid[j][cellCol]==num)
    return 0;

   }


    for(i=rowStart;i<=rowStart+2;i++)
  for(j=colStart;j<=colStart+2;j++)
      if(grid[i][j]==num)return 0;


    return 1;
}
int sudokuSolver(){

     int digit;
     int prevRow,prevCol;
     totalNumOfCalls++;

     if(!findEmptyCell())
 return 1;

     for(digit=1;digit<=9;digit++){
  if(isValid(row,col,digit)){
  grid[row][col]=digit;
  prevRow=row;prevCol=col;
  if(sudokuSolver())
   return 1;

  row=prevRow;col=prevCol;
  grid[row][col]=RESET;
  }

    }

    return 0;

}
void printGrid(){

 int i,j;

 printf("\t-------------------------\n");
 for(i=0;i<9;i++){
    printf("\t");
    for(j=0;j<9;j++){
       if(j==0)
    printf("| ");
       if(grid[i][j]==0)
    printf(". ");
       else
    printf("%d ",grid[i][j]);
       if((j+1)%3==0 )
    printf("| ");

   }

   if((i+1)%3==0 )
       printf("\n\t-------------------------");

   printf("\n");

 }

}

