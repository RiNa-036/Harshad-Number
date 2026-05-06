Task-1
public class HarshadChecker {
    public static boolean isHarshad(int n) {
        if (n <= 0) return false;
        int original = n;
        int sum = 0;
        while (n > 0) {
            sum += n % 10;
            n /= 10;
        }
        return (original % sum == 0);
    }

    public static void main(String[] args) {
        int num = 18;
        System.out.println(isHarshad(num));
    }
}


Task-2
class Solution {
    public int sumOfTheDigitsOfHarshadNumber(int x) {
        int originalX = x;
        int sum = 0;
        while (x > 0) {
            sum += x % 10;
            x /= 10;
        }
        if (originalX % sum == 0) {
            return sum;
        }
        return -1;
    }
}


Task-3
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        final int N = 1_000_001;

        // Sieve of Eratosthenes
        boolean[] isPrime = new boolean[N];
        Arrays.fill(isPrime, true);
        isPrime[0] = isPrime[1] = false;
        for (int i = 2; (long) i * i < N; i++) {
            if (isPrime[i]) {
                for (int j = i * i; j < N; j += i) {
                    isPrime[j] = false;
                }
            }
        }

        // Mark generated numbers: d(r) = r + digitSum(r)
        boolean[] generated = new boolean[N];
        for (int r = 1; r < N; r++) {
            int s = r, x = r;
            while (x > 0) {
                s += x % 10;
                x /= 10;
            }
            if (s < N) generated[s] = true;
        }

        // Prefix count of Devlali primes
        int[] cnt = new int[N];
        for (int i = 1; i < N; i++) {
            cnt[i] = cnt[i - 1] + ((isPrime[i] && !generated[i]) ? 1 : 0);
        }

        // Fast input
        DataInputStream in = new DataInputStream(new BufferedInputStream(System.in));
        StringBuilder sb = new StringBuilder();

        int Q = nextInt(in);
        while (Q-- > 0) {
            int a = nextInt(in);
            int b = nextInt(in);
            int ans = cnt[b] - (a > 0 ? cnt[a - 1] : 0);
            sb.append(ans).append('\n');
        }

        // Fast output
        PrintWriter pw = new PrintWriter(new BufferedWriter(new OutputStreamWriter(System.out)));
        pw.print(sb);
        pw.flush();
    }

    // Fast integer reader
    private static int nextInt(DataInputStream in) throws IOException {
        int ret = 0, b;
        do {
            b = in.read();
        } while (b != -1 && (b < '0' || b > '9'));
        while (b >= '0' && b <= '9') {
            ret = ret * 10 + b - '0';
            b = in.read();
        }
        return ret;
    }
}
