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
// Structure to represent a day 
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
 {
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
DATA STRUCTURES LAB                                                                                                       BCSL305 
 
VTU, Belagavi  2 
 
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
DATA STRUCTURES LAB                                                                                                       BCSL305 
 
VTU, Belagavi  3 
 
OUT PUT: 
 
Do you want to enter details for day 1 
[Y/N]: y 
Day Name: sunday 
Date: 11 
Activity: sports 
Do you want to enter details for day 2 
[Y/N]: y 
Day Name: monday 
Date: 12 
Activity: International conference 
Do you want to enter details for day 3 
[Y/N]: Day Name: Date: n 
Activity:  
Do you want to enter details for day 4 
[Y/N]: n 
Do you want to enter details for day 5 
[Y/N]: n 
Do you want to enter details for day 6 
[Y/N]: n 
Do you want to enter details for day 7 
[Y/N]: n 
Week's Activity Details: 
Day 1: 
 
 
Day Name: Sunday 
Date: 11 
Activity: s 
Day 2: 
Day Name: Monday 
Date: 12 
Activity: I 
Day 3: 
No Activity 
Day 4: 
No Activity 
Day 5: 
No Activity 
Day 6: 
No Activity 
Day 7: 
No Activit
