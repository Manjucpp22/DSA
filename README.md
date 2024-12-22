1. Develop a Program in C for the following: 
A. Declare a calendar as an array of 7 elements (A dynamically Created array) to represent 7 
days of a week. Each Element of the array is a structure having three fields. The first field 
is the name of the Day (A dynamically allocated String), the second field is the date of the 
Day (A integer), the third field is the description of the activity for a particular day (A 
dynamically allocated String). 
B. Write functions create(), read() and display(); to create the calendar, to read the data from 
the keyboard and to print weeks activity details report on screen. 
 
#include <stdio.h> 
#include <stdlib.h> 
#include <string.h> 
#include <ctype.h> 
 
#define NUM_DAYS_IN_WEEK 7 
typedef struct 
{ 
 char *acDayName; 
 int iDate; 
 char *acActivity; 
 } DAYTYPE; 
 void fnFreeCal (DAYTYPE *); 
 void fnDispCal (DAYTYPE *); 
 void fnReadCal (DAYTYPE *); 
 DAYTYPE *fnCreateCal(); 
  
 int main() 
 {/
 DAYTYPE *weeklyCalendar = fnCreateCal(); 
 fnReadCal (weeklyCalendar); 
 fnDispCal(weeklyCalendar);   
 fnFreeCal (weeklyCalendar); 
 return 0; 
} 
DAYTYPE *fnCreateCal () 
{ 
    DAYTYPE *calendar = (DAYTYPE *)malloc( NUM_DAYS_IN_WEEK *sizeof(DAYTYPE)); 
   for (int i = 0; i < NUM_DAYS_IN_WEEK; i++) 
    { 
    calendar[i].acDayName = NULL;  
    calendar[i].iDate = 0; 
    calendar[i].acActivity = NULL; 
    } 
return calendar; 
} 
void fnReadCal (DAYTYPE *calendar) 
{ 
char cChoice; 
for (int i = 0; i < NUM_DAYS_IN_WEEK; i++) 
    { 
    printf("Do you want to enter details for day %d [Y/N]: ", i + 1); 
    scanf("%c", &cChoice); 
    getchar(); 
    if (tolower(cChoice) == 'n') 
    continue; 
    printf("Day Name: "); 
    char nameBuffer[50]; 
    scanf("%s", &nameBuffer); 
     calendar[i].acDayName = strdup (nameBuffer); 
    printf("Date: "); 
    scanf("%d", &calendar[i].iDate); 
    printf("Activity: "); 
    char activityBuffer[100]; 
    scanf("%S", &activityBuffer); 
    calendar[i].acActivity = strdup (activityBuffer); 
    printf("\n"); 
    getchar(); 
    } 
} 
void fnDispCal (DAYTYPE *calendar) 
{ 
printf("\nWeek's Activity Details:\n"); 
for (int i = 0; i < NUM_DAYS_IN_WEEK; i++) 
{ 
printf("Day %d:\n", i + 1); 
if (calendar[i].iDate == 0) 
    { 
    printf("No Activity\n\n"); 
    continue; 
    } 
printf(" Day Name: %s\n", calendar[i].acDayName); 
printf(" Date: %d\n", calendar [i].iDate); 
printf(" Activity: %s\n\n", calendar[i].acActivity); 
} 
} 
void fnFreeCal (DAYTYPE *calendar) 
{ 
for(int i = 0; i < NUM_DAYS_IN_WEEK; i++) 
    { 
    free (calendar[i].acDayName); 
    free (calendar[i].acActivity); 
    } 
free(calendar); 
}


2). Develop a Program in C for the following operations on Strings. a. Read a main String (STR), a Pattern String (PAT) and a Replace String (REP) b. Perform Pattern Matching Operation: Find and Replace all occurrences of PAT in STR with REP if PAT exists in STR. Report suitable messages in case PAT does not exist in STR Support the program with functions for each of the above operations. Don't use Built-in functions.


#include <stdio.h>
#include <string.h>

int main()
{
    char st[200], srch[30], rep[30], res[200], cpy[200];
    int i=0, j=0 ,k=0, l, mtch, iStop, len, nom=0;

    printf("\nEnter the main string\n");
	scanf(" %[^\n]", st);

    printf("\nEnter the Pattern string\n");
	scanf(" %[^\n]", srch);

    printf("\nEnter the Replace string\n");
	scanf(" %[^\n]", rep);

    	strcpy(cpy, st);

    for(i=0;i<(strlen(st)-strlen(srch)+1);i++)
    {
        mtch = 0;

        for(j=0;j<strlen(srch);j++)
        {

            if(st[i+j] == srch[j])
            {
                mtch++;
            }
            else
            {
                break;
            }

            if(mtch == strlen(srch))   
            {
                nom++;     
                for(k=0;k<i;k++)
                {
                    res[k] = st[k];     
                }
                iStop = k + strlen(srch); 
                res[k] = '\0';
                strcat(res, rep); 
                len = strlen(res);

                for(k=iStop, l=0; st[k] != '\0';k++, l++) 
                {
                    res[len+l] = st[k];
                }
                res[len+l] = '\0';
                strcpy(st,res);
            }
        }
    }

    printf("\nInput Text\n");
    printf("%s\n",cpy);

    if(nom > 0)
    {
        printf("\n%d matches occured\n\nText after replacing matched patterns is shown below\n", nom);
        printf("\n%s\n",res);
    }
    else
    {
        printf("\nPattern String not found in Text\n");
    }
    return 0;
}

3. Develop a menu driven Program in C for the following operations on STACK of Integers (Array 
Implementation of Stack with maximum size MAX) a. Push an Element on to Stack b. Pop an Element from 
Stack c. Demonstrate how Stack can be used to check Palindrome d. Demonstrate Overflow and Underflow 
situations on Stack e. Display the status of Stack f. Exit Support the program with appropriate functions for 
each of the above operations 
 
#include <stdio.h> 
#include <stdlib.h> 
#include <stdbool.h> 
 
#define MAX 4 
 
bool fnStkFull(int); 
bool fnStkEmpty(int); 
void fnPush(int [], int, int*); 
int fnPop(int [], int*); 
void fnDisplay(int[], int); 
int fnPeek(int [], int); 
bool fnChkPalindrome(int); 
 
int main(void) 
{ 
int stkArray[MAX]; 
int top = -1; 
int iElem, iChoice; 
for(;;) 
{ 
 printf("\nSTACK OPERATIONS\n"); 
 printf("===================="); 
 printf("\n1.Push\n 
                              2.Pop\n 
     3.Display\n 
     4.Peek\n 
     5.CheckPalindrome\n 
     6.DemonstarteOverflow\n 
     7.Demonstarte Underflow\n 
     8.EXIT\n"); 
  printf("Enter your choice\n"); 
  scanf("%d",&iChoice); 
  switch(iChoice) 
  { 
  case 1: if(!fnStkFull(top)) 
                    { 
                        printf("\nEnter element to be pushed onto the stack\n"); 
                        scanf("%d", &iElem); 
                        fnPush(stkArray, iElem, &top); 
                    } 
                    else 
                    { 
                        printf("\nStack Overflow\n"); 
                    } 
 break; 
 
  case 2: if(!fnStkEmpty(top)) 
                    { 
                        iElem = fnPop(stkArray, &top); 
                        printf("\nPopped Element is %d\n", iElem); 
                    } 
                    else 
                    { 
                        printf("\nStack Underflow\n"); 
                    }
                    break; 
 
  case 3: if(fnStkEmpty(top)) 
                    { 
                        printf("\nStack Empty\n"); 
                    } 
                    else 
                    { 
                        fnDisplay(stkArray, top); 
                    } 
     break; 
 
  case 4: if(!fnStkEmpty(top)) 
     { 
      iElem = fnPeek(stkArray, top); 
      printf("\nElement at the  top of the stack is %d\n", iElem); 
     } 
     else 
      printf("\nEmpty Stack\n"); 
     break; 
 
  case 5: printf("\nEnter number to be checked for a palindrome : "); 
                    scanf("%d", &iElem); 
                    if(fnChkPalindrome(iElem)) 
                    { 
                        printf("\n%d is a palindrome\n", iElem); 
                    } 
                    else 
                    { 
                        printf("\n%d is not a palindrome\n", iElem); 
                    } 
                    break; 
 
  case 6: if(!fnStkFull(top)) 
                        printf("\nThere are currently %d elements in Stack\nPush %d elemnts for Stack to overflow", top+1, MAX - 
(top+1)); 
                    while(!fnStkFull(top)) 
                    { 
                        printf("\nEnter an element : "); 
                        scanf("%d", &iElem); 
                        fnPush(stkArray, iElem, &top); 
                    } 
                    printf("\nStack Overflow cannot push elements onto the stack\n"); 
                    break; 
 
  case 7: if(!fnStkEmpty(top)) 
                        printf("\nThere are currently %d elements in Stack\nPop out %d elemnts for Stack to Underflow", top+1, MAX - 
(top+1)); 
                    while(!fnStkEmpty(top)) 
                    { 
                        iElem = fnPop(stkArray, &top); 
                        printf("\nPopped Element is %d\n", iElem); 
                    } 
                    printf("\nStack Underflow cannot pop elements from the stack\n"); 
                    break; 
 
  case 8: exit(1); 
 
   default: printf("\nWrong choice\n"); 
  } 
 } 
 return 0; 
} 
 
bool fnStkFull(int t) 
{ 
 return ((t == MAX-1) ? true : false); 
} 
 
bool fnStkEmpty(int t) 
{ 
 return ((t == -1) ? true : false); 
} 
 
void fnPush(int stk[], int iElem, int *t) 
{ 
 *t = *t + 1; 
 stk[*t] = iElem; 
} 
 
int fnPop(int stk[], int *t) 
{ 
 int iElem; 
 iElem = stk[*t]; 
 *t = *t - 1; 
 
 return iElem; 
} 
 
void fnDisplay(int stk[], int t) 
{ 
 int i; 
 
 printf("\nStack Contents are: \n"); 
 for(i = t ; i > -1; --i) 
 { 
  printf("\t%d\n", stk[i]); 
 } 
 printf("Stack has %d elements\n", t+1); 
} 
 
int fnPeek(int stk[], int t) 
{ 
 return stk[t]; 
} 
 
bool fnChkPalindrome(int iVal) 
{ 
    int palStk[10]; 
    int t = -1, iDig, iRev = 0; 
 
    int iCopy = iVal; 
 
    while(iCopy != 0) 
    { 
        iDig = iCopy % 10; 
        fnPush(palStk, iDig, &t); 
        iCopy /= 10; 
    } 
    int p = 0; 
    while(p <= t) 
    { 
        iDig = palStk[p]; 
        iRev = iRev *10 + iDig; 
p++; 
} 
if(iRev == iVal) 
return true; 
else 
return false; 
}


  4. Develop a Program in C for converting an Infix Expression to Postfix 
Expression.  Program  should  support  for  both  parenthesized  and free  
parenthesized expressions with the operators: +, -, *, /, % (Remainder), ^ 
(Power) and alphanumeric operands. 
 
#include <stdio.h> 
#include <ctype.h> 
#include <stdlib.h> 
#include <string.h> 
 
#define STK_SIZE 10 
 
void fnPush(char [], int*, char); 
char fnPop(char [], int*); 
int fnPrecd(char); 
 
int main() 
{ 
 int i, j=0; 
 char acExpr[50], acStack[50], acPost[50], cSymb; 
 int top = -1; 
 
 printf("\nEnter a valid infix expression\n"); 
 scanf("%s", acExpr); 
 
 fnPush(acStack, &top, '#'); 
 for(i=0;acExpr[i]!='\0'; ++i) 
 { 
  cSymb = acExpr[i]; 
  if(isalnum(cSymb)) 
  { 
   acPost[j++] = cSymb; 
  } 
  else if(cSymb == '(') 
  { 
   fnPush(acStack, &top, cSymb); 
  } 
  else if(cSymb == ')') 
  { 
   while(acStack[top] != '(') 
{ 
    acPost[j++] = fnPop(acStack, &top); 
   } 
   fnPop(acStack, &top); 
  } 
  else 
  { 
   while(fnPrecd(acStack[top]) >= fnPrecd(cSymb)) 
   { 
    if((cSymb == '^') && (acStack[top] == '^')) 
     break; 
                acPost[j++] = fnPop(acStack, &top); 
   } 
   fnPush(acStack, &top, cSymb); 
  } 
 
 } 
 while(acStack[top] != '#') 
 { 
  acPost[j++] = fnPop(acStack, &top); 
 } 
 acPost[j] = '\0'; 
 
 printf("\nInfix Expression is %s\n", acExpr); 
 printf("\nPostfix Expression is %s\n", acPost); 
 return 0; 
} 
 
void fnPush(char Stack[], int *t , char elem) 
{ 
 *t = *t + 1; 
 Stack[*t] = elem; 
 
} 
 
char fnPop(char Stack[], int *t) 
{ 
 char elem; 
 elem = Stack[*t]; 
 *t = *t -1; 
 return elem; 
} 
 
int fnPrecd(char ch) 
{ 
 int iPrecdVal; 
 switch(ch) 
 { 
  case '#' :  iPrecdVal = -1; break; 
  case '(' :  iPrecdVal = 0; break; 
  case '+' : 
  case '-' :  iPrecdVal = 1; break; 
  case '%' : 
  case '*' : 
  case '/' :  iPrecdVal = 2; break; 
  case '^' : iPrecdVal = 3; break; 
 } 
 return iPrecdVal; 
}



5. Develop a Program in C for the following Stack Applications  
a. Evaluation of Suffix expression with single digit operands and operators: +, -, *, /, %, ^  
b. Solving Tower of Hanoi problem with n disks   
 
void push(int [], int*, int); 
int pop(int [], int*); 
 
int main() 
{ 
 int iastack[50], i, op1, op2, res; 
 char expr[50], symb; 
 int top = -1; 
 
 printf("\nEnter a valid postfix expression\n"); 
 scanf("%s", expr); 
 
 for(i=0; i<strlen(expr); i++) 
 { 
  symb = expr[i]; 
 
  if(isdigit(symb)) 
 
  { 
   push(iastack, &top, symb-'0'); 
  } 
  else 
  { 
   op2 = pop(iastack, &top); 
   op1 = pop(iastack, &top); 
   switch(symb) 
   { 
    case '+' :  res = op1 + op2; 
       break; 
    case '-' :  res = op1 - op2; 
       break; 
    case '*' :  res = op1 * op2; 
       break; 
    case '/' :  res = op1 / op2; 
       break; 
    case '%' :  res = op1 % op2; 
       break; 
    case '^' :  res = (int)pow(op1 , op2); 
       break; 
   } 
   push(iastack, &top, res); 
  } 
 } 
 res = pop(iastack, &top); 
 printf("\nValue of %s expression is %d\n", expr, res); 
 return 0; 
} 
 
void push(int Stack[], int *t , int elem) 
{ 
 *t = *t + 1; 
 Stack[*t] = elem; 
 
} 
 
int pop(int Stack[], int *t) 
{ 
 int elem; 
 elem = Stack[*t]; 
 *t = *t -1; 
 return elem; 
}

5. Develop a Program in C for the following Stack Applications  
b. Solving Tower of Hanoi problem with n disks   
 
#include <stdio.h> 
void towers(int, char, char, char); 
int main() 
{ 
    int num; 
    printf("Enter the number of disks : "); 
    scanf("%d", &num); 
    printf("The sequence of moves involved in the Tower of Hanoi are :\n"); 
    towers(num, 'A', 'C', 'B'); 
    printf("\n"); 
    return 0; 
} 
void towers(int num, char frompeg, char topeg, char auxpeg) 
{ 
    if (num == 1) 
    { 
        printf("\n Move disk 1 from peg %c to peg %c", frompeg, topeg); 
        return; 
    } 
    towers(num - 1, frompeg, auxpeg, topeg); 
    printf("\n Move disk %d from peg %c to peg %c", num, frompeg, topeg); 
    towers(num - 1, auxpeg, topeg, frompeg); 
}

