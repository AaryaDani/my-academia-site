---
title: C++ Final Project
tags:
- Coding
date: "2024-04-06T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: 

image:
  caption: 
  focal_point: Smart
---


```yaml
// "The Use of Artificial Intelligence in Waste Management"
 /*  Our paper goes into detail about waste management and why it's important.
  *  We then go into detail about the specifics of deep learning, including an 
  *  overview of neural networks operate.
  *  We then expand upon this to cover operation of automated machines that
  *  sort a vast variety of different types of waste and the top company that 
  *  builds them called AMP Robotics.
  * */ 

/* Our app has three main functionalities: (1) learn and take a quiz on 
 * different topics from our paper, (2) a fun sustainability
 * game that authorizes the user before it can begin, and (3) to explain
 * how neural networks operate
 */


#include <stdlib.h>
#include <stdio.h>
#include <time.h>
#include <math.h>
#include <string.h>
#include <ctype.h>


//function prototypes
void NN(void);
void welcome(void);
void wait(void);
double rand0to1(void);
double rand0to10(void);
void SustainabilityGame(void);
void enterPittID(char *);
void SustainMain(void);
int SubjectChoicePrompt(void);
void TopicLearning(int);
void TopicQuiz(int);
void QuizMain(void);
void help(int);


int main(void)
{
	char userChoice[5]; //user's choice for which program to run, or if they type help
	int helpNum; //the number the user wants to learn more about
	bool valid; //if userChoice is valid
	bool repeat; //if user types "help" or wants to redo the program
	char rptChar; //character to control whether program repeats
	
	printf("Welcome to our program! Enter a number from the list below to start that program,\n");
	printf("or type \"HELP\" to learn more about a specific program.\n");
	printf("\t1) Topics quiz\n\t2) Sustainability game\n\t3) About neural network\n");
	
	
	do{
		printf("\nWhat would you like to do: ");
		scanf("%s", userChoice);
		
		valid = 1; //determines whether the entered value is valid
		repeat = 0; //usually zero unless "help" entered
		
		//compares user's entered value and completes 
		if ( !strncmp(userChoice, "1", 5) )
			QuizMain();
		else if ( !strncmp(userChoice, "2", 5) )
			SustainMain();
		else if ( !strncmp(userChoice, "3", 5) )
			NN();
		else if ( !strncasecmp(userChoice, "HELP", 5) )
		{
			do 
			{
				printf("Enter the number of the program you would like to know more about: ");
				scanf("%d", &helpNum);
				
				if ( helpNum != 1 && helpNum != 2 && helpNum != 3 )
					printf("[ERROR] Please enter an above value!\n");
			} while ( helpNum != 1 && helpNum != 2 && helpNum != 3 );
			
			help( helpNum ); 
			repeat = 1; //will repeat so user can actually select something
		}
		else 
			valid = 0;
		
		//Asks user if they want to repeat the program and redisplays the menu if so
		//This only displays so long as some valid entry is inputted that is not "help"
		if ( repeat != 1 && valid) 
		{
			do
			{
				printf("\n\nWould you like to repeat the program? (y/n) :");
				scanf(" %c", &rptChar);
				
				if (rptChar != 'y' && rptChar != 'n')
					printf("[ERROR] Please enter y or n!\n");
					
				if (rptChar == 'y')
				{
					repeat = 1;
					printf("\t1) Topics quiz\n\t2) Sustainability game\n\t3) About neural network\n");
				}
			} while (rptChar != 'y' && rptChar != 'n');
		}
		
		if ( !valid )
			printf("[ERROR] Please enter a valid command!\n");
		
	} while (!valid || repeat);
	
	printf("\nThank you for using our program!");
	
	return 0;
} //END MAIN


//---------------------------------------------------------------------

void help(int helpNum) //displays correct info based on which number is entered
{
	switch (helpNum)
	{
		case 1:
			printf("The goal of this feature is to allow the user the option to learn about\n");
			printf("different topics covered within our FYEC paper, and complete brief quizzes afterward\n");
			printf("to check their comprehension of the material.\n");
			break;
		case 2:
			printf("Play a game with the topic of sustainability. You will be asked several\n");
			printf("questions relating to sustainability and the number you get correct will\n.");
			printf("displayed at the end.");
			break;
		case 3:
			printf("A wall of text that tells you about how neural networks work. You can go\n"); //I can say this because I made it
			printf("through at your own pace as the program waits for you until it resumes.");
			break;
			
	}
}

void NN (void)
{
	srand(time(0)); //set seed of random numbers to give me randomness in values produced
	double input[3] = {1, 0, 1};
	double weight[3] = {rand0to10(), rand0to10(), rand0to10()};
	double weightSum;
	double sigmoid;
	
	
	welcome();
	
	printf("Every one of the arrows in the diagram carries a \"weight\" value, and every circle, or node,\ncarries an \"activation\" value that is between 0 and 1.\n");
	printf("For this network, we will have three input values, one hidden layer, and two output values. We will work assuming we are training the network to operate like the OR operator.\n");
	printf("This OR operator will have three inputs. If any of the inputs are true (1), the output is expected to be true (1).\n");
	
	wait();
	
	printf("We will provide an input of:\n\t%.0lf\n\t%.0lf\n\t%.0lf\nWe will call this layer the \"current layer\" for now as we step through each layer.\n", input[0], input[1], input[2]);
	printf("All of the weight values (the lines between the nodes) are initially set to be random.\n");
	printf("To find the activation value for each node in the next layer, we take the weighted sum of the activation values at the current layer times the weight value connected to that node.\n"); 
	printf("For example, let's look at the first node in the second layer. To find the activation value for it, we will take the activation values for the input layer, and multiply by the arrow values.\n");
	
	wait();
	
	weightSum = (input[0] * weight[0]) + (input[1] * weight[1]) + (input[2] * weight[2]) - 15;
	printf("Suppose it looks like this, where the values in the parentheses are the weight values connected to the first node in the second layer: \n\t%.0lf (%.2lf)\n\t%.0lf (%.2lf)\n\t%.0lf (%.2lf)\n",input[0], weight[0], input[1], weight[1], input[2], weight[2]);
	printf("Thus, taking the weighted sum, plus some bias (in this case it's 10), of all of these values yields:\n\n\t(%.0lf * %.2lf) + (%.0lf * %.2lf) + (%.0lf * %.2lf) - 15 = %.2lf\n",input[0], weight[0], input[1], weight[1], input[2], weight[2], weightSum); 
	
	wait();
	
	printf("Clearly, this value is not between 0 and 1, which, as we established earlier, is the range for the activation values. Thus, we must use something known as the \"sigmoid,\" or \"squashing\" function. It's called the squashing function because it takes any range of values and \"squashes\" it down to between 0 and 1.\n");
	printf("The function is as follows:\n\n\tsigmoid = 1 / (1 + e^-x)\n\n");
	sigmoid = 1 / (1 + exp( -weightSum ) );
	printf("Plugging our weighted sum into this function yields: %.4lf\n", sigmoid);
	
	wait();
	
	printf("This is now the activation value in the first node in the second layer. This process is repeated for all nodes in the layer, which we won't show for simplicity sake.\n");
	printf("If we look now at the output layer, the same process will be applied for each of these nodes to get our final result. Let' see what our output layer looks like.\n");
	printf("Output layer:\n\t%.2lf\n\t%.2lf", .226, .724); //Hard-coded values as an example of possible output
	
	wait();
	
	printf("If we recall, we desired a function that worked like the OR operator. Thus, we need output nodes that are 0 or 1, which we can that see we did not get.\n");
	printf("This is to be expected since all of our weight values were set randomly and therefore it's natural to get a random output.\n");
	printf("From here, we apply a \"cost\" function to determine just how far the answer is from the actual value. The higer the value is, the more inaccurate the network is.\n");
	printf("Now, we apply concepts of multivariable calculus to find the minimum of this cost function to know how to find the optimal weight values.\n");
	printf("This process repeats over and over until the cost function approaches 0.\n\n");
	
	printf("Thus concludes the explanation of neural networks. Thanks for hanging in there!");
}

void welcome(void) //provides welcome message and link to follow
{
	printf("\n\nWelcome! This program gives insight into how a neural network learns to be able to give a desired output based on input values.\n");
	printf("For this example, please pull up the following image from Wikipedia to naid in understanding (Ctrl + click to follow):\n\n");
	printf("\thttps://en.wikipedia.org/wiki/Neural_network_%%28machine_learning%%29#/media/File:Colored_neural_network.svg\n");
	wait();
}

void wait(void) //allows user to decide when to continue with the program
{
	char proceed;
	printf("\nPress ENTER whenever you are ready to proceed. ");
	scanf("%c", &proceed);
	printf("\n");
}

double rand0to1(void) //returns a random number between 0 and 1
{
	return rand() / ((double)RAND_MAX);
}

double rand0to10(void) //returns a random number between 0 and 10
{
	return rand0to1() * 10;
}


// Function to validate Pitt ID (must be 7 digits)
int validatePittID(char *pittID) {
    int i = 0;
    while (pittID[i] != '\0') {
        if (!isdigit(pittID[i])) {
            return 0; // Pitt ID contains non-digit characters
        }
        i++;
    }
    return i == 7; // Pitt ID must be exactly 7 digits
}


// Function to prompt the user to enter a valid Pitt ID
void enterPittID(char *pittID) {
    do {
        printf("Enter your 7-digit Pitt ID: ");
        scanf("%s", pittID);
    } while (!validatePittID(pittID));
}

//Function to educate about sustainability
void SustainabilityGame() {
    printf("Hello! Today we will be playing a game that revolves around sustainability! Your goal will be to categorize whether an action is sustainable or not\n");
    printf("Which one of these actions is more environmentally friendly?:\n A: Installing solar panels on rooftops to generate electricity \n B: Using coal-powered plants to generate electricity\n C: Dumping waste into rivers and oceans\n");

    char response;
    int count = 0; // Initialize count to zero

    do {
        scanf(" %c", &response); 
        switch (response) {
            case 'a':
            case 'A':
                printf("That's correct! Installing solar panels helps reduce reliance on fossil fuels.\n");
                count++; // Increment count
                break;
            case 'b':
            case 'B':
                printf("Incorrect. Coal-powered plants contribute to air pollution and climate change.\n");
                break;
            case 'c':
            case 'C':
                printf("Incorrect. Dumping waste into water bodies harms aquatic life and ecosystems.\n");
                break;
            default:
                printf("Invalid option! Please choose again.\n");
        }
    } while (response != 'a' && response != 'A' && response != 'b' && response != 'B' && response != 'c' && response != 'C');
    
    printf("What is the term used to describe the practice of planting trees to absorb carbon dioxide and combat climate change?\n A: Deforestation \n B: Reforestation\n C: Desertification\n");
    do {
        scanf(" %c", &response); 
        switch (response) {
            case 'a':
            case 'A':
                printf("Incorrect. Deforestation refers to the removal of trees, which exacerbates climate change.\n");
                break;
            case 'b':
            case 'B':
                printf("That's correct! Reforestation helps mitigate climate change by restoring tree cover.\n");
                count++; // Increment count
                break;
            case 'c':
            case 'C':
                printf("Incorrect. Desertification refers to the process of land turning into desert due to various factors.\n");
                break;
            default:
                printf("Invalid option! Please choose again.\n");
        }
    } while (response != 'a' && response != 'A' && response != 'b' && response != 'B' && response != 'c' && response != 'C');
    
    printf("Which of the following is an example of sustainable agriculture?\n A: Using excessive pesticides and fertilizers that harm soil health\n B: Rotating crops to maintain soil fertility and reduce pests\n C: Clearing large areas of forests for agriculture\n");
    do {
        scanf(" %c", &response); 
        switch (response) {
            case 'a':
            case 'A':
                printf("Incorrect. Excessive use of pesticides and fertilizers can degrade soil quality and harm ecosystems.\n");
                break;
            case 'b':
            case 'B':
                printf("That's correct! Crop rotation is a sustainable farming practice that helps maintain soil health and biodiversity.\n");
                count++; // Increment count
                break;
            case 'c':
            case 'C':
                printf("Incorrect. Deforestation for agriculture leads to loss of biodiversity and contributes to climate change.\n");
                break;
            default:
                printf("Invalid option! Please choose again.\n");
        }
    } while (response != 'a' && response != 'A' && response != 'b' && response != 'B' && response != 'c' && response != 'C');
    
    printf("You chose the best option %d times!\n", count);

}
    
void SustainMain(void) {
    char pittID[10]; // Increased size to accommodate 7 digits 

    enterPittID(pittID);

    printf("Your Pitt ID is valid: %s\n", pittID);
    
    SustainabilityGame();
    
}

void QuizMain(void)
{
	//Define variables
	int topicselection;
	char repeatthisprogram;
	
	do
	{
		//Display the user options for topics to learn about
		printf("\n\nThe following topics are available to learn about:\n1 - Global Solid Waste Issues\n2 - The Solid Waste Management Process\n3 - AMP AI\n");
	
		//Call the SubjectChoicePrompt function and store the result in topicselection
		topicselection = SubjectChoicePrompt();
	
		//Call the TopicLearning function based on the user's choice for topicselection
		TopicLearning(topicselection);
	
		//Call the TopicQuiz function based on the user's choice for topicselection
		TopicQuiz(topicselection);
	
		//Ask the user if they would like to repeat the program to learn about another topic
		do
		{
			printf("Would you like to learn about another topic? (Type y/n)");
			scanf(" %c",&repeatthisprogram);
		} while(repeatthisprogram!='y' && repeatthisprogram!='Y' && repeatthisprogram!='n' && repeatthisprogram!='N');
		
		//Repeat the program if the user answers yes
	} while (repeatthisprogram=='y' || repeatthisprogram=='Y');

}



//Function Definitions



//SubjectChoicePrompt function

int SubjectChoicePrompt(void)
{
	int topicselection;
	
	//Prompt for user response and error check answer
	do
	{
		printf("Enter 1, 2, or 3 to select a topic.\n");
		scanf("%d",&topicselection);
	} while (topicselection<1 && topicselection>3);
	
	//Confirm the user's selection via printed text onscreen
	printf("\nYou have selected topic %d - ",topicselection);
	switch (topicselection)
	{
		case 1:
		printf("Global Solid Waste Issues\n");
		break;
		case 2:
		printf("The Solid Waste Management Process\n");
		break;
		case 3:
		printf("AMP AI\n");
		break;
	}
	
	//Return the user's topic selection to the main for future use
	return topicselection;
}

/**********************************************************************/

//TopicLearning function

void TopicLearning(int topicselection)
{
	switch (topicselection)
	{
		case 1:
		
		//Display relevant info on global solid waste issues
		
		printf("\nGlobal Solid Waste Issues");
		printf("\nIn a rapidly expanding global environment, the issue of solid waste management");
		printf("\nbecomes increasingly more important to manage. On an annual basis, 290 million tons");
		printf("\nof municipal solid waste are generated in America alone, with 50%% of that waste ending");
		printf("\nup in landfills. This contributes to a significant portion of global warming, estimated");
		printf("\nto be close to 25%%. This is in no small part due to the face that less than 10%% of plastics");
		printf("\nin America are recycled.");
		printf("\n\nOf course, America is only a small component of the entire world's solid waste generation- the");
		printf("\nglobal total of all solid waste generated in 2020 was 2.01 billion metric tons, an amount expected");
		printf("\nto rise to 3.4 billion tons by 2050.");
		printf("\n\nBecause of the sheer quantities of solid waste generated on a global level, solid waste");
		printf("\nhas become increasingly difficult to manage, with the extraction of renewable material relying");
		printf("\nheavily on human labor, usually in the form of tedious and dangerous tasks.");
		break;
		case 2:
		
		//Display relevant info on the solid waste management process
		
		printf("\nThe solid waste management process is the process by which disposed items are filtrated and");
		printf("\ndisposed of according to their relevant characteristics. This is necessary because solid");
		printf("\nwaste can vary greatly in terms of origin, material, recyclability, or whether it could");
		printf("\npose a hazard to waste workers or the environment where it could be disposed. The process");
		printf("\ncan generally be broken down into the following 6 steps:");
		printf("\n\n1. Identification - where the presence of waste is identified by collection systems.");
		printf("\n2. Handling - where that waste is collected into garbage bins, dumpsters, and other receptacles.");
		printf("\n3. Collection - where waste workers collect waste from receptacles into garbage trucks or similar systems.");
		printf("\n4. Transport - where the waste is brought to a processing facility where it can be sorted through.");
		printf("\n5. Processing - a key phase where the individual pieces of waste are sorted based on their characteristics.");
		printf("\n6. Disposal - where the filtrated waste is disposed according to the results of the processing phase.");
		break;
		case 3:
		
		//Display relevant info on AMP AI
		
		printf("\nBecause the need for pattern recognition is what forces humans to still be involved in the arduous");
		printf("\ntasks of waste management, AI has emerged as a possible substitute in terms of pattern recognition");
		printf("\nthat could alleviate this need and streamline the solid waste management process.");
		printf("\n\nAMP AI is one such AI platform, developed by AMP Robotics. It''s capable of real-time capturing of");
		printf("\nrelevant waste materials using a camera feed of a continuous stream of waste. This camera feed is");
		printf("\nconnected to an image recognition platform called AMP Neuron, which compares the feed with existing");
		printf("\ntraining data to filtrate materials based on shape, size, brand, or up to 100 possible customizable");
		printf("\ncharacteristics. The resulting data is sent to a physical probe system called AMP CortexTM, which");
		printf("\nseparates individual waste items at a rate of 80 items per minute, at 99%% accuracy. This allows for");
		printf("\n90%% of the waste processing phase to take place without touching human hands.");
		printf("\n\nAMP Robotics has installed over 300 robotics systems across 100 total facilities, spanning multiple");
		printf("\ncontinents. At its current rate of operations, AMP sorts over 90 billion items annually, with each");
		printf("\nindividual system priced at approximately $300,000, which is significantly cheaper than the equivalent");
		printf("\nwage of multiple salaried workers over the course of multiple years of use.");
		break;
	}
}
	
//*********************************************************************

//TopicQuiz function

void TopicQuiz(int topicselection)
{
	int userscore=0;
	char userletterchoice, tfanswer, mcanswer;
	
	do
	{
		//Prompt the user to take a quiz and error check their response
		printf("\nWould you like to take a brief quiz on the material you just read? (Enter y/n)\n");
		scanf(" %c",&userletterchoice);
	} while (userletterchoice!='y' && userletterchoice!='Y' && userletterchoice!='n' && userletterchoice!='N');
	
	//If the user answers "yes," provide them with a brief quiz based on their topic selection
	if (userletterchoice=='y' || userletterchoice=='Y')
	{
		switch (topicselection)
		{
			case 1:
			
			//Ask the first question (true or false)
			printf("\nTrue or False: Because of increasing populations globally, solid waste management will become less of an issue in the future. (answer T/F)\n");
			scanf(" %c",&tfanswer);
			
			//Provide the user with feedback based on their answer
			if (tfanswer=='f' || tfanswer=='F')
			{
				printf("Correct - increasing global populations mean that solid waste management will become more of an issue in the future.\n");
				userscore=userscore+1;
			}
			else
			{
				printf("Incorrect - increasing global populations mean that solid waste management will become more of an issue in the future.\n");
			}
			
			//Ask the second question(multiple choice)
			printf("\nHow much solid waste does the US generate on an annual basis?\nA - 290 tons\nB - 290,000 tons\nC - 290,000,000 tons\nD - 290,000,000,000 tons\n");
			scanf(" %c",&mcanswer);
			
			//Provide the user with feedback based on their answer
			if (tfanswer=='c' || tfanswer=='C')
			{
				printf("Correct - the US generates 290,000,000 tons of solid waste anually\n");
				userscore=userscore+1;
			}
			else
			{
				printf("Incorrect - the US generates 290,000,000 tons of solid waste anually\n");
			}
			break;
			
			case 2:
			
			//Ask the first question (true or false)
			printf("\nTrue or False:  Solid Waste Management does not require a great degree of precision due to the lack of\nvariety between solid waste. (answer T/F)\n");
			scanf(" %c",&tfanswer);
			
			//Provide the user with feedback based on their answer
			if (tfanswer=='f' || tfanswer=='F')
			{
				printf("Correct - Solid waste can vary greatly in terms of origin, material, potential risk, and other factors.\n");
				userscore=userscore+1;
			}
			else
			{
				printf("Incorrect - Solid waste can vary greatly in terms of origin, material, potential risk, and other factors.\n");
			}
			
			//Ask the second question(multiple choice)
			printf("\nWhat is the fifth stage in the solid waste management process, which focuses on classifying and sorting waste?\nA - Identification\nB - Processing\nC - Sortation\nD - Filtration\n");
			scanf(" %c",&mcanswer);
			
			//Provide the user with feedback based on their answer
			if (tfanswer=='b' || tfanswer=='B')
			{
				printf("Correct - The processing phase is where waste is sorted based on its relevant characteristics.\n");
				userscore=userscore+1;
			}
			else
			{
				printf("Incorrect - The processing phase is where waste is sorted based on its relevant characteristics.\n");
			}
			break;
			
			case 3:
			
			//Ask the first question (true or false)
			printf("\nTrue or False: AMP AI comes with the risk of human workers losing their jobs. (answer T/F)\n");
			scanf(" %c",&tfanswer);
			
			//Provide the user with feedback based on their answer
			if (tfanswer=='t' || tfanswer=='T')
			{
				printf("Correct - AI developments unfortunately often come with the downside of a loss of employment for workers.\nHowever, it''s important to consider whether these developments may in turn open up new job opportunities, or whether\nthese jobs may not be ideal for humans to work due to unsatisfying conditions.\n");
				userscore=userscore+1;
			}
			else
			{
				printf("Incorrect - AI developments unfortunately often come with the downside of a loss of employment for workers.\nHowever, it''s important to consider whether these developments may in turn open up new job opportunities, or whether\nthese jobs may not be ideal for humans to work due to unsatisfying conditions.\n");
			}
			
			//Ask the second question(multiple choice)
			printf("\nWhich feature of AMP AI is a database from which the system can classify trash?\nA - AMP AI\nB - AMP Neuron\nC - AMP CortexTM\nD - AMP DataBrain\n");
			scanf(" %c",&mcanswer);
			
			//Provide the user with feedback based on their answer
			if (tfanswer=='b' || tfanswer=='B')
			{
				printf("Correct - AMP Neuron is a database that houses the system''s training data, allowing AMP to classify the trash it sees.\n");
				userscore=userscore+1;
			}
			else
			{
				printf("Incorrect - AMP Neuron is a database that houses the system''s training data, allowing AMP to classify the trash it sees.\n");
			}
			break;
		}
		
		//Provide the user with feedback based on their score
		
		printf("You answered %d questions correctly.",userscore);
		if (userscore==2)
		{
			printf(" Great job!\n");
		}
		else
		{
			printf("\n");
		}
	}
}