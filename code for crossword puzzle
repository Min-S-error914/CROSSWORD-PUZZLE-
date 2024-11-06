#include <iostream>
#include <vector>
#include <string>

using namespace std;

enum Direction { ACROSS, DOWN };

class Word {
public:
    Word(const string& word, const string& clue, int x, int y, Direction dir)
        : word(word), clue(clue), x(x), y(y), direction(dir) {}

    string getWord() const { return word; }
    string getClue() const { return clue; }
    int getX() const { return x; }
    int getY() const { return y; }
    Direction getDirection() const { return direction; }

private:
    string word;
    string clue;
    int x, y;
    Direction direction;
};

class CrosswordGrid {
public:
    CrosswordGrid(int width, int height)
        : width(width), height(height) {
        grid.resize(height, vector<char>(width, ' ')); // Initialize grid with empty spaces
    }

    bool canPlaceWord(const Word& word) const {
        int x = word.getX();
        int y = word.getY();
        Direction dir = word.getDirection();

        // Check if the word fits within the grid boundaries
        if (dir == ACROSS) {
            if (x + word.getWord().length() > width) return false;
        } else if (dir == DOWN) {
            if (y + word.getWord().length() > height) return false;
        }

        // Check if the word can be placed (no overlap with existing letters)
        for (int i = 0; i < word.getWord().length(); ++i) {
            if (dir == ACROSS) {
                if (grid[y][x + i] != ' ' && grid[y][x + i] != word.getWord()[i]) {
                    return false;
                }
            } else if (dir == DOWN) {
                if (grid[y + i][x] != ' ' && grid[y + i][x] != word.getWord()[i]) {
                    return false;
                }
            }
        }
        return true;
    }

    bool placeWord(const Word& word) {
        if (canPlaceWord(word)) {
            int x = word.getX();
            int y = word.getY();
            Direction dir = word.getDirection();

            for (int i = 0; i < word.getWord().length(); ++i) {
                if (dir == ACROSS) {
                    grid[y][x + i] = word.getWord()[i];
                } else if (dir == DOWN) {
                    grid[y + i][x] = word.getWord()[i];
                }
            }
            return true;
        }
        return false;
    }

    void displayGrid() const {
        for (const auto& row : grid) {
            for (char cell : row) {
                cout << (cell == ' ' ? '.' : cell) << ' '; // '.' represents empty spaces
            }
            cout << endl;
        }
    }

private:
    int width, height;
    vector<vector<char>> grid;
};

int main() {
    // Create a 10x10 crossword grid
    CrosswordGrid grid(10, 10);

    // Define some words with their clues and starting positions
    Word word1("HELLO", "A common greeting", 0, 0, ACROSS);
    Word word2("WORLD", "Planet we live on", 0, 0, DOWN);
    Word word3("CROSS", "The theme of the puzzle", 5, 0, ACROSS);
    Word word4("PUZZLE", "A type of game", 5, 0, DOWN);

    // Place words on the grid
    grid.placeWord(word1);
    grid.placeWord(word2);
    grid.placeWord(word3);
    grid.placeWord(word4);

    // Display the grid
    cout << "Crossword Puzzle Grid:\n";
    grid.displayGrid();

    // Display clues
    cout << "\nClues:\n";
    cout << "1. " << word1.getClue() << " (ACROSS)\n";
    cout << "2. " << word2.getClue() << " (DOWN)\n";
    cout << "3. " << word3.getClue() << " (ACROSS)\n";
    cout << "4. " << word4.getClue() << " (DOWN)\n";

    return 0;
}
