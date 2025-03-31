//Zackery Hengartner
//EECS 1510
// 4/9/24
//Dr. Hobbs
//This program description below:
/*
 * program will read inputs line by line from a text file
 * the file for input will be input.txt
 * according to the inputs if an output happens it will go to the console as well as a file know as output.txt
 * that will be printed there using PrintWriter
 * starting with a try block, while there is input on the file, the first input will be the string for which
 * object is being selected. a switch statement will decide which of the objects match to the input.
 * cases for each object will correlate to the ones from the handout.
 * when a user inputs zero it will break the first and second switches to leave the loop.
 * if there is an error it will print the message of the error then termninate the program 
 */
import java.io.*;
import java.util.*;
public class Project2
{

	public static void main(String[] args) throws Exception
	{
		File file = new File("input.txt"); //File for input.txt that holds the inputs from user
		PrintWriter outputFile = new PrintWriter("output.txt"); //printwriter that will print to output.txt file
		Scanner input; //scanner called input
		
		//use try, this will be a very big block
		
		try //try block
		{
			input = new Scanner(file); //input using scanner of the file for inputs
			while(input.hasNext())
			{
				String objectSelection = input.nextLine(); //objectselection to figure out what object is being made
				//use switch based on the input object "customer", "employee", "loan", "checking", etc.
				
				switch(objectSelection) //switch that analyzes what object is being made
				{
				case "Customer": //if the user decides to create customer object
				{
					int constructorSelection = Integer.parseInt(input.nextLine()); //input that decides what constructor to use
					Customer newCustomer = null; //customer object that is set to null
					if(constructorSelection == 1) //if the number is 1 create a new object with parameters
					{
						newCustomer = new Customer(input.nextLine(), input.nextLine(), input.nextLine()); //create customer object with parameters
					}
					else //only has 1 constructor so error if its anything but 1
					{
						throw new Exception("error");
					}
					int methodSelection; //variable to figure out which method is being used
					do
					{
						methodSelection = Integer.parseInt(input.nextLine()); //get the input and parses as int to see what number method
						switch(methodSelection) //switch statement for each method that customer can use
						{
						case 0: //there is no 0 method so break if user inputs this
							break;
						case 1: //print the name to the file and the console
							outputFile.println(newCustomer.getName());
							System.out.println(newCustomer.getName());
							break;
						case 2: //getaddress and print it to the file and console
							outputFile.println(newCustomer.getAddress());
							System.out.println(newCustomer.getAddress());
							break;
						case 3: //get license number and print it to the file and console
							outputFile.println(newCustomer.getLicenseNumber());
							System.out.println(newCustomer.getLicenseNumber());
							break;
						case 4://set name and use input from user
							newCustomer.setName(input.nextLine());
							break;
						case 5://set address using input from user
							newCustomer.setAddress(input.nextLine());
							break;
						case 6: //set license number using input from user
							newCustomer.setLicenseNumber(input.nextLine());
							break;
						default: //throw exception if anything over 6
							throw new Exception("error");
						}
					} while(methodSelection != 0); //while the method being selected is not 0, if zero break
					break;
				}
				case "Employee": //if the user decides to make employee object
				{
					int constructorSelection = Integer.parseInt(input.nextLine()); //input that decides what constructor to use
					Employee newCustomer = null; //employee object that is set to null
					if(constructorSelection == 1) //only 1 constructor so if not 1 then throw error
					{
						newCustomer = new Employee(input.nextLine(), input.nextLine(), input.nextLine(), Integer.parseInt(input.nextLine())); //create employee object
					}
					else 
					{
						throw new Exception("error");
					}
					int methodSelection;
					do
					{
						methodSelection = Integer.parseInt(input.nextLine()); //user input a number that correlates to case for method selection
						switch(methodSelection) //switch statemetn on what method is being selected
						{
						case 0: //no 0 method so break
							break;
						case 1: //get name and print to file and console
							outputFile.println(newCustomer.getName());
							System.out.println(newCustomer.getName());
							break;
						case 2: //get address and print to file and console
							outputFile.println(newCustomer.getAddress());
							System.out.println(newCustomer.getAddress());
							break;
						case 3: //get license number and print to file and console
							outputFile.println(newCustomer.getLicenseNumber());
							System.out.println(newCustomer.getLicenseNumber());
							break;
						case 4://get EmployeeID and print to file and console with certain length adding zeros if less than length
							outputFile.printf("%08d\n",newCustomer.getEmployeeID());
							System.out.printf("%08d\n",newCustomer.getEmployeeID());
							break;
						case 5: //sets name from input
							newCustomer.setName(input.nextLine());
							break;
						case 6: //sets address from input
							newCustomer.setAddress(input.nextLine());
							break;
						case 7: //sets license number from input
							newCustomer.setLicenseNumber(input.nextLine());
							break;
						case 8: //setemployeeId
							String s = input.nextLine();
							if (s.length() > 9) //if the integer from input is greater than integer overflow throw error
							{
								throw new Exception("error");	
							}
							newCustomer.setEmployeeID(Integer.parseInt(s));
							break;
						default:
							throw new Exception("error");
						}
					} while(methodSelection != 0);
					break;
				}
				case "Loan":
				{
					int constructorSelection = Integer.parseInt(input.nextLine()); //input that decides what constructor to use
					Loan newCustomer = null; //Loan object that is set to null
					if(constructorSelection == 1) //constructor 1
					{
						newCustomer = new Loan(input.nextLine());
					}
					else if (constructorSelection == 2) //constructor 2
					{
						newCustomer = new Loan(Long.parseLong(input.nextLine()), Double.parseDouble(input.nextLine()), Double.parseDouble(input.nextLine()), Integer.parseInt(input.nextLine()), input.nextLine());
					}
					else //any other number = error
					{
						throw new Exception("error");
					}
					int methodSelection;
					do
					{
						methodSelection = Integer.parseInt(input.nextLine());
						switch(methodSelection)
						{
						case 0:
							break;
						case 1: 
							outputFile.printf("%.2f\n\n",newCustomer.getAccountBalance());
							System.out.printf("%.2f\n\n",newCustomer.getAccountBalance());
							break; //get acc balanace with two decimal places
						case 2:
							outputFile.printf("%010d\n",newCustomer.getAccountNumber());
							System.out.printf("%010d\n",newCustomer.getAccountNumber());
							break;//get account number with length required adding zeros if needs
						case 3:
							outputFile.println(newCustomer.getAnnualInterestRate());
							System.out.println(newCustomer.getAnnualInterestRate());
							break;//get annual interest rate
						case 4:
							outputFile.println(newCustomer.getNumberOfYears());
							System.out.println(newCustomer.getNumberOfYears());
							break;//get number of years
						case 5:
							outputFile.println(newCustomer.getLoanDate());
							System.out.println(newCustomer.getLoanDate());
							break;//get loan date
						case 6:
							outputFile.println(newCustomer.getName());
							System.out.println(newCustomer.getName());
							break;//get name
						case 7:
							newCustomer.setAccountBalance(Double.parseDouble(input.nextLine()));
							break;//set account balance
						case 8:
							newCustomer.setAnnualInterestRate(Double.parseDouble(input.nextLine()));
							break;//set annual interest rate
						case 9:
							newCustomer.setNumberOfYears(Integer.parseInt(input.nextLine()));
							break;//set number of years
						case 10:
							outputFile.printf("%.2f\n",newCustomer.getMonthlyPayment());
							System.out.printf("%.2f\n",newCustomer.getMonthlyPayment());
							break;//get monthly payment rounding to decimal places
						case 11:
							outputFile.printf("%.2f\n",newCustomer.getTotalPayment());
							System.out.printf("%.2f\n",newCustomer.getTotalPayment());
							break;//get total payment round to two decimal places
						default:
							throw new Exception("error");
						}
					} while(methodSelection != 0);
					break;
				}
				case "Checking":
				{
					int constructorSelection = Integer.parseInt(input.nextLine()); //input that decides what constructor to use
					Checking newCustomer = null; //Checking object that is set to null
					if(constructorSelection == 1) //constructor 1
					{
						newCustomer = new Checking(Double.parseDouble(input.nextLine()), input.nextLine());
					}
					else if (constructorSelection == 2) //constructor 2
					{
						newCustomer = new Checking(Long.parseLong(input.nextLine()),Double.parseDouble(input.nextLine()), Double.parseDouble(input.nextLine()), input.nextLine());
					}
					else //any other number = error
					{
						throw new Exception("error");
					}
					int methodSelection;
					do
					{
						methodSelection = Integer.parseInt(input.nextLine());
						switch(methodSelection)
						{
						case 0:
							break;
						case 1:
							outputFile.printf("%.2f\n",newCustomer.getAccountBalance());
							System.out.printf("%.2f\n",newCustomer.getAccountBalance());
							break; //get acc balanace with two decimal places
						case 2:
							outputFile.printf("%010d\n",newCustomer.getAccountNumber());
							System.out.printf("%010d\n",newCustomer.getAccountNumber());
							break;//get account num
						case 3:
							newCustomer.setAccountBalance(Double.parseDouble(input.nextLine()));
							break;//set account balance
						case 4:
							outputFile.println(newCustomer.getAnnualInterestRate());
							System.out.println(newCustomer.getAnnualInterestRate());
							break;//get annual interest rate
						case 5:
							outputFile.println(newCustomer.getName());
							System.out.println(newCustomer.getName());
							break;//get name
						case 6:
							newCustomer.setAnnualInterestRate(Double.parseDouble(input.nextLine()));
							break;//set annual interest rate
						case 7:
							newCustomer.makeDeposit(Double.parseDouble(input.nextLine()));
							break;//make deposit
						case 8:
							newCustomer.makeWithdrawal(Double.parseDouble(input.nextLine()));
							break;//make withdrawal
						default:
							throw new Exception("error");
						}
					} while(methodSelection != 0);
					break;
				}
				case "Savings":
				{
					int constructorSelection = Integer.parseInt(input.nextLine()); //input that decides what constructor to use
					Savings newCustomer = null; //Savings object that is set to null
					if(constructorSelection == 1) //constructor 1
					{
						newCustomer = new Savings(Double.parseDouble(input.nextLine()), input.nextLine());
					}
					else if (constructorSelection == 2) //constructor 2
					{
						newCustomer = new Savings(Long.parseLong(input.nextLine()), Double.parseDouble(input.nextLine()), Double.parseDouble(input.nextLine()), input.nextLine());
					}
					else //anything else error
					{
						throw new Exception("error");
					}
					int methodSelection;
					do
					{
						methodSelection = Integer.parseInt(input.nextLine());
						switch(methodSelection)
						{
						case 0:
							break;
						case 1:
							outputFile.printf("%.2f\n",newCustomer.getAccountBalance());
							System.out.printf("%.2f\n",newCustomer.getAccountBalance());
							break; //get acc balanace with two decimal places
						case 2:
							outputFile.printf("%010d\n",newCustomer.getAccountNumber());
							System.out.printf("%010d\n",newCustomer.getAccountNumber());
							break;//get account num with 10 digits adding zeros if needed
						case 3:
							newCustomer.setAccountBalance(Double.parseDouble(input.nextLine()));
							break;//set account balance
						case 4:
							outputFile.println(newCustomer.getAnnualInterestRate());
							System.out.println(newCustomer.getAnnualInterestRate());
							break;//get annualinterestrate
						case 5:
							outputFile.println(newCustomer.getName());
							System.out.println(newCustomer.getName());
							break;//get name
						case 6:
							newCustomer.setAnnualInterestRate(input.nextDouble());
							break;//set annual interest rate
						case 7:
							newCustomer.makeDeposit(Double.parseDouble(input.nextLine()));
							break;//make deposit
						case 8:
							newCustomer.makeWithdrawal(Double.parseDouble(input.nextLine()));
							break;//make withdrawal
						default:
							throw new Exception("error");
						}
					} while(methodSelection != 0);
					break;
				}
				case "0": //if zero input then break the switch
					break;
				default:
					break;
				}
			}
		}
		catch(Exception ex)
		{
			outputFile.println(ex.getMessage()); //print the error message to file
			System.out.println(ex.getMessage()); //print the error message to console
		}
		outputFile.close(); //close printWriter
		System.exit(1); //terminate program
	}

}
