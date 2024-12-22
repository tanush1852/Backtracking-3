# Backtracking-3

## Problem1 
N Queens(https://leetcode.com/problems/n-queens/)
## Time Complexity:O(n!) Space Complexity:O(n)
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> result = new ArrayList<>();
        char[][] board = new char[n][n];

       
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                board[i][j] = '.';
            }
        }

        
        backtrack(0, board, result, n);
        return result;
    }

    private void backtrack(int row, char[][] board, List<List<String>> result, int n) {
        if (row == n) {
           
            result.add(constructBoard(board));
            return;
        }

        for (int col = 0; col < n; col++) {
            if (isSafe(row, col, board, n)) {
                
                board[row][col] = 'Q';

               
                backtrack(row + 1, board, result, n);

              
                board[row][col] = '.';
            }
        }
    }

    private boolean isSafe(int row, int col, char[][] board, int n) {
        // Check the column
        for (int i = 0; i < row; i++) {
            if (board[i][col] == 'Q') {
                return false;
            }
        }

        // Check the upper-left diagonal
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
            if (board[i][j] == 'Q') {
                return false;
            }
        }

        // Check the upper-right diagonal
        for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++) {
            if (board[i][j] == 'Q') {
                return false;
            }
        }

        return true;
    }

    private List<String> constructBoard(char[][] board) {
        List<String> constructed = new ArrayList<>();
        for (int i = 0; i < board.length; i++) {
            constructed.add(new String(board[i]));
        }
        return constructed;
    }
}



## Problem2
Word Search(https://leetcode.com/problems/word-search/)

## Time Complexity: O(m*n*3^L) Space Complexity:O(L+m*n)

class Solution {
    int m,n;
    int[][] mat;
    int[][] dirs;
    public boolean exist(char[][] board, String word) {
        this.m=board.length;
        this.n=board[0].length;
        this.mat=new int[m][n];
        this.dirs=new int[][]{{-1,0},{1,0},{0,1},{0,-1}};
        boolean flag=false;
        for(int i=0;i<m;i++)
        {
            for(int j=0;j<n;j++)
            {
                if(board[i][j]==word.charAt(0) && mat[i][j]!=1)
                {
                   if(check(board,i,j,0,word))
                   flag=true;
                }
             }
        }
        
        return flag;
    }
    
    public boolean check(char[][] board,int r,int c,int k,String word)
    {
        if(k==word.length()-1)
        return true;
        mat[r][c]=1;
        for(int[] dir:dirs)
        {
            int row=r+dir[0];
            int col=c+dir[1];
            if(row>=0 && col>=0 && row<m && col<n && board[row][col]==word.charAt(k+1) && mat[row][col]!=1){
               

                if(check(board,row,col,k+1,word)){
                    return true;
                }
            }
            
        }

        mat[r][c]=0;
        return false;
        
    }
}