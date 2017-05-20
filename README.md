# RabbitHole


1.	Rabbit Hole
Rabbit hole is a term for a portal for time travel. 
You are trying to go back in the past to prevent Kennedy’s assassination. But first you should find the rabbit hole. Your energy is limited and if you exhaust it, you will be tired and can’t continue the mission.
You will be given an array of strings representing different obstacles you should overcome. 
•	“Left|[integer value]”-you should jump to the left with [integer value] positions and decrease your energy with [integer value];
•	“Right|[integer value]”-you should jump to the right with [integer value] positions and decrease your energy with [integer value];
•	“Bomb|[integer value]”-the bomb explodes and this element of the array should be removed, your energy should be decreased be the [integer value], you should start from the beginning (index 0);
•	“RabbitHole” – you have found the rabbit hole, the program should stop here, print on the console – “You have 5 years to save Kennedy!”
 
Your mission begins at the first element of the array. The rabbit hole will be only one.
The program ends when you find the rabbit hole or when your energy is gone. And if it is gone due to bomb explosion you should print “You are dead due to bomb explosion!” on the console or if it is due jumps print
“You are tired. You can't continue the mission.”.
After every move someone puts a bomb at the end of the array with [integer value] of your current energy (the last element is removed and the bomb is placed there, but when the last element is the “RabbitHole”, it can’t be removed and the bomb is placed after it).



Input / Constrains
•	First line – space separated string values consists the obstacles you should overcome.
•	Second line – integer value representing your initial energy in range [0-100].
Output
•	If you find the Rabbit Hole you should print: “You have 5 years to save Kennedy!”;
•	If you die due to bomb explosion (your energy is gone, after a bomb explosion): “You are dead due to bomb explosion!”;
•	If you are tired (your energy is gone, after a jump): “You are tired. You can't continue the mission.” .





Examples

Input	                                                      
RabbitHole Left|100 Right|10 Bomb|10 Left|11

100	 
	Output         You have 5 years to save Kennedy!

Input
Right|100 Left|10 Bomb|11 RabbitHole Bomb|10 Left|2

80	
	Output   You are tired. You can't continue the mission.

-----------------------------------------------------------------------------------------------------------------------------

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Scanner;

public class RabbitHole {

	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		
		String[] array = scan.nextLine().split(" ");
		List<String> action = new ArrayList<>(Arrays.asList(array));
		int energy = Integer.parseInt(scan.nextLine());
		scan.close();
		
		int currentIndex = 0;
		boolean lastBomb = false;
		
		while (energy > 0) {

			lastBomb = false;
			String[] currentParams = action.get(currentIndex).replace("|", "-").split("-");
			String command = currentParams[0];
			
			if (command.equals("RabbitHole")) {
				System.out.println("You have 5 years to save Kennedy!");
				break;
			} 
			
			int value = Integer.parseInt(currentParams[1]);
			
			switch (command) {
			case "Left":
				currentIndex = Math.abs((currentIndex - value) % action.size());
				energy -= value;
				break;
			case "Right":
				currentIndex = (currentIndex + value) % action.size();
				energy -= value;
				break;
			case "Bomb":
				action.remove(currentIndex);
				currentIndex = 0;
				energy -= value;
				lastBomb = true;
				break;
			}		
			
			if (!action.get(action.size() - 1).equals("RabbitHole") ) {
				action.remove(action.size() - 1);
			}
				action.add("Bomb|" + energy);
			
			if (energy <= 0 && lastBomb) {
				System.out.println("You are dead due to bomb explosion!");
				
			} else if (energy <= 0 && !lastBomb) {
				System.out.println("You are tired. You can't continue the mission.");
			}
		}
		
	}
}



	      
