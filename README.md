/*
This app will utilize the stdio, stdlib, and time header files in order to properly function.
The standard library header file is included so that rand/srand can be used
The time.h header file is included so that the time() function can be used
*/
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>

/* Create a function that chooses a random number to point to a stored answer within the array
* This function takes an int variable, and then computes a random number between 0-10 using the srand and rand functions, and returns the random value generated

*/

int randomNumber(int generate)
{
	int pickANumber = 0;
	srand(time(NULL));
	pickANumber = rand() % 10;
	return pickANumber;
}






// Begin main() function, which returns 0
int main()
{
	// define structure to store data about program users (helpful if program is expanded to multiple users with unique profiles)
	typedef struct currentUser
		{
		int accountNumber;
		const char* userName;
		} user;

	user data;

	// store user data in userData structure (currently one user)
	data.accountNumber = 1;
	data.userName = "Optimus Prime";

	// Define variable for collecting user input

	char* inquiry[100];

	// Define variable to hold value of randomly chosen array response
	int chosenAnswer = 0;

	// create an array to hold 10 potential answers

	const char* answers[11] = {
	"The outcome is very doubtful.", "Most definitely!", "Hard to say at this time.", "The answer is certainly yes!",
	"I'm afraid not.", "There is no way to tell.", "I can confidently answer yes!", "Absolutely not!",
	"This is one of the world's greatest mysteries...", "It seems impossible, but is not" };


	// prompt user for a question, user's question is inconsequential as response is chosen at random
	printf("Ask your question...but beware the answer! ");
	 scanf("%s", inquiry);

	// generate random number between 0 and 9 using the user defined random number function

	randomNumber(chosenAnswer);

	// Output one of the stored answers from the array based on the random number that was generated through the random number function

	printf(answers[chosenAnswer]);

	// open file to store questions asked
	FILE* fpath;
	fpath = fopen("questions.txt", "a+");

	// ensure file opened successfully
	if (fpath == NULL)
	{
		printf("Error opening file\n");
		exit(1);
	}

	// write user question to file
	fprintf(fpath, "An answer has been given!\n");
	
	fflush(fpath);

	// close file after appending user question

	fclose(fpath);

	// terminate program by returning 0 to end the main() function
	return 0;
}
