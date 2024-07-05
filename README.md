include <iostream>
#include <vector>
#include <string>
using namespace std;
void initializeBoard(vector<vector<char>>& board);
void displayBoard(const vector<vector<char>>& board);
bool makeMove(vector<vector<char>>& board, char player, int row, int col);
bool checkWin(const vector<vector<char>>& board, char player);
bool checkDraw(const vector<vector<char>>& board);
bool isValidMove(const vector<vector<char>>& board, int row, int col);
bool playAgain();

int main() {
    char currentPlayer = 'X';
    bool gameover = false;
    vector<vector<char>> board(3, vector<char>(3, ' '));
    cout << "Welcome to Tic-Tac-Toe!" << endl;
    do {
        initializeBoard(board);

        while (!gameover) {
            int row, col;
            displayBoard(board);
            cout << "Player " << currentPlayer << ", enter your move (row [1-3] and column [1-3]): ";
            cin >> row >> col;
            row--;
            col--;
            if (isValidMove(board, row, col)) {
                if (makeMove(board, currentPlayer, row, col)) {
                    if (checkWin(board, currentPlayer)) {
                        displayBoard(board);
                        cout << "Player " << currentPlayer << " wins!" << endl;
                        gameover = true;
                    }
                    else if (checkDraw(board)) {
                        displayBoard(board);
                        cout << "It's a draw!" << endl;
                        gameover = true;
                    }
                    else {
                       
                     currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
                    }
                }
                else {
                    cout << "That cell is already occupied. Try again." << endl;
                }
            }
            else {
                cout << "Invalid move. Please enter row and column within range [1-3]." << endl;
            }
        }
        gameover = false; 
    } while (playAgain());
    cout << "Thanks for playing Tic-Tac-Toe!" << endl;
    return 0;
}
void initializeBoard(vector<vector<char>>& board) {
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            board[i][j] = ' ';
        }
    }
}
void displayBoard(const vector<vector<char>>& board) {
    cout << "-------------" << endl;
    for (int i = 0; i < 3; ++i) {
        cout << "| ";
        for (int j = 0; j < 3; ++j) {
            cout << board[i][j] << " | ";
        }
        cout << endl << "-------------" << endl;
    }
}
bool makeMove(vector<vector<char>>& board, char player, int row, int col) {
    if (board[row][col] == ' ') {
        board[row][col] = player;
        return true;
    }
    return false;
}
bool checkWin(const vector<vector<char>>& board, char player) {

    for (int i = 0; i < 3; ++i) {
        if (board[i][0] == player && board[i][1] == player && board[i][2] == player)
            return true;
    }
    for (int j = 0; j < 3; ++j) {
        if (board[0][j] == player && board[1][j] == player && board[2][j] == player)
            return true;
    }
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player))
        return true;

    return false;
}
bool checkDraw(const vector<vector<char>>& board) {
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            if (board[i][j] == ' ')
                return false;
        }
    }
    return true;
}
bool isValidMove(const vector<vector<char>>& board, int row, int col) {
    return (row >= 0 && row < 3 && col >= 0 && col < 3 && board[row][col] == ' ');
}
bool playAgain() {
    char choice;
    cout << "Do you want to play again? (y/n): ";
    cin >> choice;
    return (choice == 'y' || choice == 'Y');
}
