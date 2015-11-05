# ATM
simple java atm
package pack;

import java.util.Scanner;

public class AssignmentTakeMyMoney {

	static String name1 = "user1";
	static String pin1 = "1111";
	static int cashAmount1 = 100;

	static String name2 = "user2";
	static String pin2 = "2222";
	static int cashAmount2 = 200;

	static String name3 = "user3";
	static String pin3 = "3333";
	static int cashAmount3 = 300;
	static Scanner keyboard;

	public static void main(String[] args) {
		keyboard = new Scanner(System.in);

		System.out.println("Enter client name: ");
		String nameInput = keyboard.next();

		while (getClientIfExists(nameInput) == 0) {
			System.out.println("This client doesn't exist. Enter client name: ");
			nameInput = keyboard.next();
		}

		int numberOfTries = 3;
		while (numberOfTries != 0) {
			System.out.println("Enter pin to login");
			String pinInput = keyboard.next();

			int clientId = checkAndReturnClient(nameInput, pinInput);
			if (clientId == 0) {
				numberOfTries--;
				System.out.println("Pin incorect. Try again. " + (numberOfTries) + " tries left");
			} else {
				System.out.println("Welcone client " + nameInput);
				numberOfTries = 3;
				while (true) {
					System.out.println("Select operation: 1 to check amount, 2 to widraw, 3 to deposit, 0 to exit");
					String operationId = keyboard.next();
					if (!operationId.equalsIgnoreCase("0") && !operationId.equalsIgnoreCase("1")
							&& !operationId.equalsIgnoreCase("2") && !operationId.equalsIgnoreCase("3")) {
						System.out.println("Invalid operation: " + operationId);
						continue;
					}
					if (operationId.equalsIgnoreCase("0")) {
						System.out.println("Bye client " + nameInput);
						return;
					} else {
						printOperation(operationId);
						if (operationId.equalsIgnoreCase("1")) {
							System.out.println("You have " + getAmount(clientId));
						}

						if (operationId.equalsIgnoreCase("2")) {
							System.out.println("Enter amount to be widraw");
							int widrawAmount = keyboard.nextInt();
							if (canWidraw(clientId, widrawAmount)) {
								widrawAmount(clientId, widrawAmount);
							} else {
								System.out.println("Insuficient funds. ");
								continue;
							}
						}

						if (operationId.equalsIgnoreCase("3")) {
							System.out.println("Enter amount to be deposited");
							int depositAmount = keyboard.nextInt();
							depositAmount(clientId, depositAmount);
						}
					}

				}

			}
		}
		if (numberOfTries == 0) {
			System.out.println("You had 3 failed attempts to login.");
		}
		System.out.println("Bye");
	}

	/*
	 * Returns 1,2,3 corresponding to a client or 0 if no client was identified
	 */
	public static int checkAndReturnClient(String name, String pin) {

		if (name1.equals(name) && pin1.equals(pin)) {
			return 1;
		}
		if (name2.equals(name) && pin2.equals(pin)) {
			return 2;
		}
		if (name3.equals(name) && pin3.equals(pin)) {
			return 3;
		}
		return 0;
	}

	public static void printOperation(String operationId) {
		if (operationId.equalsIgnoreCase("1")) {
			System.out.println("Display amount");
		}

		if (operationId.equalsIgnoreCase("2")) {
			System.out.println("Widraw mondey");
		}

		if (operationId.equalsIgnoreCase("3")) {
			System.out.println("Deposit money");
		}

	}

	public static String getClientName(int clientId) {
		if (clientId == 1) {
			return name1;
		}
		if (clientId == 2) {
			return name2;
		}
		if (clientId == 3) {
			return name3;
		}

		return "Error";
	}

	public static int getAmount(int clientId) {
		if (clientId == 1) {
			return cashAmount1;
		}
		if (clientId == 2) {
			return cashAmount2;
		}
		if (clientId == 3) {
			return cashAmount3;
		}

		return -1;
	}

	public static void widrawAmount(int clientId, int widrawAmount) {
		if (clientId == 1) {
			cashAmount1 = cashAmount1 - widrawAmount;
		}
		if (clientId == 2) {
			cashAmount2 = cashAmount2 - widrawAmount;
		}
		if (clientId == 3) {
			cashAmount3 = cashAmount3 - widrawAmount;
		}
	}

	public static void depositAmount(int clientId, int depositAmount) {
		if (clientId == 1) {
			cashAmount1 = cashAmount1 + depositAmount;
		}
		if (clientId == 2) {
			cashAmount2 = cashAmount2 + depositAmount;
		}
		if (clientId == 3) {
			cashAmount3 = cashAmount3 + depositAmount;
		}
	}

	public static boolean canWidraw(int clientId, int widrawAmount) {
		if (clientId == 1) {
			if (cashAmount1 >= widrawAmount) {
				return true;
			}
		}
		if (clientId == 2) {
			if (cashAmount2 >= widrawAmount) {
				return true;
			}
		}
		if (clientId == 3) {
			if (cashAmount3 >= widrawAmount) {
				return true;
			}
		}
		return false;
	}

	public static int getClientIfExists(String clientName) {
		if (name1.equalsIgnoreCase(clientName)) {
			return 1;
		}
		if (name2.equalsIgnoreCase(clientName)) {
			return 2;
		}
		if (name3.equalsIgnoreCase(clientName)) {
			return 3;
		}
		return 0;
	}

}
