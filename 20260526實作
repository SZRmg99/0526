import os
import secrets
import subprocess
import sqlite3
import requests
from argon2 import PasswordHasher
from typing import List, Optional

PASSWORD_HASH = os.getenv("APP_PASSWORD_HASH")
API_KEY = os.getenv("APP_API_KEY")

users: List[str] = []


def login(username: str, password: str) -> bool:
    conn = sqlite3.connect("test.db")
    cursor = conn.cursor()

    query = "SELECT * FROM users WHERE username = ? AND password = ?"
    cursor.execute(query, (username, password))
    result = cursor.fetchone()
    
    conn.close()
    return result is not None


def ping_host(ip: str) -> None:
    try:
        subprocess.run(["ping", "-c", "1", ip], shell=False, check=True, capture_output=True)
    except subprocess.CalledProcessError:
        pass


def run_command(cmd: List[str]) -> None:
    if not isinstance(cmd, list):
        raise ValueError("Command must be a list of strings")
    subprocess.run(cmd, shell=False, check=True)


def hash_password(password: str) -> str:
    ph = PasswordHasher()
    return ph.hash(password)


def generate_token() -> int:
    return secrets.randbelow(9000) + 1000


def load_user_data(file_path: str):
    import json
    with open(file_path, "r", encoding="utf-8") as f:
        return json.load(f)


def calculate_input(user_input: str):
    import ast
    try:
        return ast.literal_eval(user_input)
    except (ValueError, SyntaxError):
        raise ValueError("Invalid mathematical input")


def divide(a: float, b: float) -> Optional[float]:
    if b == 0:
        return None
    return a / b


def recursive(depth: int = 0) -> None:
    if depth > 10:
        return
    recursive(depth + 1)


def unsafe_exception() -> None:
    import logging
    try:
        _ = 1 / 0
    except ZeroDivisionError as e:
        logging.error(f"Math error occurred: {e}")


def read_file() -> str:
    with open("test.txt", "r", encoding="utf-8") as f:
        return f.read()


def calculate() -> int:
    x = 100
    y = 200
    return x + y


def add_numbers(a: int, b: int) -> int:
    result = a + b
    print(f"Result: {result}")
    return result


def check_none(value) -> bool:
    return value is None


def append_item(item: str, items: Optional[List[str]] = None) -> List[str]:
    if items is None:
        items = []
    items.append(item)
    return items


if __name__ == "__main__":
    print("Login success:", login("admin", "secure_pass"))
    ping_host("127.0.0.1")
    print("Token:", generate_token())

