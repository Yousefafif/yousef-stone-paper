#include <iostream>
#include <cstdlib>
using namespace std;



enum enSTP { Stone = 1, Paper = 2, Scissors = 3 };

int RandomNumber(int From, int To)
{
    // Function to generate a random number
    int randNum = rand() % (To - From + 1) + From;
    return randNum;
}

enSTP userinput(int choice)
{
    switch (choice)
    {
    case 1:
        return enSTP::Stone;
    case 2:
        return enSTP::Paper;
    case 3:
        return enSTP::Scissors;
    }
}

const char* MoveToString(enSTP move)
{
    switch (move)
    {
    case enSTP::Stone:
        return "Stone";
    case enSTP::Paper:
        return "Paper";
    case enSTP::Scissors:
        return "Scissors";
    
    }
}
void describewinner(enSTP userMove, enSTP pcMove,int &player1wins, int &computerwins, int &draws )



{
     if (userMove == enSTP::Paper && pcMove == enSTP::Stone || userMove == enSTP::Stone && pcMove == enSTP::Scissors|| userMove == enSTP::Scissors && pcMove == enSTP::Paper)
    {
        cout << " [Player1]" << endl;
        system("color 2F");
        player1wins++;
        
        
    }

    
 else if (userMove == pcMove)
    {
        cout << " [No Winner]" << endl;
        system("color 6F");
        draws++;
        
    }

    else
    {
        cout << " [Computer]" << endl;
        system("color 4F");
        cout << "\a";
        computerwins++;
        
        
    }
   
}
void results(int rounds, int player1wins, int computerwins, int draw)

{
    string finalresult;

    if ((player1wins > computerwins) && (player1wins > draw))
    {
        finalresult = "Player1";
        system("color 2F");
    }

    else if ((player1wins < computerwins) && (computerwins > draw))
    {
        finalresult = "Computer";
        system("color 4F");
        cout << "\a";
    }

    else
    {
        finalresult = "Draw";
        system("color 6F");
    }


    cout << "\t\t-------------------------------------------------------------" << endl << endl;
    cout << "\t\t\t\t+++ G a m e  O v e r +++" << endl;;
    cout << "\t\t-------------------------------------------------------------" << endl << endl;
    cout << "\t\t--------------------- [Game Results ]------------------------" << endl;
    cout << "\t\tGame Rounds        : " << rounds << endl;
    cout << "\t\tPlayer1 won times  : " << player1wins << endl;
    cout << "\t\tComputer won times : " << computerwins << endl;
    cout << "\t\tDraw times         : " << draw << endl;
    cout << "\t\tFinal Winner       : " << finalresult << endl;
    cout << "\t\t-------------------------------------------------------------" << endl << endl;



}

void start()
{
    int userchoice, pcchoice, round = 0, player1wins = 0, computerwins = 0, draws = 0;

    cout << "How Many Rounds 1 to 10 ?\n";
    cin >> round;
    cout << endl << endl;

    for (int i = 1; i <= round; i++)
    {


        cout << "Round [" << i << "] begins:" << endl << endl;

        cout << "Your choice: [1]: Stone, [2]: Paper, [3]: Scissors? ";
        cin >> userchoice;
        pcchoice = RandomNumber(1, 3);
        enSTP userMove = userinput(userchoice);
        enSTP pcMove = userinput(pcchoice);
        cout << endl;

        cout << "------------Round [" << i << "] ------------" << endl << endl;

        cout << "Player1 choice  : " << MoveToString(userMove) << endl;
        cout << "Computer choice : " << MoveToString(pcMove) << endl;

        cout << "Round winner    :";  describewinner(userMove, pcMove, player1wins, computerwins, draws);





        cout << endl;
        cout << "----------------------------------" << endl << endl;


    }
    results(round,player1wins, computerwins, draws);
}







int main()
{
    

    srand((unsigned)time(NULL));

    start();

    char again;
    cout << "\t\tDo you want to play again? Y/N? " ;
    cin >> again;
    if (again == 'y' || again == 'Y')
    {
        cout << endl;
        start();
    }
    else
        cout << endl << endl;
        cout << "\t\tThanks For playing ";

    return 0;
}



