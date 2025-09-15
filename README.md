# ================================
# Project: Timeless Code Space
# Description:
# A powerful space for crafting and refining code
# Dedicated to experimenting with ideas, building resilient solutions,
# and shaping projects that stand the test of time.
# ================================

# ---------- main.py ----------
"""
Main entry point of the project.
"""

from core import ideas, resilience


def run():
    print("🚀 Welcome to the Timeless Code Space")
    print("🔧 Crafting resilient solutions, refining ideas, and experimenting with code.\n")

    # Example experiments
    print("💡 Idea Prototype:", ideas.reverse_string("timeless"))
    print("🛡️ Resilience Check (safe divide):", resilience.safe_divide(10, 0))
    print("🛡️ Resilience Check (retry demo):", resilience.retry(lambda: 1 / 0, retries=3))


if __name__ == "__main__":
    run()


# ---------- core/ideas.py ----------
"""
Module for coding ideas, prototypes, and creative experiments.
"""

def reverse_string(s: str) -> str:
    """Return the reversed version of a string."""
    return s[::-1]

def factorial(n: int) -> int:
    """Compute factorial of n recursively."""
    if n <= 1:
        return 1
    return n * factorial(n - 1)


# ---------- core/resilience.py ----------
"""
Module for resilient and reliable solutions.
Includes error handling, safe utilities, and retry mechanisms.
"""

import time

def safe_divide(a: float, b: float) -> float:
    """Safely divide two numbers, returning None if division by zero."""
    try:
        return a / b
    except ZeroDivisionError:
        return None

def retry(func, retries=3, delay=1):
    """
    Retry a function multiple times before failing.
    func: callable with no arguments
    retries: number of attempts
    delay: seconds between retries
    """
    for attempt in range(1, retries + 1):
        try:
            return func()
        except Exception as e:
            print(f"Attempt {attempt} failed: {e}")
            if attempt < retries:
                time.sleep(delay)
    return None


# ---------- tests/test_resilience.py ----------
"""
Basic tests for resilience.py
Run with: pytest
"""

from core import resilience

def test_safe_divide():
    assert resilience.safe_divide(10, 2) == 5
    assert resilience.safe_divide(10, 0) is None

def test_retry_success():
    f = lambda: 42
    assert resilience.retry(f, retries=2) == 42

def test_retry_failure():
    f = lambda: 1 / 0
    assert resilience.retry(f, retries=2) is None
