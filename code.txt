#include <iostream>
#include <cstdlib>   //for rand() and srand()
#include <ctime>     //for clock()
#include <limits>    //for numeric_limits
#include <iomanip>   //for setw() and setfill()
#include <unistd.h>  // for sleep()
#include <fstream>   //for ifstream
#include <string>    //for string
#include <windows.h> //for sleep()
#include <chrono>    //for time_point

// This code can only run in code block cuz sleep() function

using namespace std;
using namespace chrono; // for time_point

const int N = 9;
int grid[N][N];

void waitAndClearConsole()
{
    int sleepTime = 30000; // sleep for 30 seconds
    clock_t startTime = clock();

    while (clock() < startTime + sleepTime * CLOCKS_PER_SEC / 1000)
    {
        if (GetAsyncKeyState(VK_SPACE) & 0x8000)
        { // check if 'spaceBar' is pressed
            break;
        }
    }
// Clear console
#ifdef _WIN32
    system("cls");
#else
    system("clear");
#endif
}
void waitAndClearConsole2()
{
    int sleepTime = 10000; // sleep for 10 seconds
    clock_t startTime = clock();

    while (clock() < startTime + sleepTime * CLOCKS_PER_SEC / 1000)
    {
        if (GetAsyncKeyState(VK_SPACE) & 0x8000)
        { // check if 'spaceBar' is pressed
            break;
        }
    }
// Clear console
#ifdef _WIN32
    system("cls");
#else
    system("clear");
#endif
}
void clearConsole()
{
#ifdef _WIN32
    system("cls");
#else
    system("clear");
#endif // Clears the console
}
// for "Sudoku" message
void displayText(string text)
{
    // Loop to gradually decrease opacity
    for (int i = 40; i >= 0; i--)
    {
        clearConsole();
        // Loop over each character in the text
        for (char c : text)
        {
            if (isspace(c))
            { // Leave spaces unchanged
                cout << c;
            }
            else
            {
                int r = rand() % 40; // Generate a random number
                if (r < i)
                { // Set character to a space with probability i%
                    cout << ' ';
                }
                else
                { // Otherwise, output the character
                    cout << c;
                }
            }
        }
        cout << endl;
        sleep(0.01); // Wait for 10 milliseconds (adjust as necessary)
        if (GetAsyncKeyState(VK_SPACE) & 0x8000)
        {          // check if 'spaceBar' is pressed
            break; // exit loop if 'spaceBar' is pressed
        }
    }
    // Wait for 1.5 seconds unless 'spaceBar' is pressed
    if (!(GetAsyncKeyState(VK_SPACE) & 0x8000))
    { // check if 'spaceBar' is  NOT pressed
        sleep(1.5);
    }

    // Loop to gradually increase opacity
    for (int i = 0; i <= 10; i++)
    {
        clearConsole();
        // Loop over each character in the text
        for (char c : text)
        {
            if (isspace(c))
            { // Leave spaces unchanged
                cout << c;
            }
            else
            {
                int r = rand() % 10; // Generate a random number
                if (r < i)
                { // Set character to a space with probability i%
                    cout << ' ';
                }
                else
                { // Otherwise, output the character
                    cout << c;
                }
            }
        }
        cout << endl;
        sleep(0.0001); // Wait for 0.1 milliseconds (adjust as necessary)
        if (GetAsyncKeyState(VK_SPACE) & 0x8000)
        {          // check if 'spaceBar' is pressed
            break; // exit loop if 'spaceBar' is pressed
        }
    }
    clearConsole();
}

// for "Powered By Ututu" message
void displayText2(string text)
{
    int delay = 1; // adjust this value to change the speed of the animation
    clock_t startTime = clock();
    for (int i = 0; i < text.length(); i++)
    {
        cout << text[i];
        while (clock() < startTime + delay * (i + 1) * CLOCKS_PER_SEC / 1000)
            ;
    }
    waitAndClearConsole();
}

// for how to play sudoku text
void displayText3(string text)
{
    int delay = 50; // adjust this value to change the speed of the animation
    clock_t startTime = clock();
    for (int i = 0; i < text.length(); i++)
    {
        cout << text[i];
        if (GetAsyncKeyState(VK_SPACE) & 0x8000)
        {                               // check if 'spaceBar' is pressed
            cout << text.substr(i + 1); // display remaining characters and exit loop
            break;
        }
        while (clock() < startTime + delay * (i + 1) * CLOCKS_PER_SEC / 1000)
            ;
    }
    sleep(1);
}

void introAnimation()
{
    // Output ASCII art text from a .txt file with animation
    ifstream asciiFile("sudokuText1-Title.txt");
    string asciiText((istreambuf_iterator<char>(asciiFile)), istreambuf_iterator<char>());
    displayText(asciiText); // for "Sudoku"message

    ifstream asciiFile2("sudokuText2-Intro.txt");
    string asciiText2((istreambuf_iterator<char>(asciiFile2)), istreambuf_iterator<char>());
    displayText2(asciiText2); // for "Powered By Ututu" message
    sleep(1);

    ifstream asciiFile3("sudokuText3-Rules.txt");
    string asciiText3((istreambuf_iterator<char>(asciiFile3)), istreambuf_iterator<char>());
    displayText3(asciiText3);
    waitAndClearConsole();
}

// for "Game Over !" message
void displayText4(string text)
{
    int delay = 1.5; // adjust this value to change the speed of the animation
    clock_t startTime = clock();
    for (int i = 0; i < text.length(); i++)
    {
        cout << text[i];
        while (clock() < startTime + delay * (i + 1) * CLOCKS_PER_SEC / 1000)
            ;
    }
}

// for "You Won !" message
void displayText5(string text)
{
    int delay = 1.5; // adjust this value to change the speed of the animation
    clock_t startTime = clock();
    for (int i = 0; i < text.length(); i++)
    {
        cout << text[i];
        while (clock() < startTime + delay * (i + 1) * CLOCKS_PER_SEC / 1000)
            ;
    }
}

// for "00-rule" message
void displayText6(string text)
{
    int delay = 20; // adjust this value to change the speed of the animation
    clock_t startTime = clock();
    for (int i = 0; i < text.length(); i++)
    {
        cout << text[i];
        if (GetAsyncKeyState(VK_SPACE) & 0x8000)
        {                               // check if 'spaceBar' is pressed
            cout << text.substr(i + 1); // display remaining characters and exit loop
            break;
        }
        while (clock() < startTime + delay * (i + 1) * CLOCKS_PER_SEC / 1000)
            ;
    }
    sleep(1);
}

int getDifficulty()
{
    int difficulty;
    while (true)
    {
        cout << "Enter difficulty level (beginner = 0, easy = 1, medium = 2, hard = 3): ";
        char input;
        while (true)
        {
            if (cin >> input && input >= '0' && input <= '3' && cin.peek() == '\n')
            {
                difficulty = input - '0';
                break;
            }
            else
            {
                cout << "\nInvalid input, you can only enter a single digit between 0 and 3.\n"
                     << endl;
                cout << "*Press Spacebar to skip";
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(), '\n');
                waitAndClearConsole();
                cout << "Enter difficulty level (beginner = 0, easy = 1, medium = 2, hard = 3): ";
            }
        }
        return difficulty;
    }
}

// Function to check if a number can be placed in a cell
bool canPlace(int num, int row, int col)
{
    // Check row
    for (int i = 0; i < N; i++)
        if (grid[row][i] == num)
            return false;

    // Check column
    for (int i = 0; i < N; i++)
        if (grid[i][col] == num)
            return false;

    // Check sub-grid
    int sub_grid_row = row - row % 3;
    int sub_grid_col = col - col % 3;
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            if (grid[i + sub_grid_row][j + sub_grid_col] == num)
                return false;
        }
    }

    return true;
}

// Recursive function to generate a valid Sudoku puzzle
bool solveSudoku(int row, int col)
{
    if (row == N)
        return true;

    if (col == N)
        return solveSudoku(row + 1, 0);

    if (grid[row][col] != 0)
        return solveSudoku(row, col + 1);

    for (int num = 1; num <= 9; num++)
    {
        int r = rand() % 9 + 1;
        if (canPlace(r, row, col))
        {
            grid[row][col] = r;

            if (solveSudoku(row, col + 1))
                return true;

            grid[row][col] = 0;
        }
    }
    return false;
}

void getFillLevel(int difficulty, int &fill_level, int &mistake_limiter)
{
    switch (difficulty)
    {
    case 0:
        fill_level = 8;
        mistake_limiter = 3;
        break;
    case 1:
        fill_level = 6;
        mistake_limiter = 3;
        break;
    case 2:
        fill_level = 5;
        mistake_limiter = 3;
        break;
    case 3:
        fill_level = 4;
        mistake_limiter = 3;
        break;
    default:
        break;
    }
}

void fillGrid(int difficulty)
{
    int fill_level;
    int mistake_limiter;
    getFillLevel(difficulty, fill_level, mistake_limiter);

    // Generate a valid Sudoku puzzle
    solveSudoku(0, 0);

    // Fill in the grid with numbers
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {
            if (rand() % 10 > fill_level)
                grid[i][j] = 0;
        }
    }
}
// Function to display the grid
void displayGrid()
{
    clearConsole();
    cout << "\n             Sudoku Grid: " << endl;
    cout << "                           -------------------------------------------------" << endl;
    cout << "                           |               |               |               |\n";
    for (int i = 0; i < N; i++)
    {
        cout << "                           ";
        cout << "| ";
        cout << "  ";
        for (int j = 0; j < N; j++)
        {
            if (grid[i][j] == 0)
                cout << "_ ";
            else
                cout << grid[i][j] << " ";

            if ((j + 1) % 3 == 0 && j < N - 1)
            {
                cout << "  ";
                cout << "| ";
                cout << "  ";
            }
            else
                cout << "  ";
        }

        cout << "| " << endl;

        if ((i + 1) % 3 == 0 && i < N - 1)
        {
            cout << "                           |               |               |               |\n";
            cout << "                           -------------------------------------------------" << endl;
            cout << "                           |               |               |               |\n";
        }
    }
    cout << "                           |               |               |               |\n";
    cout << "                           -------------------------------------------------" << endl;
}

// Function to check if the number is in the row
bool inRow(int row, int num)
{
    for (int i = 0; i < N; i++)
    {
        if (grid[row][i] == num)
            return true;
    }
    return false;
}

// Function to check if the number is in the column
bool inCol(int col, int num)
{
    for (int i = 0; i < N; i++)
    {
        if (grid[i][col] == num)
            return true;
    }
    return false;
}

// Function to check if the number is in the 3x3 box
bool inBox(int row, int col, int num)
{
    int r = row - row % 3;
    int c = col - col % 3;
    for (int i = r; i < r + 3; i++)
    {
        for (int j = c; j < c + 3; j++)
        {
            if (grid[i][j] == num)
                return true;
        }
    }
    return false;
}

// Function to check if it is safe to put the number in the cell
bool isSafe(int row, int col, int num)
{
    return !inRow(row, num) && !inCol(col, num) && !inBox(row, col, num);
}

bool isGridComplete()
{
    for (int i = 0; i < 9; i++)
    {
        for (int j = 0; j < 9; j++)
        {
            if (grid[i][j] == 0)
                return false;
        }
    }
    return true;
}

void display(int mistake_counter) // pass mistake_counter by value
{

    cout << "                                                                                  mistake:" << mistake_counter - 1 << "/3 \n";
}
// for time spent
void display2(steady_clock::time_point start_time)
{
    steady_clock::time_point current_time = steady_clock::now();
    auto elapsed_time = duration_cast<seconds>(current_time - start_time);
    int minutes = elapsed_time.count() / 60;
    int seconds = elapsed_time.count() % 60;

    cout << "\n                                                                             Time Taken: " << setfill('0') << setw(2) << minutes << ":" << setw(2) << seconds << "      ";
}
// Function to play the sudoku game
void playGame(int difficulty, int &mistake_counter)
{
    steady_clock::time_point start_time = steady_clock::now();
    int fill_level;
    int mistake_limiter;
    getFillLevel(difficulty, fill_level, mistake_limiter);
    int row, col, num;
    bool exit = false;
    while (!exit)
    {
        cout << "\nEnter row, col, and number separated by spaces (or enter -1 to exit or enter 00 for rule): ";

        if (!(cin >> row))
        {
            cout << "\nInvalid input, you can only enter numbers.\n"
                 << endl;
            cout << "*Press Spacebar to skip\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            display2(start_time);
            waitAndClearConsole();
            displayGrid();
            display(mistake_counter);
            continue;
        }

        if (row == 00)
        {
            clearConsole();
            ifstream asciiFile6("sudokuText6-00.txt");
            string asciiText6((istreambuf_iterator<char>(asciiFile6)), istreambuf_iterator<char>());
            displayText6(asciiText6);
            waitAndClearConsole();
            displayGrid();
            display(mistake_counter);
            continue;
        }

        if (row == -1)
        {
            exit = true;
            break;
        }
        if (!(cin >> col))
        {
            cout << "\nInvalid input, you can only enter numbers.\n"
                 << endl;
            cout << "*Press Spacebar to skip\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            display2(start_time);
            waitAndClearConsole();
            displayGrid();
            display(mistake_counter);
            continue;
        }
        if (!(cin >> num))
        {
            cout << "\nInvalid input, you can only enter numbers.\n"
                 << endl;
            cout << "*Press Spacebar to skip\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            display2(start_time);
            waitAndClearConsole();
            displayGrid();
            display(mistake_counter);
            continue;
        }
        else
        {
            string line;
            getline(cin, line);
            if (!line.empty() || num < 1 || num > 9)
            {
                cout << "\nInvalid input, you can only enter numbers from 1 to 9.\n"
                     << endl;
                cout << "*Press Spacebar to skip\n";
                display2(start_time);
                waitAndClearConsole();
                displayGrid();
                display(mistake_counter);
                continue;
            }
        }

        if (row < 1 || row > 9 || col < 1 || col > 9 || num < 1 || num > 9)
        {
            cout << "\nInvalid input, all values must be within the range of 1-9 for row and col, and 1-9 for num.\n"
                 << endl;
            cout << "*Press Spacebar to skip\n";
            display2(start_time);
            waitAndClearConsole();
            displayGrid();
            display(mistake_counter);
            continue;
        }
        if (grid[row - 1][col - 1] != 0)
        {
            cout << "\nInvalid move, cell is already filled. Try again.\n"
                 << endl;
            cout << "*Press Spacebar to skip\n";
            display2(start_time);
            waitAndClearConsole();
            displayGrid();
            display(mistake_counter);
        }
        else if (!isSafe(row - 1, col - 1, num))
        {
            mistake_counter++;
            cout << "\nInvalid move, wrong number. You've made a mistake .Try again.\n"
                 << endl;
            cout << "*Press Spacebar to skip\n";
            display2(start_time);
            waitAndClearConsole();
            displayGrid();
            display(mistake_counter);

            if (mistake_counter > mistake_limiter)
            {
                clearConsole();
                cout << "\n\nYou have reached the maximum number of allowed mistakes (" << mistake_counter - 1 << "). Game over.\n\n"
                     << endl;
                ifstream asciiFile4("sudokuText4-GameOver.txt"); // for "Game Over!" message
                string asciiText4((istreambuf_iterator<char>(asciiFile4)), istreambuf_iterator<char>());
                displayText4(asciiText4);
                cout << "\n\n\n\n\n\n";
                display2(start_time);
                waitAndClearConsole2();
                exit = true;
                break;
            }
        }
        else
        {
            clearConsole();
            grid[row - 1][col - 1] = num;
            displayGrid();
            display(mistake_counter);
            if (isGridComplete())
            {
                clearConsole();
                ifstream asciiFile5("sudokuText5-YouWon.txt"); // for "You Won !" message
                string asciiText5((istreambuf_iterator<char>(asciiFile5)), istreambuf_iterator<char>());
                displayText5(asciiText5);
                cout << "\n\n\n\n\n\n";
                display2(start_time);
                waitAndClearConsole2();
                exit = true;
                break;
            }
        }
    }
}
void resetGrid()
{
    for (int row = 0; row < N; row++)
    {
        for (int col = 0; col < N; col++)
        {
            grid[row][col] = 0;
        }
    }
}

int main()
{
    introAnimation();
    bool playAgain = true;

    while (playAgain)
    {
        int difficulty = getDifficulty();
        srand(time(0));
        fillGrid(difficulty);
        displayGrid();
        int mistake_counter = 1;
        display(mistake_counter);
        playGame(difficulty, mistake_counter);

        cout << "Do you want to play again? Enter 'yes' to continue or any other key to exit." << endl;
        string input;
        cin >> input;

        if (input == "yes")
        {
        clearConsole();
        resetGrid();
        int difficulty = getDifficulty();
        srand(time(0));
        fillGrid(difficulty);
        displayGrid();
        int mistake_counter = 1;
        display(mistake_counter);
        playGame(difficulty, mistake_counter);
        cout << "Do you want to play again? Enter 'yes' to continue or any other key to exit." << endl;
        string input;
        cin >> input;
        clearConsole();
        }
        else
        {
            playAgain = false;
        }
    }
    return 0;
}
