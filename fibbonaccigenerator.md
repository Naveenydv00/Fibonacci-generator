from functools import lru_cache
from typing import List


class FibonacciGenerator:
    """Efficient generator for Fibonacci numbers (F(1) = 1, F(2) = 1, ...)."""

    @staticmethod
    def _validate_positive_integer(n: int) -> None:
        """Ensure the input is a positive integer."""
        if not isinstance(n, int) or n <= 0:
            raise ValueError("Input must be a positive integer.")

    @staticmethod
    def fibonacci_iterative(n: int) -> int:
        """Return the nth Fibonacci number using an iterative approach."""
        FibonacciGenerator._validate_positive_integer(n)
        a, b = 1, 1
        for _ in range(2, n):
            a, b = b, a + b
        return a

    @staticmethod
    @lru_cache(maxsize=None)
    def fibonacci_recursive(n: int) -> int:
        """Return the nth Fibonacci number using memoized recursion."""
        FibonacciGenerator._validate_positive_integer(n)
        if n <= 2:
            return 1
        return (FibonacciGenerator.fibonacci_recursive(n - 1) +
                FibonacciGenerator.fibonacci_recursive(n - 2))

    @staticmethod
    def sequence_1_to_n(n: int) -> List[int]:
        """
        Generate a list of Fibonacci numbers from F(1) to F(n).

        Args:
            n (int): Number of terms to generate.

        Returns:
            List[int]: [F(1), F(2), ..., F(n)]
        """
        FibonacciGenerator._validate_positive_integer(n)
        if n == 1:
            return [1]
        seq = [1, 1]
        for _ in range(2, n - 1):
            seq.append(seq[-1] + seq[-2])
        return seq


def main() -> None:
    n, nth = 10, 8

    print(f"Fibonacci numbers from F(1) to F({n}): {FibonacciGenerator.sequence_1_to_n(n)}")
    print(f"F({nth}) (iterative): {FibonacciGenerator.fibonacci_iterative(nth)}")
    print(f"F({nth}) (recursive): {FibonacciGenerator.fibonacci_recursive(nth)}")


if __name__ == "__main__":
    main()
