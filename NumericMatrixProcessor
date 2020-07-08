package processor;

import java.math.RoundingMode;
import java.text.DecimalFormat;
import java.util.Scanner;


public class Main {

    private static Scanner scan;

    public static void main(String[] args) {
        scan = new Scanner(System.in);
        boolean running = true;

        while (running) {
            System.out.println("1. Add matrices");
            System.out.println("2. Multiply maxtrix to a constant");
            System.out.println("3. Multiply matrices");
            System.out.println("4. Transpose matrix");
            System.out.println("5. Calculate a determinant");
            System.out.println("6. Inverse Matrix");
            System.out.println("0. Exit");

            int mode = scan.nextInt();
            double[][] resultMatrix = new double[0][0];

            switch (mode) {
                case 1:
                    resultMatrix = addMatrices();
                    break;
                case 2:
                    double[][] matrix = createMatrix("first");
                    System.out.print("Enter a constant: ");
                    int mult = scan.nextInt();
                    resultMatrix = multMatrixByConstant(matrix, mult);
                    System.out.println("The multiplication result is:");
                    break;
                case 3:
                    resultMatrix = multMatrices();
                    break;
                case 4:
                    System.out.println("1. Main diagonal");
                    System.out.println("2. Side diagonal");
                    System.out.println("3. Vertical line");
                    System.out.println("4. Horizontal line");
                    System.out.print("Your choice: ");
                    int transposeType = scan.nextInt();
                    resultMatrix = transposeMatrix(createMatrix("first"), transposeType);
                    break;
                case 5:
                    double determinant = getDeterminant(createMatrix("first"));
                    System.out.println("The result is:");
                    System.out.println(determinant);
                    break;
                case 6:
                    resultMatrix = getInverse(createMatrix("first"));
                    break;
                default:
                    mode = 0;
                    running = false;
                    break;
            }
            if ((mode > 0 && mode < 5) || mode == 6) {
                printMatrix(resultMatrix);
            }

            System.out.println();
        }
    }

    private static double[][] getInverse(double[][] matrix) {
        double determinant = getDeterminant(matrix);
        if (determinant != 0) {
            double[][] adjoint = new double[matrix.length][matrix[0].length];
            for (int i = 0; i < matrix.length; i++) {
                for (int j = 0; j < matrix.length; j++) {
                    adjoint[i][j] = getCofactor(matrix, i, j);
                }
            }

            return multMatrixByConstant(transposeMatrix(adjoint, 1), 1 / getDeterminant(matrix));
        }
        return matrix;
    }

    private static double getDeterminant(double[][] matrix) {
        double determinant = 0;
        int rows = matrix.length;
        int cols = matrix[0].length;

        if (rows == cols) {
            if (rows == 1) {
                return matrix[0][0];
            } else if (rows == 2) {
                determinant += matrix[0][0] * matrix[1][1] - matrix[0][1] * matrix[1][0];
            } else {
                for (int i = 0; i < matrix.length; i++) {
                    determinant += matrix[0][i] * getCofactor(matrix, 0, i);
                }
            }
        }

        return determinant;
    }

    private static double getCofactor(double[][] matrix, int row, int col) {
        double co = Math.pow(-1, (row + 1) + (col + 1)) * getDeterminant(nextMatrix(matrix, row, col));
        co = co == -0 ? 0 : co;
        return co;
    }

    private static double[][] nextMatrix(double[][] matrix, int row, int col) {
        double[][] nextMatrix = new double[matrix.length - 1][matrix[0].length - 1];
        int count = 0;

        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[i].length; j++) {
                if (i != row && j != col) {
                    nextMatrix[count / nextMatrix.length][count % nextMatrix.length] = matrix[i][j];
                    count++;
                }
            }
        }

        return nextMatrix;
    }

    private static double[][] transposeMatrix(double[][] matrix, int transposeType) {
        double[][] resultMatrix = new double[matrix.length][matrix[0].length];

        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[i].length; j++) {
                double num = 0;
                switch (transposeType) {
                    case 1:
                        num = matrix[j][i];
                        break;
                    case 2:
                        num = matrix[Math.abs(j + 1 - matrix[i].length)][Math.abs(i + 1 - matrix.length)];
                        break;
                    case 3:
                        num = matrix[i][matrix[i].length - j - 1];
                        break;
                    case 4:
                        num = matrix[matrix.length - i - 1][j];
                        break;
                    default:
                        break;
                }
                resultMatrix[i][j] = num;
            }
        }

        return resultMatrix;
    }

    private static double[][] multMatrices() {
        double[][] firstMatrix = createMatrix("first");
        double[][] secondMatrix = createMatrix("second");
        double[][] resultMatrix = new double[0][0];

        if (firstMatrix[0].length == secondMatrix.length) {
            resultMatrix = new double[firstMatrix.length][secondMatrix[0].length];
            for (int i = 0; i < resultMatrix.length; i++) {
                for (int j = 0; j < resultMatrix[0].length; j++) {
                    double result = 0;
                    for (int k = 0; k < firstMatrix[i].length; k++) {
                        result += firstMatrix[i][k] * secondMatrix[k][j];
                    }
                    resultMatrix[i][j] = result;
                }
            }
        }
        System.out.println("The resulting matrix is: ");
        return resultMatrix;
    }

    public static double[][] multMatrixByConstant(double[][] matrix, double mult) {
        double[][] resultMatrix = new double[matrix.length][matrix[0].length];

        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                double num = matrix[i][j] * mult;
                resultMatrix[i][j] = num == -0 ? 0 : num;
            }
        }

        return resultMatrix;
    }

    public static double[][] addMatrices() {
        double[][] firstMatrix = createMatrix("first");
        double[][] secondMatrix = createMatrix("second");
        double[][] resultMatrix = new double[0][0];

        if (firstMatrix.length == secondMatrix.length && firstMatrix[0].length == secondMatrix[0].length) {
            resultMatrix = new double[firstMatrix.length][firstMatrix[0].length];
            for (int i = 0; i < firstMatrix.length; i++) {
                for (int j = 0; j < firstMatrix[0].length; j++) {
                    resultMatrix[i][j] = firstMatrix[i][j] + secondMatrix[i][j];
                }
            }
        }

        return resultMatrix;
    }

    private static double[][] createMatrix(String num) {
        System.out.print("Enter size of " + num + " matrix: ");
        int dy = scan.nextInt();
        int dx = scan.nextInt();
        System.out.println("Enter " + num + " matrix:");

        double[][] matrix = new double[dy][dx];

        for (int i = 0; i < dy; i++) {
            for (int j = 0; j < dx; j++) {
                matrix[i][j] = scan.nextDouble();
            }
        }

        return matrix;
    }

    private static void printMatrix(double[][] matrix) {
        DecimalFormat df = new DecimalFormat("#0.00");
        df.setRoundingMode(RoundingMode.FLOOR);
        for (double[] row : matrix) {
            StringBuilder str = new StringBuilder();
            for (double d : row) {
                if (d >= 0) {
                    str.append(" ");
                }
                str.append(df.format(d)).append(" ");
            }
            System.out.println(str.toString().replaceAll("\\s++$", ""));
        }
        System.out.println();
    }
}
