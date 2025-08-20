# leetcode----1277
Count Square Submatrices with All ones
//code in java
public class Solution {
    public int countSquares(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        int count = 0;

        int[][] dp = new int[rows][cols];

        // Initialize first row and column
        for (int i = 0; i < rows; i++) {
            dp[i][0] = matrix[i][0];
            count += dp[i][0];
        }
        for (int j = 1; j < cols; j++) {
            dp[0][j] = matrix[0][j];
            count += dp[0][j];
        }

        // Fill the dp table
        for (int i = 1; i < rows; i++) {
            for (int j = 1; j < cols; j++) {
                if (matrix[i][j] == 1) {
                    dp[i][j] = Math.min(dp[i - 1][j], Math.min(dp[i][j - 1], dp[i - 1][j - 1])) + 1;
                    count += dp[i][j];
                }
            }
        }

        return count;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[][] matrix = {
            {0, 1, 1, 1},
            {1, 1, 1, 1},
            {0, 1, 1, 1}
        };
        int result = solution.countSquares(matrix);
        System.out.println("The number of square submatrices with all ones is: " + result); // Output: 15
    }
}
