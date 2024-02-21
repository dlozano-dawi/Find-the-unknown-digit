# Find-the-unknown-digit
Solution for the Kata Kyu 4 Find The Unknown Digit
~~~
public class Runes {

	public static int solveExpression( final String expression ) {
        boolean state = false;
        boolean state2 = false;
        boolean opB = false;
        String first = "";
        String second = "";
        String solve = "";
        String op = "";

        for (int i = 0; i < expression.length(); i++) {
            if (opB && (expression.charAt(i) == '*' || expression.charAt(i) == '+' || expression.charAt(i) == '-' )) {
                op += expression.charAt(i);
                state = true;
                opB = false;
            } else if (!state) {
                    opB = true;
                first += expression.charAt(i);
            } else if (expression.charAt(i) == '=') {
                state2 = true;
            } else if (!state2 && state) {
                second += expression.charAt(i);
            } else if (state2) {
                solve += expression.charAt(i);
            }
        }

        for (int i = 0; i < 10; i++) {
            if ( first.contains(i + "") || second.contains(i + "") || solve.contains(i + "")) {
                continue;
            }
            if (i == 0 && ((first.charAt(0) == '?' && first.length() > 1) || (second.charAt(0) == '?' && second.length() > 1)) && !op.equals("*")) {
                continue;
            }
            StringBuilder firstSb = new StringBuilder(first);
            StringBuilder secondSb = new StringBuilder(second);
            StringBuilder solveSb = new StringBuilder(solve);
            while (firstSb.indexOf("?") != -1 || secondSb.indexOf("?") != -1 || solveSb.indexOf("?") != -1) {
                    
                int indexSbF = firstSb.indexOf("?");
                int indexSbS = secondSb.indexOf("?");
                int indexSbSS = solveSb.indexOf("?");
                if (indexSbF != -1) {
                    String intF = Integer.toString(i);
                    firstSb.setCharAt(indexSbF, intF.charAt(0));
                }
                if (indexSbS != -1) {
                    String intS = Integer.toString(i);
                    secondSb.setCharAt(indexSbS, intS.charAt(0));
                }
                if (indexSbSS != -1) {
                    String intSS = Integer.toString(i);
                    solveSb.setCharAt(indexSbSS, intSS.charAt(0));
                }
            }
            if (op.equals("*")) {
                int solveM = Integer.parseInt(firstSb.toString()) * Integer.parseInt(secondSb.toString()); 
                if (Integer.toString(solveM).length() == solve.length() && solveM == Integer.parseInt(solveSb.toString()) ) {
                    return i;
                }
            } else if (op.equals("-")) {
                int solveM = Integer.parseInt(firstSb.toString()) - Integer.parseInt(secondSb.toString()); 
                if (Integer.toString(solveM).length() == solve.length() && solveM == Integer.parseInt(solveSb.toString()) ) {
                    return i;
                }
            } else if (op.equals("+")) {
                int solveM = Integer.parseInt(firstSb.toString()) + Integer.parseInt(secondSb.toString()); 
                if (Integer.toString(solveM).length() == solve.length() && solveM == Integer.parseInt(solveSb.toString()) ) {
                    return i;
                }
            }
        }
		return -1;
	}
}
~~~
