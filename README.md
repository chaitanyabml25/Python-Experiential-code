#include <iostream>
#include <vector>
#include <string>
#include <iomanip>
using namespace std;

int main() {

    const int rounds = 25;

    // 25 rounds
    vector<string> player = {
        "Rock","Rock","Rock","Rock","Rock",
        "Rock","Rock","Rock","Rock","Rock",
        "Rock","Rock",
        "Paper","Paper",
        "Paper","Paper","Paper","Paper","Paper",
        "Scissors","Scissors","Scissors","Scissors","Scissors","Scissors"
    };

    vector<string> computer = {
        "Rock","Rock","Rock","Rock","Rock",
        "Rock","Rock","Rock","Rock","Rock",
        "Rock","Scissors",
        "Rock","Rock",
        "Scissors","Scissors","Scissors","Scissors","Scissors",
        "Rock","Rock","Rock","Rock","Rock","Rock"
    };

    int playerWins = 0;
    int computerWins = 0;
    int ties = 0;

    int rockCount = 0;
    int paperCount = 0;
    int scissorsCount = 0;

    int currentStreak = 0;
    int longestStreak = 0;

    cout << "============================================================\n";
    cout << "           ROCK PAPER SCISSORS - 25 ROUND DEMO\n";
    cout << "============================================================\n\n";

    for (int i = 0; i < rounds; i++) {

        string result;

        // Count moves
        if (player[i] == "Rock")
            rockCount++;
        else if (player[i] == "Paper")
            paperCount++;
        else
            scissorsCount++;

        // Check result
        if (player[i] == computer[i]) {
            result = "It's a Tie!";
            ties++;
            currentStreak = 0;
        }
        else if (
            (player[i] == "Rock" && computer[i] == "Scissors") ||
            (player[i] == "Paper" && computer[i] == "Rock") ||
            (player[i] == "Scissors" && computer[i] == "Paper")
        ) {
            result = "You win this round!";
            playerWins++;

            currentStreak++;

            if (currentStreak > longestStreak)
                longestStreak = currentStreak;
        }
        else {
            result = "Computer wins this round!";
            computerWins++;
            currentStreak = 0;
        }

        cout << "Round " << setw(2) << i + 1
             << ": You chose " << player[i]
             << ", Computer chose " << computer[i]
             << " -> " << result << "\n";
    }

    double winRate = (playerWins * 100.0) / rounds;

    // Favourite move
    string favouriteMove;

    if (rockCount >= paperCount && rockCount >= scissorsCount)
        favouriteMove = "Rock";
    else if (paperCount >= rockCount && paperCount >= scissorsCount)
        favouriteMove = "Paper";
    else
        favouriteMove = "Scissors";

    // --------------------------------------------------------
    // PERFORMANCE ANALYSIS
    // --------------------------------------------------------

    cout << "\n============================================================\n";
    cout << "                    PERFORMANCE ANALYSIS\n";
    cout << "============================================================\n";

    cout << "Total rounds played       : " << rounds << "\n";
    cout << "Player wins               : " << playerWins << "\n";
    cout << "Computer wins             : " << computerWins << "\n";
    cout << "Ties                      : " << ties << "\n";
    cout << fixed << setprecision(2);
    cout << "Player win rate           : " << winRate << "%\n";
    cout << "Player's favourite move   : " << favouriteMove << "\n";

    cout << "Move distribution         : Rock: " << rockCount
         << ", Paper: " << paperCount
         << ", Scissors: " << scissorsCount << "\n";

    cout << "Longest player win streak : "
         << longestStreak << "\n";

    // --------------------------------------------------------
    // VERTICAL BAR CHART
    // --------------------------------------------------------

    cout << "\n============================================================\n";
    cout << "                 ROUND OUTCOMES (BAR CHART)\n";
    cout << "============================================================\n\n";

    int maxValue = playerWins;

    if (computerWins > maxValue)
        maxValue = computerWins;

    if (ties > maxValue)
        maxValue = ties;

    // Vertical bars
    for (int level = maxValue; level >= 1; level--) {

        cout << setw(3) << level << " | ";

        if (playerWins >= level)
            cout << "      ███      ";
        else
            cout << "               ";

        if (computerWins >= level)
            cout << "      ███      ";
        else
            cout << "               ";

        if (ties >= level)
            cout << "      ███";

        cout << "\n";
    }

    cout << "    +------------------------------------------------\n";
    cout << "             PLAYER       COMPUTER       TIES\n";
    cout << "               " << playerWins
         << "            " << computerWins
         << "            " << ties << "\n";


    // --------------------------------------------------------
    // PLAYER MOVE DISTRIBUTION BAR CHART
    // --------------------------------------------------------

    cout << "\n============================================================\n";
    cout << "              PLAYER MOVE DISTRIBUTION\n";
    cout << "============================================================\n\n";

    int maxMove = rockCount;

    if (paperCount > maxMove)
        maxMove = paperCount;

    if (scissorsCount > maxMove)
        maxMove = scissorsCount;

    for (int level = maxMove; level >= 1; level--) {

        cout << setw(3) << level << " | ";

        if (rockCount >= level)
            cout << "     ███     ";
        else
            cout << "             ";

        if (paperCount >= level)
            cout << "     ███     ";
        else
            cout << "             ";

        if (scissorsCount >= level)
            cout << "     ███";

        cout << "\n";
    }

    cout << "    +---------------------------------------\n";
    cout << "            ROCK       PAPER      SCISSORS\n";
    cout << "             " << rockCount
         << "          " << paperCount
         << "           " << scissorsCount << "\n";

    // --------------------------------------------------------
    // FINAL OUTPUT
    // --------------------------------------------------------

    cout << "\n============================================================\n";
    cout << "                       FINAL OUTPUT\n";
    cout << "============================================================\n";

    cout << "\nFinal Score -> You : " << playerWins
         << " | Computer : " << computerWins
         << " | Ties : " << ties << "\n";

    cout << "\nCONCLUSION\n";
    cout << "------------------------------------------------------------\n";
    cout << "The Rock Paper Scissors game was completed for 25 rounds.\n";
    cout << "The program records each round and calculates performance\n";
    cout << "statistics for the game.\n";

    cout << "\n                       Thank You!\n";

    return 0;
}
