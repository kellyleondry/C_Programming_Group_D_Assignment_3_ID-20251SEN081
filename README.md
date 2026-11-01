# C_Programming_Group_D_Assignment_3_ID-20251SEN081
ASSIGNMENT 3

# RUNNABLE CODES
Q.1


#include <stdio.h>

// Function declarations
void inputMarks(int arr[], int size);
int findTotal(int arr[], int size);
float findAverage(int total, int size);
int findMax(int arr[], int size);
int findMin(int arr[], int size);
int countPass(int arr[], int size);

int main()
{
    int marks[5];
    int total, highest, lowest;
    int passed, failed;
    float average;

    // Input marks
    inputMarks(marks, 5);

    // Calculate results using functions
    total = findTotal(marks, 5);
    average = findAverage(total, 5);
    highest = findMax(marks, 5);
    lowest = findMin(marks, 5);
    passed = countPass(marks, 5);

    // Calculate failed students
    failed = 5 - passed;

    // Display all marks
    printf("\n===== STUDENT RESULTS =====\n");

    for (int i = 0; i < 5; i++)
    {
        printf("Student %d: %d\n", i + 1, marks[i]);
    }

    // Display total and average
    printf("\nTotal Marks: %d\n", total);
    printf("Average Mark: %.2f\n", average);

    // Display highest and lowest
    printf("Highest Mark: %d\n", highest);
    printf("Lowest Mark: %d\n", lowest);

    // Display pass and fail
    printf("Students Passed: %d\n", passed);
    printf("Students Failed: %d\n", failed);

    // Check pass conditions
    if (passed == 0)
    {
        printf("No student passed.\n");
    }
    else if (passed == 5)
    {
        printf("All students passed.\n");
    }

    // Check identical marks
    if (highest == lowest)
    {
        printf("All marks are identical.\n");
    }

    // Classify performance
    if (average >= 70)
    {
        printf("Performance: Excellent\n");
    }
    else if (average >= 50)
    {
        printf("Performance: Moderate\n");
    }
    else
    {
        printf("Performance: Poor\n");
    }

    return 0;
}

// Function to input and validate marks
void inputMarks(int arr[], int size)
{
    for (int i = 0; i < size; i++)
    {
        do
        {
            printf("Enter marks for student %d: ", i + 1);
            scanf("%d", &arr[i]);

            if (arr[i] < 0 || arr[i] > 100)
            {
                printf("Invalid mark! Enter a value between 0 and 100.\n");
            }

        } while (arr[i] < 0 || arr[i] > 100);
    }
}

// Function to calculate total marks
int findTotal(int arr[], int size)
{
    int total = 0;

    for (int i = 0; i < size; i++)
    {
        total += arr[i];
    }

    return total;
}

// Function to calculate average
float findAverage(int total, int size)
{
    return (float)total / size;
}

// Function to find highest mark
int findMax(int arr[], int size)
{
    int max = arr[0];

    for (int i = 1; i < size; i++)
    {
        if (arr[i] > max)
        {
            max = arr[i];
        }
    }

    return max;
}

// Function to find lowest mark
int findMin(int arr[], int size)
{
    int min = arr[0];

    for (int i = 1; i < size; i++)
    {
        if (arr[i] < min)
        {
            min = arr[i];
        }
    }

    return min;
}

// Function to count students who passed
int countPass(int arr[], int size)
{
    int count = 0;

    for (int i = 0; i < size; i++)
    {
        if (arr[i] >= 50)
        {
            count++;
        }
    }

    return count;
}


Q.2

#include <stdio.h>

// Function declaration
void withdraw(int *balance, int amount);

int main()
{
    int balance = 50000;
    int amount;
    int totalWithdrawals = 0;
    int totalAmount = 0;
    int invalidAttempts = 0;
    int choice;

    printf("Initial Balance: %d RWF\n", balance);

    while (balance > 0)
    {
        printf("\nEnter withdrawal amount: ");
        scanf("%d", &amount);

        // Check invalid transactions
        if (amount <= 0 || amount > balance)
        {
            invalidAttempts++;

            printf("Invalid withdrawal amount!\n");

            if (invalidAttempts == 3)
            {
                printf("Transaction session terminated due to repeated invalid attempts.\n");
                break;
            }

            continue;
        }

        // Process withdrawal
        withdraw(&balance, amount);

        // Update transaction records
        totalWithdrawals++;
        totalAmount += amount;

        invalidAttempts = 0;

        printf("Withdrawal Amount: %d RWF\n", amount);
        printf("New Balance: %d RWF\n", balance);

        // Check if account is empty
        if (balance == 0)
        {
            printf("Account emptied successfully.\n");
            break;
        }

        // Ask whether to continue
        printf("\nDo you want another withdrawal? (1 = Yes, 0 = No): ");
        scanf("%d", &choice);

        if (choice == 0)
        {
            break;
        }
    }

    // Display final transaction summary
    printf("\n===== TRANSACTION SUMMARY =====\n");
    printf("Successful Withdrawals: %d\n", totalWithdrawals);
    printf("Total Amount Withdrawn: %d RWF\n", totalAmount);
    printf("Final Balance: %d RWF\n", balance);

    return 0;
}

// Function to process withdrawal using pointer
void withdraw(int *balance, int amount)
{
    *balance = *balance - amount;
}

Q.3

#include <stdio.h>

// Function declarations
void inputStock(int arr[], int size);
int totalStock(int arr[], int size);
void findLowStock(int arr[], int size);
void sortStock(int arr[], int size);
void updateStock(int *item);

int main()
{
    int stock[8];
    int index;
    int lowCount = 0;
    int total;

    // Input stock quantities
    inputStock(stock, 8);

    // Ask user to select a product
    do
    {
        printf("\nEnter product index to update (0-7): ");
        scanf("%d", &index);

        if (index < 0 || index >= 8)
        {
            printf("Invalid product index! Try again.\n");
        }

    } while (index < 0 || index >= 8);

    // Update selected product using its address
    updateStock(&stock[index]);

    // Sort stock in ascending order
    sortStock(stock, 8);

    // Display updated and sorted stock
    printf("\n===== UPDATED STOCK LIST =====\n");

    for (int i = 0; i < 8; i++)
    {
        printf("Product %d: %d\n", i + 1, stock[i]);
    }

    // Calculate total stock
    total = totalStock(stock, 8);

    // Display total stock
    printf("\nTotal Stock: %d\n", total);

    // Count low-stock products
    printf("\n===== LOW STOCK REPORT =====\n");

    for (int i = 0; i < 8; i++)
    {
        if (stock[i] < 5)
        {
            lowCount++;
        }
    }

    findLowStock(stock, 8);

    printf("Number of low-stock items: %d\n", lowCount);

    return 0;
}

// Function to input and validate stock
void inputStock(int arr[], int size)
{
    for (int i = 0; i < size; i++)
    {
        do
        {
            printf("Enter stock for product %d: ", i + 1);
            scanf("%d", &arr[i]);

            if (arr[i] < 0)
            {
                printf("Invalid stock! Quantity cannot be negative.\n");
            }

        } while (arr[i] < 0);
    }
}

// Function to calculate total stock
int totalStock(int arr[], int size)
{
    int total = 0;

    for (int i = 0; i < size; i++)
    {
        total += arr[i];
    }

    return total;
}

// Function to identify low-stock products
void findLowStock(int arr[], int size)
{
    int count = 0;

    for (int i = 0; i < size; i++)
    {
        if (arr[i] < 5)
        {
            printf("Product %d has low stock: %d\n", i + 1, arr[i]);
            count++;
        }
    }

    if (count == size)
    {
        printf("All products are low in stock.\n");
    }
    else if (count == 0)
    {
        printf("No low-stock products.\n");
    }
}

// Function to sort stock in ascending order
void sortStock(int arr[], int size)
{
    int temp;

    for (int i = 0; i < size - 1; i++)
    {
        for (int j = 0; j < size - 1 - i; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

// Function to update stock using a pointer
void updateStock(int *item)
{
    int newStock;

    do
    {
        printf("Enter new stock quantity: ");
        scanf("%d", &newStock);

        if (newStock < 0)
        {
            printf("Invalid stock! Quantity cannot be negative.\n");
        }

    } while (newStock < 0);

    *item = newStock;
}



Q.4

#include <stdio.h>
#include <ctype.h>
#include <string.h>

// Function declarations
void analyze(char *str, int *v, int *c, int *d, int *s);
void reverse(char *str);
int isPalindrome(char *str);

int main()
{
    char str[200];

    int vowels = 0, consonants = 0;
    int digits = 0, special = 0;

    printf("Enter a sentence: ");
    fgets(str, sizeof(str), stdin);

    // Remove newline added by fgets()
    str[strcspn(str, "\n")] = '\0';

    // Analyze the string
    analyze(str, &vowels, &consonants, &digits, &special);

    printf("\n===== STRING ANALYSIS =====\n");
    printf("Vowels: %d\n", vowels);
    printf("Consonants: %d\n", consonants);
    printf("Digits: %d\n", digits);
    printf("Special Characters: %d\n", special);

    // Check palindrome before reversing original string
    if (isPalindrome(str))
    {
        printf("The string is a palindrome.\n");
    }
    else
    {
        printf("The string is not a palindrome.\n");
    }

    // Reverse the original string
    reverse(str);

    printf("Reversed String: %s\n", str);

    return 0;
}

// Function to analyze characters using pointers
void analyze(char *str, int *v, int *c, int *d, int *s)
{
    while (*str != '\0')
    {
        if (isalpha(*str))
        {
            char ch = tolower(*str);

            if (ch == 'a' || ch == 'e' || ch == 'i' ||
                ch == 'o' || ch == 'u')
            {
                (*v)++;
            }
            else
            {
                (*c)++;
            }
        }
        else if (isdigit(*str))
        {
            (*d)++;
        }
        else if (!isspace(*str))
        {
            (*s)++;
        }

        str++;
    }
}

// Function to reverse the string using pointers
void reverse(char *str)
{
    char *start = str;
    char *end = str;
    char temp;

    // Find the last character
    while (*end != '\0')
    {
        end++;
    }

    end--;

    // Swap characters
    while (start < end)
    {
        temp = *start;
        *start = *end;
        *end = temp;

        start++;
        end--;
    }
}

// Function to check palindrome using pointers
int isPalindrome(char *str)
{
    char *left = str;
    char *right = str;

    // Find the end of the string
    while (*right != '\0')
    {
        right++;
    }

    right--;

    // Compare characters from both ends
    while (left < right)
    {
        // Ignore spaces
        if (isspace(*left))
        {
            left++;
            continue;
        }

        if (isspace(*right))
        {
            right--;
            continue;
        }

        // Compare without considering uppercase/lowercase
        if (tolower(*left) != tolower(*right))
        {
            return 0;
        }

        left++;
        right--;
    }

    return 1;
}



# EXPLANATIONS
1. Student Result Processing System

The Student Result Processing System is designed to process and analyze marks for five students. The program first accepts marks from the user and checks that each mark is between 0 and 100. It uses an array to store all the marks. The inputMarks() function handles entering and validating the marks. The findTotal() function calculates the sum of all marks, while findAverage() calculates the average mark. The findMax() and findMin() functions identify the highest and lowest marks. The countPass() function counts students who scored 50 or above. Finally, the program displays the marks, total, average, highest mark, lowest mark, and students' performance.

2. Bank Withdrawal System Using Pointers

The Bank Withdrawal System allows a user to withdraw money from an account. The program starts with an initial account balance and allows multiple withdrawal transactions. It uses the withdraw() function to process each transaction. A pointer is used to access and modify the original account balance. The program checks whether the withdrawal amount is valid and whether sufficient money is available. Invalid transactions are rejected, and after three consecutive invalid attempts, the program terminates. After every successful withdrawal, the remaining balance is updated. The process continues until the user stops or the balance reaches zero. Finally, the program displays the total amount withdrawn, number of successful transactions, and remaining balance.

3. Warehouse Stock Management System

The Warehouse Stock Management System manages the stock quantities of eight products. The program uses an array to store the quantity of each product. The inputStock() function allows the user to enter stock quantities and prevents negative values. The totalStock() function calculates the total quantity of all products. The findLowStock() function identifies products with fewer than five items remaining. The user can select a product and update its quantity using the updateStock() function. Pointers are used to modify the selected product's original stock value. The sortStock() function arranges all stock quantities in ascending order. Finally, the program displays the updated stock, total stock, and low-stock information.

4. String Processing System Using Pointers

The String Processing System accepts a complete sentence from the user using the fgets() function. It uses pointers to access and process individual characters without using array indexing inside the functions. The analyze() function counts vowels, consonants, digits, and special characters in the sentence. It uses character-checking functions to identify different types of characters. The reverse() function reverses the sentence by exchanging characters from opposite ends using pointers. The isPalindrome() function checks whether the sentence reads the same forward and backward. It ignores spaces and differences between uppercase and lowercase letters. The original sentence is checked before it is reversed. Finally, the program displays the character analysis, palindrome result, and reversed sentence.
