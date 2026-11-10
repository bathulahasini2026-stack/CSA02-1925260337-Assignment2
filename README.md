# CSA02-1925260337-Assignment2
This repository contains C Programming Assignment 2 (CO2), covering operators, decision-making statements, looping constructs and algorithm optimization. It includes program solutions, pseudocode, execution outputs, test cases and complexity analysis for Questions 1–7.

COURSE CODE:CSA02
NAME :B.HASINI
REG.NO.:1925260337
C-PROGRAMMING
COURSE FACULTY : SURYA SHANMUGAM
BRANCH : Btech AI ML

CO 2 ASSIGNMENT 2
ABOUT: Performance Optimization and Experimental Analysis of Prime Number Checking Using Mathematical Logic in C Programming




TABLE OF CONTENTS
QUESTION 1(pharmacy billing system)
QUESTION 2(Passenger Concession Verification System)
QUESTION 2(alternative code for passenger concession verification system)
QUESTION 3(Alternative code for Bitwise Device Controller)
QUESTION 3(Bitwise Device Controller)
QUESTION 4(Student Grade and Scholarship Eligibility Checker)
QUESTION 5(Alternative Code using FOR LOOP for Trial Division Prime Checker)
QUESTION 5(Alternative code using DO WHILE LOOP for the Trail Division Prime Checker)
QUESTION 5(Alternative code using Sieve of Eratosthenes Prime Generator for the Trail Division Prime Checker)
QUESTION 5(Alternative method using WHILE LOOP for the Trial Division Prime Checker)
QUESTION 5(Trial Division Prime Checker)
QUESTION 6(Alternative code for the Loan Repayment Schedule)
QUESTION 6(Loan Repayment Schedule)
QUESTION 7(Alternative code for Improved Trial Division Prime Checker)
QUESTION 7(Improved Trial Division Prime Checker)
QUESTION4(Alternative code for Student Grade and Scholarship Eligibility Checker)

TODO 1 – Switch ON a Device(Q-3)
TODO 2 – Grade Classification Using Switch Statement(Q-4)
TODO 2 – Switch OFF a Device(Q-3)
TODO 3 – Toggle a Device(Q-3)
TODO 4 – Check Whether a Device Is ON(Q-3)
TODO-3 PRIME NUMBER CHECKING(Q-5)

QUESTION 1(pharmacy billing system)
#include <stdio.h>
#include <stdbool.h>

int main(void)
{
    double price, quantity;
    double gross_amount, discount, discounted_amount, gst, total_amount;
    int senior_input;
    bool senior_status;

    /* READ inputs */
    printf("Enter price: ");
    scanf("%lf", &price);

    printf("Enter quantity: ");
    scanf("%lf", &quantity);

    printf("Senior citizen? (1 = Yes, 0 = No): ");
    scanf("%d", &senior_input);
    senior_status = (senior_input == 1);

    /* Calculations */
    gross_amount = price * quantity;

    if (senior_status) {
        discount = gross_amount * 0.10;
    } else {
        discount = 0;
    }

    discounted_amount = gross_amount - discount;

    gst = discounted_amount * 0.05;

    total_amount = discounted_amount + gst;

    if (total_amount > 1000) {
        total_amount = total_amount - 50;
    }

    /* DISPLAY outputs */
    printf("\nGross Amount : %.2f\n", gross_amount);
    printf("Discount     : %.2f\n", discount);
    printf("GST          : %.2f\n", gst);
    printf("Total Amount : %.2f\n", total_amount);

    return 0;
}
COMMANDS USED TO RUN

Compile with: gcc bill.c -o bill, then run ./bill.
//OUTPUTS
 Sample run (price = 600, quantity = 2, senior = 1):

Enter price: 600
Enter quantity: 2
Senior citizen? (1 = Yes, 0 = No): 1

Gross Amount : 1200.00
Discount     : 120.00
GST          : 54.00
Total Amount : 1084.00

SCREENSHOT OF THE OUTPUT:<img width="357" height="241" alt="image" src="https://github.com/user-attachments/assets/5993c818-4dc3-4235-a95c-ad209937857e" />

QUESTION 2(Passenger Concession Verification System)
#include <stdio.h>
#include <stdbool.h>

#define TOTAL_PASSENGERS 1000

/* Simulates checking the disability card.
   Here the operator enters the result; replace this with real
   verification logic (database lookup, card scan, etc.) if needed. */
bool verify_disability_card(void)
{
    int result;

    printf("  Verify disability card (1 = Valid, 0 = Not valid): ");
    scanf("%d", &result);

    return (result == 1);
}

int main(void)
{
    int verification_calls = 0;
    int senior_input, class_input;
    bool senior_status, eligible_class;
    bool disability_status, concession;

    for (int passenger = 1; passenger <= TOTAL_PASSENGERS; passenger++) {

        printf("\nPassenger %d\n", passenger);

        /* READ inputs */
        printf("  Senior citizen? (1 = Yes, 0 = No): ");
        scanf("%d", &senior_input);
        senior_status = (senior_input == 1);

        printf("  Eligible class? (1 = Yes, 0 = No): ");
        scanf("%d", &class_input);
        eligible_class = (class_input == 1);

        if (senior_status && eligible_class) {
            concession = true;
        } else {
            verification_calls = verification_calls + 1;

            disability_status = verify_disability_card();

            if (disability_status == true) {
                concession = true;
            } else {
                concession = false;
            }
        }

        if (concession == true) {
            printf("  Concession Approved\n");
        } else {
            printf("  Concession Not Approved\n");
        }
    }

    printf("\nTotal verification calls: %d\n", verification_calls);

    return 0;
}
COMMANDS USED TO RUN
gcc concession.c -o concession

OUTPUTS OF THE CODE
Sample run (with TOTAL_PASSENGERS set to 3)
Passenger 1
  Senior citizen? (1 = Yes, 0 = No): 1
  Eligible class? (1 = Yes, 0 = No): 1
  Concession Approved

Passenger 2
  Senior citizen? (1 = Yes, 0 = No): 0
  Eligible class? (1 = Yes, 0 = No): 1
  Verify disability card (1 = Valid, 0 = Not valid): 1
  Concession Approved

Passenger 3
  Senior citizen? (1 = Yes, 0 = No): 0
  Eligible class? (1 = Yes, 0 = No): 0
  Verify disability card (1 = Valid, 0 = Not valid): 0
  Concession Not Approved

Total verification calls: 2
SREENSHOT OF THE OUTPUT:<img width="572" height="411" alt="image" src="https://github.com/user-attachments/assets/5d41e4f8-0417-4304-8f9b-708a27d7c33b" />

QUESTION 2(alternative code for passenger concession verification system)
#include <stdio.h>
#include <stdbool.h>

int main(void)
{
    int senior_input, class_input, card_input;
    bool senior_status, eligible_class;
    bool concession = false;        /* starts FALSE so it is never uninitialized */
    bool disability_card_valid = false;

    /* READ inputs */
    printf("Senior citizen? (1 = Yes, 0 = No): ");
    scanf("%d", &senior_input);
    senior_status = (senior_input == 1);

    printf("Eligible class? (1 = Yes, 0 = No): ");
    scanf("%d", &class_input);
    eligible_class = (class_input == 1);

    if (senior_status == true) {

        if (eligible_class == true) {
            concession = true;
        } else {
            /* VERIFY disability_card */
            printf("Verify disability card (1 = Valid, 0 = Not valid): ");
            scanf("%d", &card_input);
            disability_card_valid = (card_input == 1);
        }

    } else {
        /* VERIFY disability_card */
        printf("Verify disability card (1 = Valid, 0 = Not valid): ");
        scanf("%d", &card_input);
        disability_card_valid = (card_input == 1);
    }

    if (concession == true || disability_card_valid == true) {
        printf("Concession Approved\n");
    } else {
        printf("Concession Not Approved\n");
    }

    return 0;
}

COMMANDS USED TO COMPILE
gcc concession_single.c -o concession_single
./concession_single

OUTPUTS OF THE CODE:
Sample runs

Senior citizen? (1 = Yes, 0 = No): 1
Eligible class? (1 = Yes, 0 = No): 1
Concession Approved
Senior citizen? (1 = Yes, 0 = No): 0
Eligible class? (1 = Yes, 0 = No): 1
Verify disability card (1 = Valid, 0 = Not valid): 0
Concession Not Approved

SCREENSHOT OF THE OUTPUT:<img width="476" height="178" alt="image" src="https://github.com/user-attachments/assets/f142a11c-d37f-413f-a127-2035cec93666" />

QUESTION 3(Bitwise Device Controller)
#include <stdio.h>

#define SIZE 8

int main(void)
{
    int state[SIZE];
    int count = 0;

    /* Initialize all elements to 0 */
    for (int i = 0; i < SIZE; i++) {
        state[i] = 0;
    }

    state[0] = 1;              /* switch ON device 0 */
    state[2] = 1;              /* switch ON device 2 */

    state[1] = 1 - state[1];   /* toggle device 1 */

    state[0] = 0;              /* switch OFF device 0 */

    /* Display the array */
    printf("State array: ");
    for (int i = 0; i < SIZE; i++) {
        printf("%d ", state[i]);
    }
    printf("\n");

    /* Count devices that are ON */
    for (int i = 0; i < SIZE; i++) {
        if (state[i] == 1) {
            count = count + 1;
        }
    }

    printf("Number of devices ON: %d\n", count);

    return 0;
}
COMMANDS USED 
gcc register.c -o register and run ./register.

OUTPUTS
Register after switching ON Light and AC : 00000101
Register after toggling Fan, Light OFF   : 00000110
AC Status   : ON
PUMP Status : OFF
Number of devices ON: 2

SCREENSHOT OF OUTPUT:<img width="505" height="227" alt="image" src="https://github.com/user-attachments/assets/27467ea8-c629-4282-8004-972597721c5c" />

QUESTION 3(Alternative code for Bitwise Device Controller)
#include <stdio.h>

#define SIZE 8

int main(void)
{
    int state[SIZE];
    int count = 0;

    /* Initialize all elements to 0 */
    for (int i = 0; i < SIZE; i++) {
        state[i] = 0;
    }

    state[0] = 1;              /* switch ON device 0 */
    state[2] = 1;              /* switch ON device 2 */

    state[1] = 1 - state[1];   /* toggle device 1 */

    state[0] = 0;              /* switch OFF device 0 */

    /* Display the array */
    printf("State array: ");
    for (int i = 0; i < SIZE; i++) {
        printf("%d ", state[i]);
    }
    printf("\n");

    /* Count devices that are ON */
    for (int i = 0; i < SIZE; i++) {
        if (state[i] == 1) {
            count = count + 1;
        }
    }

    printf("Number of devices ON: %d\n", count);

    return 0;
}

COMMANDS USED
Compile with gcc state_array.c -o state_array and run ./state_array.

OUTPUTS
State array: 0 1 1 0 0 0 0 0 
Number of devices ON: 2
SCRRENSHOTS OF THE OUTPUT:<img width="366" height="146" alt="image" src="https://github.com/user-attachments/assets/3eed7592-2e5d-4f9c-935b-6d5dfde77620" />

QUESTION 4(Student Grade and Scholarship Eligibillity Checker)
#include <stdio.h>
#include <stdbool.h>

/* Assumptions: the pseudocode does not give these values, so change them as needed */
#define INCOME_LIMIT 500000.0    /* maximum family income allowed (per year) */

/* Grades eligible for the scholarship: S, A and B */
bool is_grade_eligible(char grade)
{
    return (grade == 'S' || grade == 'A' || grade == 'B');
}

int main(void)
{
    double marks, family_income;
    int grade_group;
    char grade;

    /* READ marks */
    printf("Enter marks (0 to 100): ");
    scanf("%lf", &marks);

    if (marks < 0 || marks > 100) {

        printf("Invalid Marks\n");
        grade = '?';

    } else {

        grade_group = (int)(marks / 10);   /* INTEGER PART OF (marks / 10) */

        switch (grade_group) {

            case 10:
            case 9:
                grade = 'S';
                break;

            case 8:
                grade = 'A';
                break;

            case 7:
                grade = 'B';
                break;

            case 6:
                grade = 'C';
                break;

            case 5:
                grade = 'D';
                break;

            default:
                grade = 'F';
        }
    }

    /* DISPLAY grade */
    printf("Grade: %c\n", grade);

    /* READ family_income */
    printf("Enter family income: ");
    scanf("%lf", &family_income);

    /* CHECK scholarship eligibility */
    if (is_grade_eligible(grade) && family_income <= INCOME_LIMIT) {
        printf("Scholarship Eligible\n");
    } else {
        printf("Scholarship Not Eligible\n");
    }

    return 0;
}

COMMANDS USED
gcc grade_scholarship.c -o grade_scholarship
./grade_scholarship

OUTPUTS
Enter marks (0 to 100): 85
Grade: A
Enter family income: 300000
Scholarship Eligible
SCREENSHOT OF THE OUTPUT:<img width="365" height="146" alt="image" src="https://github.com/user-attachments/assets/bf9bde51-bcb4-4efd-8bae-b634e4678960" />

QUESTION 4(Alternative Code For Student Grade and Scholarship Eligibillity Checker)
 #include <stdio.h>

int main(void)
{
    /* Lookup table: index = marks / 10 */
    char grades[] = {
        'F', 'F', 'F', 'F', 'F',
        'D', 'C', 'B', 'A', 'S', 'S'
    };

    double marks;
    int grade_group;
    char grade;

    /* READ marks */
    printf("Enter marks (0 to 100): ");
    scanf("%lf", &marks);

    if (marks < 0 || marks > 100) {

        printf("Invalid Marks\n");

    } else {

        grade_group = (int)(marks / 10);   /* INTEGER PART OF (marks / 10) */

        grade = grades[grade_group];

        printf("Grade: %c\n", grade);
    }

    return 0;
}

COMMANDS USED
gcc grade_lookup.c -o grade_lookup
./grade_lookup

OUTPUTS
Enter marks (0 to 100): 85
Grade: A
SCREENSHOT OF THE OUTPUT:<img width="356" height="147" alt="image" src="https://github.com/user-attachments/assets/3c834b81-6661-4e0c-8f09-7fe38fdc0c1b" />

QUESTION 5(Trial Division Prime Checker)
#include <stdio.h>

int main(void)
{
    int n;
    int checks = 0;

    /* READ n */
    printf("Enter a number: ");
    scanf("%d", &n);

    if (n < 2) {
        printf("Not Prime\n");
        return 0;                      /* STOP */
    }

    for (int i = 2; i <= n - 1; i++) {

        checks = checks + 1;

        if (n % i == 0) {
            printf("Not Prime\n");
            printf("Checks: %d\n", checks);
            return 0;                  /* STOP */
        }
    }

    printf("Prime\n");
    printf("Checks: %d\n", checks);

    return 0;
}

COMMANDS USED:
gcc prime_check.c -o prime_check
./prime_check
OUTPUTS:
Enter a number: 17
Prime
Checks: 15
SCREENSHOT OF THE OUTPUT:<img width="342" height="143" alt="image" src="https://github.com/user-attachments/assets/92827d4e-eb5b-412b-bb0e-a9634c5cfede" />

QUESTION 5(Alternative Code Usining FOR LOOP For Trail Division Prime Checker)
#include <stdio.h>

int main(void)
{
    long long n;
    int checks = 0;

    /* READ n */
    printf("Enter a number: ");
    scanf("%lld", &n);

    if (n < 2) {
        printf("Not Prime\n");
        return 0;                      /* STOP */
    }

    for (long long i = 2; i * i <= n; i++) {

        checks = checks + 1;

        if (n % i == 0) {
            printf("Not Prime\n");
            printf("Checks: %d\n", checks);
            return 0;                  /* STOP */
        }
    }

    printf("Prime\n");
    printf("Checks: %d\n", checks);

    return 0;
}

COMMANDS USED:
gcc prime_sqrt.c -o prime_sqrt
./prime_sqrt
OUTPUTS:
Enter a number: 17
Prime
Checks: 3
SCREENSHOT OF THE OUTPUTS:<img width="374" height="162" alt="image" src="https://github.com/user-attachments/assets/444ed059-440a-4dfa-b406-959c6f9c04ef" />


QUESTION 5(Alternative Code Using DO WHILE LOOP For Trail Division Prime Checker)
#include <stdio.h>

int main(void)
{
    long long n;
    long long i;
    int checks = 0;

    /* READ n */
    printf("Enter a number: ");
    scanf("%lld", &n);

    if (n < 2) {
        printf("Not Prime\n");
        return 0;                      /* STOP */
    }

    i = 2;

    do {

        if (i * i > n) {
            break;                     /* EXIT LOOP */
        }

        checks = checks + 1;

        if (n % i == 0) {
            printf("Not Prime\n");
            printf("Checks: %d\n", checks);
            return 0;                  /* STOP */
        }

        i = i + 1;

    } while (1);                       /* WHILE TRUE */

    printf("Prime\n");
    printf("Checks: %d\n", checks);

    return 0;
}

COMMANDS USED:
gcc prime_dowhile.c -o prime_dowhile
./prime_dowhile
OUTPUTS:
Enter a number: 17
Prime
Checks: 3
SCREENSHOT OF THE OUTPUT:<img width="410" height="238" alt="image" src="https://github.com/user-attachments/assets/36eddd81-19ea-4cf5-b3e3-8dbb25a1d0c2" />

QUESTION 5(Alternative method using WHILE LOOP for the trail divison prime checker)
#include <stdio.h>

int main(void)
{
    long long n;
    long long i;
    int checks = 0;

    /* READ n */
    printf("Enter a number: ");
    scanf("%lld", &n);

    if (n < 2) {
        printf("Not Prime\n");
        return 0;                      /* STOP */
    }

    i = 2;

    while (i * i <= n) {

        checks = checks + 1;

        if (n % i == 0) {
            printf("Not Prime\n");
            printf("Checks: %d\n", checks);
            return 0;                  /* STOP */
        }

        i = i + 1;
    }

    printf("Prime\n");
    printf("Checks: %d\n", checks);

    return 0;
}

COMMANDS USED:
gcc prime_while.c -o prime_while
./prime_while
OUTPUTS:
Enter a number: 25
Not Prime
Checks: 4
SCREENSHOT OF THE OUTPUT:<img width="430" height="238" alt="image" src="https://github.com/user-attachments/assets/cac88291-c26d-4928-9727-e487296feaa1" />

QUESTION 5(alternative code using sieve eratosthenes Prime Generator for the Trail Divisom Prime Checker)
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

int main(void)
{
    int N;

    /* READ N */
    printf("Enter N: ");
    if (scanf("%d", &N) != 1 || N < 0) {
        printf("Invalid input\n");
        return 1;
    }

    /* CREATE an array PRIME[0...N] */
    bool *prime = (bool *)malloc((N + 1) * sizeof(bool));
    if (prime == NULL) {
        printf("Memory allocation failed\n");
        return 1;
    }

    /* MARK all entries as TRUE */
    for (int i = 0; i <= N; i++) {
        prime[i] = true;
    }

    /* MARK PRIME[0] and PRIME[1] as FALSE */
    prime[0] = false;
    if (N >= 1) {
        prime[1] = false;
    }

    /* Sieve: p goes from 2 up to the square root of N */
    for (long long p = 2; p * p <= N; p++) {

        if (prime[p] == true) {

            for (long long multiple = p * p; multiple <= N; multiple += p) {
                prime[multiple] = false;
            }
        }
    }

    /* DISPLAY all primes */
    printf("Prime numbers up to %d:\n", N);
    for (int number = 2; number <= N; number++) {
        if (prime[number] == true) {
            printf("%d ", number);
        }
    }
    printf("\n");

    free(prime);
    return 0;
}

COMMANDS USED:
gcc sieve.c -o sieve
./sieve
OUTPUTS:
Enter N: 50
Prime numbers up to 50:
2 3 5 7 11 13 17 19 23 29 31 37 41 43 47
SCREENSGHOT OF THE OUTPUT:<img width="392" height="185" alt="image" src="https://github.com/user-attachments/assets/8ddbd565-4647-4ce7-9148-b12901d64d84" />

QUESTION 6(Loan repayment schedule)
#include <stdio.h>

#define MAX_MONTHS 360
#define TOLERANCE  0.01

int main(void)
{
    double principal, monthly_interest_rate, monthly_payment;
    double rate, balance, total_interest, first_interest;
    double interest, payment;
    int month;

    /* READ inputs */
    printf("Enter principal: ");
    scanf("%lf", &principal);

    printf("Enter monthly interest rate (in %%): ");
    scanf("%lf", &monthly_interest_rate);

    printf("Enter monthly payment: ");
    scanf("%lf", &monthly_payment);

    /* Validate inputs */
    if (principal <= 0 || monthly_interest_rate < 0 || monthly_payment <= 0) {
        printf("Invalid Input\n");
        return 0;                          /* STOP */
    }

    rate = monthly_interest_rate / 100;

    balance = principal;
    total_interest = 0;
    month = 0;

    /* Check that the payment covers at least the first month's interest */
    first_interest = balance * rate;

    if (monthly_payment <= first_interest) {
        printf("Repayment is insufficient\n");
        return 0;                          /* STOP */
    }

    printf("\n%-6s %-12s %-12s %-12s\n", "Month", "Interest", "Payment", "Balance");

    while (balance > TOLERANCE && month < MAX_MONTHS) {

        interest = balance * rate;

        balance = balance + interest;

        total_interest = total_interest + interest;

        if (balance < monthly_payment) {
            payment = balance;
        } else {
            payment = monthly_payment;
        }

        balance = balance - payment;

        month = month + 1;

        printf("%-6d %-12.2f %-12.2f %-12.2f\n", month, interest, payment, balance);
    }

    printf("\n");

    if (balance <= TOLERANCE) {
        printf("Loan Fully Repaid\n");
    } else {
        printf("Maximum repayment period reached\n");
    }

    printf("Total interest paid: %.2f\n", total_interest);
    printf("Months taken       : %d\n", month);

    return 0;
}

COMMANDS USED:
gcc loan.c -o loan
./loan
OUTPUTS:
Enter principal: 10000
Enter monthly interest rate (in %): 1
Enter monthly payment: 2000

Month  Interest     Payment      Balance
1      100.00       2000.00      8100.00
2      81.00        2000.00      6181.00
3      61.81        2000.00      4242.81
4      42.43        2000.00      2285.24
5      22.85        2000.00      308.09
6      3.08         311.17       0.00

Loan Fully Repaid
Total interest paid: 311.17
Months taken       : 6
SCREENSHOTS OF THE OUTPUT:<img width="414" height="368" alt="image" src="https://github.com/user-attachments/assets/cd4cb99d-e12c-4c49-a89c-95a2220f29be" />

QUESTION 6{alternative code for the Loan repayment schedule)
#include <stdio.h>
#include <math.h>

int main(void)
{
    double principal, monthly_rate, monthly_payment;
    double value, months;
    int required_months;

    /* READ inputs */
    printf("Enter principal: ");
    scanf("%lf", &principal);

    printf("Enter monthly rate (as a fraction, e.g. 0.01 for 1%%): ");
    scanf("%lf", &monthly_rate);

    printf("Enter monthly payment: ");
    scanf("%lf", &monthly_payment);

    if (monthly_payment <= principal * monthly_rate) {
        printf("Loan cannot be repaid with this payment\n");
        return 0;                          /* STOP */
    }

    value = 1 - (monthly_rate * principal / monthly_payment);

    if (value <= 0) {
        printf("Invalid calculation\n");
        return 0;                          /* STOP */
    }

    months = -log(value) / log(1 + monthly_rate);

    required_months = (int)ceil(months);   /* ROUND UP to next integer */

    printf("Required months: %d\n", required_months);

    return 0;
}

COMMANDS USED:
gcc loan_months.c -o loan_months -lm
./loan_months
OUTPUTS:
Enter principal: 10000
Enter monthly rate (as a fraction, e.g. 0.01 for 1%): 0.02
Enter monthly payment: 150
Loan cannot be repaid with this payment
SCREENSHOTS OF THE OUTPUT:<img width="521" height="186" alt="image" src="https://github.com/user-attachments/assets/ba5ff532-c967-4574-b5b7-e74d5aaf5db5" />

QUESTION 7(Improved Trail Division Prime Checker)
#include <stdio.h>

int main(void)
{
    long long n;
    long long divisor;
    int checks = 0;

    /* READ n */
    printf("Enter a number: ");
    scanf("%lld", &n);

    if (n < 2) {
        printf("Not Prime\n");
        return 0;                      /* STOP */
    }

    if (n == 2) {
        printf("Prime\n");             /* checks is not displayed here */
        return 0;                      /* STOP */
    }

    checks = checks + 1;               /* the even-number check */

    if (n % 2 == 0) {
        printf("Not Prime\n");
        printf("Checks: %d\n", checks);
        return 0;                      /* STOP */
    }

    divisor = 3;

    while (divisor <= n / divisor) {

        checks = checks + 1;

        if (n % divisor == 0) {
            printf("Not Prime\n");
            printf("Checks: %d\n", checks);
            return 0;                  /* STOP */
        }

        divisor = divisor + 2;         /* only odd divisors */
    }

    printf("Prime\n");
    printf("Checks: %d\n", checks);

    return 0;
}

COMMANDS USED:
gcc prime_odd.c -o prime_odd
./prime_odd
OUTPUTS:
Enter a number: 20
Not Prime
Checks: 1
SCREENSHOTS OF THE OUTPUTS:<img width="361" height="171" alt="image" src="https://github.com/user-attachments/assets/00509b6a-be59-44ed-b442-6ce36b43aa28" />

QUESTION 7(alternative code for improved trial division prime checker)
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

int main(void)
{
    int N;

    /* READ N */
    printf("Enter N: ");
    if (scanf("%d", &N) != 1 || N < 0) {
        printf("Invalid input\n");
        return 1;
    }

    /* CREATE PRIME ARRAY FROM 0 TO N */
    bool *prime = (bool *)malloc((N + 1) * sizeof(bool));
    if (prime == NULL) {
        printf("Memory allocation failed\n");
        return 1;
    }

    /* MARK ALL VALUES AS TRUE */
    for (int i = 0; i <= N; i++) {
        prime[i] = true;
    }

    /* MARK 0 AND 1 AS FALSE */
    prime[0] = false;
    if (N >= 1) {
        prime[1] = false;
    }

    /* FOR p = 2 TO SQUARE ROOT OF N */
    for (long long p = 2; p * p <= N; p++) {

        if (prime[p] == true) {

            for (long long multiple = p * p; multiple <= N; multiple += p) {
                prime[multiple] = false;
            }
        }
    }

    /* DISPLAY ALL VALUES MARKED TRUE */
    printf("Prime numbers up to %d:\n", N);
    for (int number = 0; number <= N; number++) {
        if (prime[number] == true) {
            printf("%d ", number);
        }
    }
    printf("\n");

    free(prime);
    return 0;
}
COMMANDS USED:
gcc sieve_display.c -o sieve_display
./sieve_display
OUTPUTS:
Enter N: 30
Prime numbers up to 30:
2 3 5 7 11 13 17 19 23 29
SCREENSHOTS OF THE OUTPUTS:<img width="717" height="166" alt="image" src="https://github.com/user-attachments/assets/febe5caa-5567-4e9a-bf12-ddb33cd61fa4" />


TODO 1 – Switch ON a Device(Q-3)
#include <stdio.h>
#include <stdint.h>

int main(void)
{
    unsigned int reg;
    int device_position;
    unsigned int mask;

    /* READ register */
    printf("Enter register value (0 to 255): ");
    scanf("%u", &reg);

    /* READ device_position */
    printf("Enter device position (0 to 7): ");
    scanf("%d", &device_position);

    /* Validate (the pseudocode does not, but a bad shift is undefined in C) */
    if (reg > 255 || device_position < 0 || device_position > 7) {
        printf("Invalid input\n");
        return 1;
    }

    mask = 1U << device_position;      /* 1 LEFT SHIFT device_position */

    reg = reg | mask;                  /* switch the device ON */

    /* DISPLAY register */
    printf("Register (decimal): %u\n", reg);

    printf("Register (binary) : ");
    for (int bit = 7; bit >= 0; bit--) {
        printf("%u", (reg >> bit) & 1U);
    }
    printf("\n");

    return 0;
}
COMMANDS USED:
gcc set_bit.c -o set_bit
./set_bit
OUTPUTS:
Enter register value (0 to 255): 5
Enter device position (0 to 7): 1
Register (decimal): 7
Register (binary) : 00000111
SCREENSHOT OF THE OUTPUT:<img width="358" height="220" alt="image" src="https://github.com/user-attachments/assets/7b556cda-f2ec-45a7-b576-85c46a672cda" />

TODO 2 – Switch OFF a Device
#include <stdio.h>

int main(void)
{
    unsigned int reg;
    int device_position;
    unsigned int mask;

    /* READ register */
    printf("Enter register value (0 to 255): ");
    scanf("%u", &reg);

    /* READ device_position */
    printf("Enter device position (0 to 7): ");
    scanf("%d", &device_position);

    /* Validate (the pseudocode does not, but a bad shift is undefined in C) */
    if (reg > 255 || device_position < 0 || device_position > 7) {
        printf("Invalid input\n");
        return 1;
    }

    mask = 1U << device_position;      /* 1 LEFT SHIFT device_position */

    reg = reg & ~mask;                 /* switch the device OFF */
    reg = reg & 0xFFU;                 /* keep the register 8 bits wide */

    /* DISPLAY register */
    printf("Register (decimal): %u\n", reg);

    printf("Register (binary) : ");
    for (int bit = 7; bit >= 0; bit--) {
        printf("%u", (reg >> bit) & 1U);
    }
    printf("\n");

    return 0;
}

COMMANDS USED:
gcc clear_bit.c -o clear_bit
./clear_bit
OUTPUTS:
Enter register value (0 to 255): 7
Enter device position (0 to 7): 1
Register (decimal): 5
Register (binary) : 00000101
SCREENSHOTS OF THE OUTPUT:<img width="370" height="166" alt="image" src="https://github.com/user-attachments/assets/0f6d88a7-e31e-432a-a514-4900b2c6474a" />

TODO 3 – Toggle a Device(Q-3)
#include <stdio.h>

int main(void)
{
    unsigned int reg;
    int device_position;
    unsigned int mask;

    /* READ register */
    printf("Enter register value (0 to 255): ");
    scanf("%u", &reg);

    /* READ device_position */
    printf("Enter device position (0 to 7): ");
    scanf("%d", &device_position);

    /* Validate (a bad shift is undefined behavior in C) */
    if (reg > 255 || device_position < 0 || device_position > 7) {
        printf("Invalid input\n");
        return 1;
    }

    mask = 1U << device_position;      /* 1 LEFT SHIFT device_position */

    reg = reg ^ mask;                  /* register XOR mask (toggle) */

    /* DISPLAY register */
    printf("Register (decimal): %u\n", reg);

    printf("Register (binary) : ");
    for (int bit = 7; bit >= 0; bit--) {
        printf("%u", (reg >> bit) & 1U);
    }
    printf("\n");

    return 0;
}
COMMANDS USED:
gcc toggle_bit.c -o toggle_bit
./toggle_bit
OUTPUTS:
Enter register value (0 to 255): 7
Enter device position (0 to 7): 1
Register (decimal): 5
Register (binary) : 00000101
SCREENSHOT OF THE OUTPUT:<img width="402" height="234" alt="image" src="https://github.com/user-attachments/assets/39a321bf-d72c-41b4-b132-fa8e44b01459" />


TODO 4- check whether a device is on
#include <stdio.h>

int main(void)
{
    unsigned int reg;
    int device_position;
    unsigned int mask;
    unsigned int result;

    /* READ register */
    printf("Enter register value (0 to 255): ");
    scanf("%u", &reg);

    /* READ device_position */
    printf("Enter device position (0 to 7): ");
    scanf("%d", &device_position);

    /* Validate (a bad shift is undefined behavior in C) */
    if (reg > 255 || device_position < 0 || device_position > 7) {
        printf("Invalid input\n");
        return 1;
    }

    mask = 1U << device_position;      /* 1 LEFT SHIFT device_position */

    result = reg & mask;               /* register AND mask */

    if (result != 0) {
        printf("Device is ON\n");
    } else {
        printf("Device is OFF\n");
    }

    return 0;
}

COMMANDS USED:
gcc check_bit.c -o check_bit
./check_bit
OTPUTS:
Enter register value (0 to 255): 5
Enter device position (0 to 7): 1
Device is OFF
SCREENSHOTS OF THE OUTPUT:<img width="398" height="147" alt="image" src="https://github.com/user-attachments/assets/1acd1e36-1f40-41a4-80b9-ddc2398d4067" />

TODO 2-Grade classification using switch statement(Q-4)
#include <stdio.h>

/* Converts marks to a grade; returns '?' for invalid marks */
char get_grade(int marks)
{
    int grade_group;
    char grade;

    if (marks < 0 || marks > 100) {
        return '?';
    }

    grade_group = marks / 10;      /* integer division */

    switch (grade_group) {

        case 10:
        case 9:
            grade = 'S';
            break;

        case 8:
            grade = 'A';
            break;

        case 7:
            grade = 'B';
            break;

        case 6:
            grade = 'C';
            break;

        case 5:
            grade = 'D';
            break;

        default:
            grade = 'F';
    }

    return grade;
}

int main(void)
{
    int marks;
    char grade;

    /* READ marks */
    printf("Enter marks (0 to 100): ");
    scanf("%d", &marks);

    grade = get_grade(marks);

    if (grade == '?') {
        printf("Invalid Marks\n");
    } else {
        printf("Grade: %c\n", grade);
    }

    return 0;
}

COMMAND USED:
gcc grade_function.c -o grade_function
./grade_function
OUTPUTS:
Enter marks (0 to 100): 100
Grade: S
SCREENSHOT OF THE OUTPUT:<img width="349" height="139" alt="image" src="https://github.com/user-attachments/assets/cb05cb45-4108-4d08-b093-278aa83e1de7" />


TODO3-PRIME NUMBER CHECKING(Q-5)
#include <stdio.h>

unsigned long checks = 0;

/* Returns 1 if n is prime, otherwise 0. */
int is_prime(unsigned long n)
{
    checks = 0;

    if (n < 2)
        return 0;

    /* i <= n / i is the same as i * i <= n, but cannot overflow */
    for (unsigned long i = 2; i <= n / i; i++)
    {
        checks++;

        if (n % i == 0)
            return 0;
    }

    return 1;
}

int main(void)
{
    unsigned long tickets[] = {97, 100, 7919, 1000003};

    for (int k = 0; k < 4; k++)
    {
        int p = is_prime(tickets[k]);

        printf("%8lu %-9s divisions = %lu\n",
               tickets[k],
               p ? "prime" : "not prime",
               checks);
    }

    return 0;
}


COMMANDS USED:gcc prime_tickets.c -o prime_tickets
OUTPUTS:
      97 prime     divisions = 8
     100 not prime divisions = 1
    7919 prime     divisions = 87
 1000003 prime     divisions = 999
 
 SCREENSHOT OF THE OUTPUT:<img width="455" height="178" alt="image" src="https://github.com/user-attachments/assets/d1301336-79fa-4ddb-b2df-474235d44702" />





































