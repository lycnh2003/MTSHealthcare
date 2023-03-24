# MTSHealthcare

package MTSHealthcare;
import java.util.Scanner;
public class MTSHealthcare {

	public static void main(String[] args) {
		 Scanner sc = new Scanner(System.in);
	        double basicCost = 436.00;
	        int age, numDependants, numFreeDependants, dependantAge;
	        String name, dependantname;
	        double inpatientSemiPrivateCost = 200.00;
	        double inpatientPrivateCost = 300.00;
	        double vat = 0.21;
	        boolean isQuoting = true;
	        double totalCost, dependantCost, vatAmount, totalCostIncludingVat;

	        System.out.println("Enter the name of the main policy holder:");
	        name = sc.nextLine();

	        while (isQuoting) {
	            System.out.println("Enter the age of the main policy holder:");
	            age = sc.nextInt();
	            totalCost = basicCost;

	            if (age > 50) {
	                totalCost += 90.00;
	            }

	            System.out.println("How many dependants would you like to add?");
	            numDependants = sc.nextInt();
	            numFreeDependants = Math.min(numDependants, 6);
	            dependantCost = 0.0;

	            for (int i = 1; i <= numFreeDependants; i++) {
	                System.out.println("Enter the names of dependant " + i + ":");
	                dependantname = sc.next();
	                System.out.println("Enter the age of dependant " + i + ":");
	                dependantAge = sc.nextInt();

	                if (dependantAge < 18) {
	                    dependantCost += getDependantCost(i);
	                } else {
	                    System.out.println("Dependant " + i + " is not eligible for coverage.");
	                }
	            }

	            totalCost += dependantCost;

	            System.out.println("Would you like inpatient coverage? (Y/N)");
	            String inpatientResponse = sc.next();

	            if (inpatientResponse.equalsIgnoreCase("Y")) {
	                System.out.println("Would you like a private room? (Y/N)");
	                String roomResponse = sc.next();

	                if (roomResponse.equalsIgnoreCase("Y")) {
	                    totalCost += inpatientPrivateCost;
	                } else {
	                    totalCost += inpatientSemiPrivateCost;
	                }
	            }

	            vatAmount = totalCost * vat;
	            totalCostIncludingVat = totalCost + vatAmount;

	            System.out.println("Your quote for the policy is: ");
	            System.out.println("Total cost without VAT: €" + String.format("%.2f", totalCost));
	            System.out.println("VAT: €" + String.format("%.2f", vatAmount));
	            System.out.println("Total cost with VAT: €" + String.format("%.2f", totalCostIncludingVat));
	            System.out.println("Do you want to get another quote? (Y/N)");
	            String quoteResponse = sc.next();

	            if (quoteResponse.equalsIgnoreCase("N")) {
	                isQuoting = false;
	            }
	        }

	        System.out.println("Thank you for using our Health Insurance Calculator!");
	    }

	    private static double getDependantCost(int dependantNumber) {
	        switch (dependantNumber) {
	            case 1:
	                return 270.00;
	            case 2:
	                return 160.00;
	            case 3:
	                return 100.00;
	            case 4:
	                return 50.00;
	            default:
	                return 0.0;
	        }
	    }
	}
