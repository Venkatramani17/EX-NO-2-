## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.




Program:



#include <stdio.h>
#include <string.h>
#include <ctype.h>


char a[5][5];


int main() {
    char key[100], text[100], ch;
    int used[26] = {0}, i, j, k = 0;
    int r1, c1, r2, c2;


    printf("Enter key: ");
    scanf("%s", key);
    printf("Enter plaintext: ");
    scanf("%s", text);


    used['J'-'A'] = 1;


    for (i = 0; key[i]; i++) {
        ch = toupper(key[i]);
        if (ch == 'J') ch = 'I';
        if (ch >= 'A' && ch <= 'Z' && !used[ch-'A']) {
            a[k/5][k%5] = ch;
            used[ch-'A'] = 1;
            k++;
        }
    }


    for (ch = 'A'; ch <= 'Z'; ch++)
        if (!used[ch-'A'])
            a[k/5][k++%5] = ch;


    for (i = 0; text[i]; i++)
        text[i] = toupper(text[i]) == 'J' ? 'I' : toupper(text[i]);


    printf("Cipher text: ");


    for (i = 0; text[i]; i += 2) {
        ch = text[i];
        char d = text[i+1] ? text[i+1] : 'X';


        for (r1=0;r1<5;r1++)
            for (c1=0;c1<5;c1++)
                if (a[r1][c1]==ch) goto first;
        first:
        for (r2=0;r2<5;r2++)
            for (c2=0;c2<5;c2++)
                if (a[r2][c2]==d) goto second;
        second:


        if (r1==r2)
            printf("%c%c",a[r1][(c1+1)%5],a[r2][(c2+1)%5]);
        else if (c1==c2)
            printf("%c%c",a[(r1+1)%5][c1],a[(r2+1)%5][c2]);
        else
            printf("%c%c",a[r1][c2],a[r2][c1]);
    }


    printf("\n");
    return 0;
}




Output:
<img width="393" height="82" alt="Screenshot 2026-10-27 092735" src="https://github.com/user-attachments/assets/d39ed951-2f7d-40c9-88be-e00198b0f374" />


