# 15.GAME.end
三子棋（终）
#define _CRT_SECURE_NO_WARNINGS 1
//放函数定义的

#include "game.h"

void InitBoard(char board[ROW][COL], int row, int col)
{
	int i = 0;
	int j = 0;
	for (i = 0; i < row; i++)
	{
		for (j = 0; j < col; j++)
		{
			board[i][j] = ' ';//将数组初始化为空格
		}
	}
}

//void DispalyBoard(char board[ROW][COL], int row, int col)
//{
//	int i = 0;
//	for (i = 0; i < row; i++)
//	{
//		//1.打印一行数据
//		printf(" %c | %c | %c \n",board[i][0],board[i][1],board[i][2]);
//		//2.打印分割行
//		if (i<row-1)
//		printf("---|---|---\n");
//	}
//}

//优化
void DispalyBoard(char board[ROW][COL], int row, int col)
{
	int i = 0;
	for (i = 0; i < row; i++)
	{
	
		int j = 0;
		for (j = 0; j < col; j++)
		{
		//1.打印一行数据
			printf(" %c ", board[i][j]);
				if(j< col -1)
					printf("|");
		}
		printf("\n");
		//2.打印分割行
		if (i < row - 1)
		{
			for (j = 0; j < col; j++)
			{
				printf("---");
				if (j < col - 1)
				printf("|");
			}
			
		}
		printf("\n");
	}
}

void PlayerMove(char board[ROW][COL], int row, int col)
{
	int x = 0;
	int y = 0;
	printf("玩家走:>\n");
	printf("请输入要下的坐标:>");

	while (1)
	{
		scanf("%d%d,&x,&y");
		//判断x，y坐标合法性
		if (x >= 1 && x <= row && y >= 1 && y <= col)
		{
			if (board[x - 1][y - 1] == ' ')
			{
				board[x - 1][y - 1] == '*'
					break;
			}
		}   
		else
		{
			printf("坐标非法，请重新输入\n");
		}
	}
}

void ComputerMove(char board[ROW][COL], , int row, int col)
	{
		int x = 0;
		int y = 0;
		printf("电脑走:>\n");
		while (1)
		{
			x = rand() % row;
			y = rand() % col;
			if (board[x][y] == ' ')
			{
				board[x][y] == '#';
				break;
			}
		}
	}

int IsFull(char board[ROW][COL], int row, int col);
{
	int i = 0;
	int j = 0;
	for (i = 0; i < row; i++)
	{
		for (j = 0; j < col; j++)
		{
			if (board[i][j] == ' ')
			{
				return 0;//没满
			}
		}
	}
	return 1;//满了
}

char IsWin(charboard[ROW][COL], int row, int col)
{
	int i = 0;
	for (i = 0; i < row; i++)
	{
		if (board[i][0] == board[i][i] && board[i][1] == board[i][2] && board != ' ')
		{
			return board[i][1];
		}
	}
	for (i = 0; i < col; i++)
	{
		if (board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[1][i] != ' ')
		{
			return board[1][i];
		}
	}
	if (board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[1][1] != ' ')
		return board[1][1];
	if (board[2][0] == board[1][1] && board[1][1] == board[0][2] && board[1][1] != ' ')
		return board[1][1];
	//判断是否平局
	if (1 == IsFull(board, ROW, COL))
	{
		return'Q';
	}
	return 'C';
}

#pragma once

#include <stdio.h>

//放函数声明的
#define ROW 3//定义行
#define COL 3//定义列

//函数声明
void InitBoard(char board[ROW][COL], int row, int col);
void DispalyBoard(char board[ROW][COL], int row, int col);
void PlaerMove(char board[ROW][COL], int row, int col);

void ComputerMove(char board[ROW][COL], int row, int col);

//判断游戏四种状态
//1.玩家赢——'*'
//2.电脑赢——'#'
//3.平局  ——'Q'
//4.继续  ——'C'

char IsWin(char board[ROW][COL], int row, int col);




#define _CRT_SECURE_NO_WARNINGS 1
//测试三子棋游戏


#include "game.h"
void menu()
{
	printf("**************************\n");
	printf("****1.paly   0.exit*******\n");
	printf("**************************\n");
}


void game()
{
	//数组-存放走出的棋盘信息
	char board[ROW][COL] = { 0 };
	//想要全部是空格，初始化棋盘
	InitBoard(board, ROW, COL);
	//打印棋盘
	DispalyBoard(board,ROW,COL);
	//下棋
	while (1)
	{
		//玩家下棋
		PlayerMove(board,ROW,COL);
		DisplayerBoard(board, ROW, COL);
		//判断玩家是否赢
		ret = IsWin(board, ROW, COL);
		if (ret != 'C')
		{
			break;
		}
		//电脑下棋
		ComputerMove(board, ROW, COL);
		DispalyBoard(board, ROW, COL);
		//判断电脑是否赢
		ret = IsWin(board, ROW, COL);
		if (ret != 'C')
		{
			break;
		}
		if (ret == '*')
		{
			printf("玩家赢\n");
		}
		else if (ret('#'))
		{
			printf("电脑赢\n");
		}
		else
		{
			printf("平局\n");
		}
	}
}

void test()
{
	int input = 0;
	do
	{
		menu();
		printf("请选择:>");
		scanf_s("%d", &input);
		switch(input)
		{
			case 1:
				game();
				break;
			case 0:
					printf("退出游戏\n");
					break;
			default:;
		}
		
	} while (input);
}

int main()
{
	test();
	return 0;
}
