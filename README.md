# Restaurant Management System

## Table of Contents
- [Project Overview](#project-overview)
- [Features](#features)
- [File Structure](#file-structure)
- [Prerequisites](#prerequisites)
- [Build & Run](#build--run)
- [Usage](#usage)
  - [Admin Flow](#admin-flow)
  - [Customer Flow](#customer-flow)
- [Persistent Data Files](#persistent-data-files)
- [Limitations & Known Issues](#limitations--known-issues)
- [Security & Safety Notes](#security--safety-notes)
- [Planned Improvements](#planned-improvements)
- [Contributing](#contributing)
- [License](#license)
- [Author / Contact](#author--contact)

## Project Overview
Restaurant Management System is a lightweight console-based C program for simple restaurant operations: admin product registration and display, customer registration and ordering, and file-based persistence. This project is intended for learning basic file I/O, structs, and simple command-line interaction in C.

## Features
- Admin registration and login (3 attempts with temporary lockout)
- Product registration (name, price, category, quantity)
- Display product list with totals
- Customer registration and returning customer flow
- Place orders for registered products and compute totals
- Simple file-based persistence for admin, products, and customers

## File Structure
- `main.c` — primary C source file (contains the full program).
- `README.md` — this documentation.
- Data files created at runtime:
  - `restaurant.txt` — stores admin credentials (binary).
  - `product.txt` — stores product records (binary).
  - `rest.txt` — stores customer records (binary).

Important: Because data is stored in binary representations of structs, files are not human-readable and are system/ABI dependent.

## Prerequisites
- C compiler (GCC recommended)
- POSIX-compatible environment for `sleep()` (Linux, macOS). On Windows, `sleep()` usage may require adaptation.

## Build & Run
1. Compile:
   - GCC: `gcc -o restaurant main.c`
2. Run:
   - `./restaurant`

Example:
```
gcc -o restaurant main.c
./restaurant
```

## Usage

### Admin Flow
1. Choose "Admin" at the main prompt.
2. If no admin exists, register (the program writes to `restaurant.txt`).
3. Admin logs in with the registered uid/password (3 attempts). If 3 attempts fail, a 30-second cooldown occurs.
4. Admin options:
   - Register Product — add products to `product.txt`.
   - Display Products — show all registered products.

### Customer Flow
1. Choose "Customer" at the main prompt.
2. New Customer — register by providing name, phone, and address (saved to `rest.txt`).
3. Old Customer — login by phone number (phone number is used as identifier).
4. View product listings and place an order by product name and quantity.

## Persistent Data Files
- Data files are stored in the working directory and are written in binary using `fwrite`/`fread`.
- Files:
  - `restaurant.txt` — single admin struct
  - `product.txt` — sequence of product structs
  - `rest.txt` — sequence of customer structs


## Limitations & Known Issues
- Uses unsafe input functions like `gets()` which can cause buffer overflows.
- Phone numbers are stored as `int` — not suitable for longer numbers, country codes, or leading zeros.
- Binary struct storage is not portable across architectures or compiler versions.
- No concurrency handling; multiple simultaneous runs may corrupt files.
- The program does not update product quantities after an order (it displays order total but does not decrement product quantity).
- Display formatting has a minor bug in `printf` format for category (missing `%` before `-15`).

## Security & Safety Notes
- Replace `gets()` with `fgets()` to avoid buffer overflows.
- Consider storing credentials hashed (not in plain text or raw struct).
- Validate and sanitize all user input; check return values of `scanf()` and `fgets()`.
- Avoid storing sensitive data in plain binary files, and consider a simple plaintext CSV or JSON with proper escaping if you need portability.

## Suggested Improvements (short-term)
- Replace unsafe input (`gets`) with `fgets`.
- Store phone numbers as strings (`char[]`) or as `long long` to support longer numbers and formatting.
- Update product quantity on successful orders and persist the updated inventory.
- Add structured text-based storage (CSV/JSON) for portability and easy debugging.
- Add tests and a Makefile for build automation.
- Add input validation and clearer error handling.
- Improve admin authentication (password hashing) and allow multiple admins.

## Contributing
Contributions are welcome. If you want changes or features, please open an issue describing your request or submit a PR when the repository is created.

## License
Specify a license of your choice (e.g., MIT). If you want, I can add an MIT license file when creating the repo.

## Author / Contact
Created by: AayushGarg2028 (please confirm GitHub username for repository creation).