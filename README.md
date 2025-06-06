# project-1-Tic-Tac-Toe-Game-
#include<stdio.h>
#include<stdbool.h>

#define size 3

char board[size][size];

void initializeboard(){
    for(int i=0;i<size;i++){
        for(int j=0;j<size;j++){
            board[i][j]='1'+(i*size+j);
        }
    }
}
void display(){
    for(int i=0;i<size;i++){
        for(int j=0;j<size;j++){
            printf("%c ",board[i][j]);
            if(j<size-1) printf(" | ");
        }
        printf("\n");
        if (i < size - 1) printf("-----------\n");
    }
}
bool Makemove(char player,int position){
    int row=(position-1)/10;
    int col=(position-1)%10;
    if(board[row][col]!='X' && board[row][col]!='O'){
        board[row][col]=player;
        return true;
    }
    return false;
}
bool Checkwin(char player){
    for(int i=0;i<size;i++){
        if(board[i][0]==player && board[i][1]==player && board[i][2]==player) return true;
        if(board[0][i]==player && board[1][i]==player && board[2][i]==player) return true;
    }
    if(board[0][0]==player && board[1][1]==player && board[2][2]==player) return true;
    if(board[0][2]==player && board[1][1]==player && board[2][0]==player) return true;
    return false;
}
bool isBoardfull(){
    for(int i=0;i<size;i++){
        for(int j=0;j<size;j++){
            if(board[i][j]!='X' && board[i][j]!='O') return false;
        }
    }
    return true;
}
int main(){
    char player='X';
    int position;
    initializeboard();
    while(true){
        display();
        printf("Player %c position(1-9):",player);
        scanf("%d",&position);
        if(position<1 || position>9 || !Makemove(player,position)){
            printf("Invalid move");
            continue;
        }
        if(Checkwin(player)){
            display();
            printf("Congratulations..!!\nPlayer %c Wins\nYennaikum VidaaMuyarchi\n",player);
            break;
        }
        if(isBoardfull()){
            display();
            printf("Good Match ends in a Draw\n");
            break;
        }
        player=(player=='X')?'O':'X';
    }
return 0;
}
