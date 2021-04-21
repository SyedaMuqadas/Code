# Code
ChutesAndLadder
package SystemDesign.SnakeAndLadder;
import java.io.*;
	
public class Snakesandladder {
	
	/*Name: Syeda Muqadas
	Date: March,2021
	Purpose: To make snake and ladder board game using methods */

	public static void main(String[] args) throws IOException {

	BufferedReader myInput2 = new BufferedReader (new InputStreamReader (System.in));
	 // Print the welcome screen and instructions

	        System.out.println ("\n\t\tWelcome To chutes And Ladders");
	        System.out.println("\t\t-------------------------------\n");
	        System.out.println ("Instructions:");
	        System.out.println("--------------");
	        System.out.println ("\t This program is a chutes and ladders game, where you will be");
	        System.out.println ("\t playing with computer. The game start at 1 for both players, ");
	        System.out.println ("\t and the first one to reach 100 will win. However, there will ");
	        System.out.println ("\t be preset squares which will be the chutes or ladders. Once you");
	        System.out.println ("\t land on top of a chute you go down a few squares, and move up if");
	        System.out.println ("\t you land on the bottom of a ladder.");
	        System.out.println("\t---------------------------------------------------------------------");
	       
	        int counter= 100,iteration=-1; // sets the counter and iteration variables to be used in making the board
	        System.out.println ("-------------------------------Game Board---------------------------------");
	       
	        /*
	        This while loop makes the board for the player to visualize what the
	        game looks like, it uses a counter to increment or decrement by 1.
	        It will also subtract by 9 or 10 when necessary to create a board
	        exactly like the one given.
	        */
	        while (counter > 0){// start while
	            if (counter%10 == 0 && counter != 100){// checks if the counter is at a 90, or 80...
	                if(iteration==-1)
	                {
	                    // subtract 9 from the counter
	                    // and sets it to start adding by one
	                    counter-=9;
	                    iteration=1;
	                }
	                else
	                {
	                    System.out.print(counter+"\t");
	                    counter-=10;
	                    iteration=-1; // set the counter to start subtract by ones
	                }
	                if(counter!=0)
	                System.out.print("\n" + counter + "\t"); // just prints out the counter with a line breck
	            }
	            else
	            System.out.print(counter + "\t"); // just prints out the counter
	            counter+=iteration; // sets counter to add by iteration
	        }// end while
	        System.out.println();
	        System.out.println ("----------------------------------------------------------------------------");
	       
	      String sGame = "yes"; // declare variable used to ask user if he wants to play
	       
	        System.out.print ("Do you want to play? Yes or No     >  "); // ask user if we wants to play the game
	        sGame = myInput2.readLine (); // reads the user's input into the variable sGame
	        System.out.print ("\n\n\n\n\n\n");
	        while (sGame.equals ("yes") || sGame.equals ("Yes"))//to make sure it is equal
	        {
	        sGame = startGame(sGame); //startGame variable 
	        }
	        System.out.println ("\n\n\n\n\t\t\t\t\t\tNext Time ;)"); //if No
	       
	       
	       
	   
	       
	}//main

	   
	    /*
	    startGame method:
	  ------------------- 
	    This method will set the chutes and ladder location and ask the user if
	    they want to continue after each move. it will return the values to the
	    main method, which will reset the game to make another move.
	    */
	    public static String startGame (String start) throws IOException {
	       
	        BufferedReader myInput = new BufferedReader (new InputStreamReader (System.in));
	       
	   
	        int userPosition = 1; // sets the location for user's piece to 1
	        int compPosition = 1; // sets the location for computer's piece to 1
	        int diceRoll = 0; // creates the first die
	        int diceRoll2 = 0; // creates the second die
	        int userRoll = 1; // declares what the user rolled
	        int compRoll = 1; // declares what the computer rolled
	        String playAgain = "yes"; //play again variable
	       
	        // declare all the snakes and ladders in a array
	        int chutesLaddersArray [] = new int [6]; // create a 6 element array
	        // store the snakes and ladders location in the array
	        chutesLaddersArray [0] = 54;
	        chutesLaddersArray [1] = 90;
	        chutesLaddersArray [2] = 99;
	        chutesLaddersArray [3] = 9;
	        chutesLaddersArray [4] = 40;
	        chutesLaddersArray [5] = 67;
	       
	       
	        while (playAgain.equals ("yes") || playAgain.equals ("Yes")) // while loop for setting variable equals "yes" or "Yes".
	        {
	           
	           
	            // gets the dice roll for user and computer
	            userRoll =  getDice(diceRoll, diceRoll2); // sends data to a function type method called getDice
	            compRoll =  getDice(diceRoll, diceRoll2); // same for the computer
	            System.out.println("-------------------------------------------------------------------------------------------------------------------");
	            System.out.println ("\t\t\t\t\t------------------------------------------");
	            System.out.println ("\t\t\t\t\t|\tYou Rolled a " + userRoll + "\t\t|"); // print the user's roll number
	            System.out.println ("\t\t\t\t\t|\tThe Computer Rolled a " + compRoll + "\t|"); // print the roll that computer got 
	            System.out.println ("\t\t\t\t\t------------------------------------------");
	           
	            // hold the user's last position for switching back if current position was greater than 100
	            userPosition = userPosition + userRoll;
	           
	            // hold the computer's last position for switching back if current position was greater than 100
	            compPosition = compPosition + compRoll;
	           
	           
	           
	            // check to see if user landed on top of a snake or at the bottom of a ladder
	            userPosition = getP(userPosition, userRoll, chutesLaddersArray); // give getP parameters, and receive a final value which can be printed out
	            // The same goes for compPosition, however compgetP gets an additional
	            // parameter (userPosition) to check if user has already won
	            compPosition = compgetP(compPosition, compRoll, chutesLaddersArray, userPosition);
	           
	            System.out.println("\t\t\t*************************************************************************");
	            System.out.println ("\t\t\t*\t\tYou are currently on " + userPosition + "\t\t\t*"); // print out the user's current location
	            System.out.println ("\t\t\t*\t\tThe Computer is currently on " + compPosition + "\t\t*"); // print out the computer's current location
	            System.out.println("\t\t\t*************************************************************************");
	           
	            // resets the position values, if the user or the computer won
	            // so that the user could play the entire game again if they wanted to
	            if (userPosition == 100 || compPosition == 100)
	            {
	                userPosition = 1;
	                compPosition = 1;
	                // asks the user if we wants to play again
	                System.out.print ("Do you want to play? Yes or No     >  ");
	                playAgain = myInput.readLine ();
	                System.out.print ("\n\n\n\n\n\n\n\n\n\n\n\n");
	            }
	            else
	            {
	                // asks the user if we wants to continue playing
	                System.out.print ("Do you want to play? Yes or No     >  ");
	                playAgain = myInput.readLine ();
	               
	            }
	           
	           
	        }// end playAgain While
	       
	        return playAgain; // returns parameter "playAgain" to main. if user wants to play again
	    }// end startGame method
	   
	    /*
	    getDice method:
	   ----------------
	    This method generates two random numbers between 1 and 6, then
	    adds them to get a final roll. It returns the value to be
	    displayed on the screen.
	    */
	    public static int getDice (int diceRoll, int diceRoll2)
	    {// start getDies class
	        diceRoll = (int)(Math.random()*6 )+1 ; //creates dice roll number 1
	        diceRoll2 = (int)(Math.random()*6 )+1 ; //creates dice roll number 2
	        int move = diceRoll + diceRoll2; // adds the two dice rolls to get a final move
	        return move; // return parameter move, it gives the final dice roll back to startGame
	    }// end getDice class
	   
	   

/*	    getP method:
	  -------------- 
	    This method is responsible for checking if the USER is on
	    top of a chute, or at the bottom of a ladder, and then
	    adjusting the user's position to match the chute or
	    ladders value.
	    */
	    public static int getP (int userPosition, int userRoll, int chutesLaddersArray []) throws IOException 
	    {
	       
	       
	        if(userPosition == chutesLaddersArray[0]) //if position equals chute 1
	        {
	            userPosition = 19; // set new position on reaching chute
	            System.out.println ("\t\t\t\t******** {You are on Chute, GO DOWN!!!} ****************");
	        }
	        else if (userPosition == chutesLaddersArray[1]) //if position equals chute 2
	        {
	            userPosition = 48; // set new position on reaching chute
	            System.out.println ("\t\t\t\t********* {You are on Chute, GO DOWN!!!} ***************");
	           
	        }
	        else if (userPosition == chutesLaddersArray[2]) //if position equals chute 3
	        {
	            userPosition = 77; // set new position on reaching chute
	            System.out.println ("\t\t\t\t********* {You are on Chute, GO DOWN!!!} ***************");
	        }
	        else if (userPosition == chutesLaddersArray[3]) //if position equals ladder 1
	        {
	            userPosition = 34; // set new position on reaching ladder
	            System.out.println ("\t\t\t\t^^^^^^^^^^^ {You Got A Ladder!! GO UP!!!} ^^^^^^^^^^^^^^");
	           
	        }
	        else if (userPosition == chutesLaddersArray[4]) //if position equals ladder 2
	        {
	            userPosition = 64; // set new position on reaching ladder
	            System.out.println ("\t\t\t\t^^^^^^^^^^^ {You Got A Ladder!! GO UP!!!} ^^^^^^^^^^^^^^");
	           
	        }
	        else if (userPosition == chutesLaddersArray[5]) //if position equals ladder 3
	        {
	           
	           
	            userPosition = 86; // set new position on reaching ladder
	            System.out.println ("\t\t\t\t^^^^^^^^^^^ {You Got A Ladder!! GO UP!!!} ^^^^^^^^^^^^^^");
	        }
	       
	        if (userPosition < 0 || userPosition > 112) 
	        {
	            System.out.println ("An error has occured please reset the game!!!!!!");
	        }
	       
	        else if (userPosition > 100) // checks if user's location is greater then a 100
	        {
	            userPosition = userPosition - userRoll; // subtract userRoll from the user position to get back to old position
	            System.out.println ("OHHH You cant jump, you must land on a 100"); // print users current location
	           
	        }
	        else if (userPosition == 100)
	        {
	            System.out.println ("YOU WON, GOOD JOB!!!"); // printing if user won
	           
	        }
	       
	       
	       
	        return userPosition; 
	    }// end getP
	   
	   
	   
	   
	   
	   
	    /*
	    compgetP method:
	  ------------------- 
	    This method is similar to the user's position method but it is for computer moves.
	    */
	   
	    public static int compgetP (int compPosition, int compRoll, int chutesLaddersArray [], int userPosition) throws IOException
	    {
	        
	       
	        if(compPosition == chutesLaddersArray[0])
	        {
	            compPosition = 19;
	            System.out.println ("\t\t\t\t~~~~~~~~~~~~~Computer is on chute, it GO DOWN!!!~~~~~~~~~~~~~");
	           
	           
	        }
	        else if (compPosition == chutesLaddersArray[1])
	        {
	            compPosition = 48;
	            System.out.println ("\t\t\t\t~~~~~~~~~~~~~Computer is on chute, it GO DOWN!!!~~~~~~~~~~~~");
	           
	        }
	        else if (compPosition == chutesLaddersArray[2])
	        {
	            compPosition = 77;
	            System.out.println ("\t\t\t\t~~~~~~~~~~~~Computer is on chute, it GO DOWN!!!~~~~~~~~~~~");
	        }
	        else if (compPosition == chutesLaddersArray[3])
	        {
	            compPosition = 34;
	            System.out.println ("^^^Computer Got TO A Ladder, it WENT UP!!!^^^");
	        }
	        else if (compPosition == chutesLaddersArray[4])
	        {
	            compPosition = 64;
	            System.out.println ("^^^Computer Got TO A Ladder, it WENT UP!!!^^^");
	           
	        }
	        else if (compPosition == chutesLaddersArray[5])
	        {
	            compPosition = 86;
	            System.out.println ("^^^Computer Got TO A Ladder, it WENT UP!!!^^^");
	        }
	       
	       
	        if (compPosition < 0 || compPosition > 112) 
	        {
	            System.out.println ("Error: Please reset the game!!!!!!");
	        }
	       
	        else if (compPosition > 100) // checks if computers's location is greater then a 100
	        {
	            compPosition = compPosition - compRoll; // get old position
	            System.out.println ("THE COMPUTER CAN'T move forward!!! it must've land on a 100"); 
	           
	        }
	        else if (compPosition == 100 && userPosition != 100)
	        {
	            System.out.println ("THE COMPUTER WON, YOU FAILED!!!"); 
	           
	        }
	       
	        return compPosition; // return the final position to starGame
	    } // end compgetP

	}//Class chutesAndLadder
