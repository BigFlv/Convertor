# Convertor
//This program converts numbers from base one to base thirty-six .
//It is also useful for fractional numbers.

package converter;
import java.util.*;
public class Main {
    public static void forDecimalNumber(int targetRadix, double number) {
        for (int i = 0; i < 5; i++) {
            double decimalDigit = number * targetRadix;
            int finalNumber = (int) decimalDigit;
            number = decimalDigit - finalNumber;
            if (finalNumber > 9) {
                System.out.print(Character.forDigit(finalNumber, 36));
            } else {
                System.out.print(finalNumber);
            }
        }
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int sourceRadix = scanner.nextInt();
        String sourceNumber = scanner.next();
        int targetRadix = scanner.nextInt();

        //check if the number is decimal
        boolean stopped = true;
        for (int i = 0; i < sourceNumber.length(); i++) {
             char ch = sourceNumber.charAt(i);
            if (ch == '.') {
                stopped = false;
                break;
            }
        }

        // instructions if the number is an integer
        if (stopped && sourceRadix != 1 && targetRadix != 1) {
            System.out.println(Integer.toString(Integer.parseInt(sourceNumber, sourceRadix), targetRadix));
        } else if (stopped && sourceRadix == 1) {
            System.out.println(Integer.toString(sourceNumber.length(), targetRadix));
        } else if (stopped) {
            for (int j = 0; j < Integer.parseInt(sourceNumber); j++) {
                System.out.print(1);
            }
        }

        //instructions if the number is decimal
        String zero = "0.";
        if (!stopped) {
            String[] sNSplit = sourceNumber.split("\\.");
            System.out.print(Integer.toString(Integer.parseInt(sNSplit[0], sourceRadix), targetRadix) + ".");
            if (sourceRadix == 10) {
                String zecimal = zero.concat(sNSplit[1]);
                forDecimalNumber(targetRadix, Double.parseDouble(zecimal));
            } else {
                double finalNumberDecimal = 0.0;
                for (int k = 0; k < sNSplit[1].length(); k ++) {
                    char ch2 = sNSplit[1].charAt(k);
                    int ch2Digit = Character.getNumericValue(ch2);
                    finalNumberDecimal = ch2Digit / Math.pow(sourceRadix, k + 1) + finalNumberDecimal;
                }
                forDecimalNumber(targetRadix, finalNumberDecimal);
            }
        }

    }
}
