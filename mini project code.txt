//**********************************************NECESSARY HEADER FILES**********************************************************


#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
#include<string.h>
#include<windows.h>

//************************************************GLOBAL VARIABLES**************************************************************

typedef struct{
	char name[50];
	int train_num;
	int num_of_seats;
}pd;




//***********************************************FUNCTION PROTOTYPE************************************************************
//function prototypes required
void reservation(void);							//main reservation function
void viewdetails(void);							//details of all the trains
void cancel(void);                              //cancellation
void printticket(char name[],int,int,float);	//print ticket
void specifictrain(int);						//print data related to specific train
float charge(int,int);							//charge automatically w.r.t number of seats and train
void login();


//**********************************************FUNCTION DECLARATION************************************************************

//*************************************************MAIN()***********************************************************************

int main()

{
    system("Color 0A");
		system("cls");

	printf("\t\t\t\t=================================================\n");
	printf("\t\t\t\t|                                               |\n");
	printf("\t\t\t\t|        -----------------------------          |\n");
	printf("\t\t\t\t|          RAILWAY RESERVATION SYSTEM           |\n");
	printf("\t\t\t\t|        -----------------------------          |\n");
	printf("\t\t\t\t|                                               |\n");
	printf("\t\t\t\t|                                               |\n");
	printf("\t\t\t\t|                                               |\n");
	printf("\t\t\t\t|                    MADE BY                    |\n");
	printf("\t\t\t\t|           |  Sahib Singh Kapoor  |            |\n");
	printf("\t\t\t\t|                                               |\n");
	printf("\t\t\t\t=================================================\n\n\n");


	printf(" \n\b Press any key to continue:");

	getch();
    system("cls");
	login();
	int menu_choice,choice_return;
	start:
	system("cls");
	printf("\n\t\t\t=================================================================================\n");
	printf("\t\t\t                          TRAIN RESERVATION SYSTEM");
	printf("\n\t\t\t==================================================================================");
	printf("\n\n\n\t\t1>> Reserve A Ticket");
	printf("\n\t\t-------------------------------------");
	printf("\n\n\n\t\t2>> View All Available Trains");
	printf("\n\t\t-------------------------------------");
	printf("\n\n\n\t\t3>> Cancel Reservation");
	printf("\n\t\t-------------------------------------");
	printf("\n\n\n\t\t4>> Exit");
	printf("\n\t\t-------------------------------------");
	printf("\n\n\t\t-->");
	scanf("%d",&menu_choice);
	switch(menu_choice)
	{
		case 1:
			reservation();
			break;
		case 2:
			viewdetails();
			printf("\n\n\n\nPress any key to go to Main Menu..");
			getch();
			break;
		case 3:
			cancel();

			break;
		case 4:
			return(0);
		default:
			printf("\nInvalid choice");
	}
	goto start;
	return(0);
}

//*********************************************DETAILS OF AVAILABLE TRAINS*************************************************/



void viewdetails(void)
{
	system("cls");
	printf("------------------------------------------------------------------------------------------------------------");
	printf("\nTr.No\tName\t\t\tDestinations\t\t         Charges\t\t     Time\n");
	printf("------------------------------------------------------------------------------------------------------------");
	printf("\n1001\tDORONTO\t\t        MUMBAI to AHEMDABAD\t\tRs.5000\t                     23:25");
	printf("\n1001\tDORONTO\t\t        KOLKATA to PURI\t\t        Rs.5000\t                     20:00");
	printf("\n1003\tRAJDHANI\t\tNEW DELHI to LUCKHNOW\t\tRs.4500\t                     20:50");
	printf("\n1004\tRAJDHANI\t\tMUMBAI to NEW DELHI\t\tRs.4500\t                     16:35");
	printf("\n1005\tSHATABDI\t\tHOWRAH to RANCHI\t\tRs.4000\t                     6:05");
	printf("\n1006\tSHATABDI\t\tLUDHIANA to NEW DELHI\t\tRs.4000\t                     16:40");
    printf("\n1007\tSUPERFAST\t\tFIROZPUR to MUMBAI\t\tRs.3500\t                     21:40");
    printf("\n1008\tSUPERFAST\t\tHOWRAH to JODHPUR\t\tRs.3500\t                     23:30");
    printf("\n1009\tMAIL EXPRESS\t\tPUNE to JAMMU\t\t        Rs.6000\t                     17:20");


}

//*********************************************RESERVATION OF TICKET**************************************************

void reservation(void)
{
	char confirm;
	int i=0;
	float charges;
	pd passdetails;
	FILE *fp;
	fp=fopen("seats_reserved.txt","a");
	system("cls");

	printf("\n\tEnter Your Name:> ");
	fflush(stdin);
	gets(passdetails.name);

	printf("\n\tEnter Number of seats:> ");
	scanf("%d",&passdetails.num_of_seats);
	printf("\n\n>>Press Enter To View Available Trains<< ");
	getch();
	system("cls");
	viewdetails();
	printf("\n\n\tEnter train number:> ");
	start1:
	scanf("%d",&passdetails.train_num);
	if(passdetails.train_num>=1001 && passdetails.train_num<=1009)
	{
		charges=charge(passdetails.train_num,passdetails.num_of_seats);
		printticket(passdetails.name,passdetails.num_of_seats,passdetails.train_num,charges);
	}
	else
	{
		printf("\nInvalid train Number! Enter again--> ");
		goto start1;
	}

	printf("\n\nConfirm Ticket (y/n):>  ");
	start:
	scanf(" %c",&confirm);
	if(confirm == 'y')
	{
		fprintf(fp,"%s\t\t%d\t\t%d\t\t%.2f\n",&passdetails.name,passdetails.num_of_seats,passdetails.train_num,charges);
		printf("===========================================");
		printf("\n           Reservation Done\n");
		printf("===========================================");
		printf("\nPress any key to go back to Main menu");
	}
	else
	{
		if(confirm=='n'){
			printf("\nReservation Not Done!\nPress any key to go back to  Main menu!");
		}
		else
		{
			printf("\nInvalid choice entered! Enter again----->  ");
			goto start;
		}
	}
	fclose(fp);
	getch();
}

//*********************************************COST OF THE TICKET(s)*************************************************

float charge(int train_num,int num_of_seats)
{
		if (train_num==1001)
	{
		return(5000.0*num_of_seats);
	}
	if (train_num==1002)
	{
		return(5000.0*num_of_seats);
	}
	if (train_num==1003)
	{
		return(4500.0*num_of_seats);
	}
	if (train_num==1004)
	{
		return(4500.0*num_of_seats);
	}
	if (train_num==1005)
	{
		return(4000.0*num_of_seats);
	}
	if (train_num==1006)
	{
		return(4000.0*num_of_seats);
	}
	if (train_num==1007)
	{
		return(3500.0*num_of_seats);
	}
	if (train_num==1008)
	{
		return(3500.0*num_of_seats);
	}
	if (train_num==1009)
	{
		return(6000.0*num_of_seats);
	}

}


//*********************************************PRINTING THE TICKET*************************************************

void printticket(char name[],int num_of_seats,int train_num,float charges)
{
	system("cls");
	printf("----------------------------------------------------------|\n");
	printf("                        TICKET                            |\n");
	printf("----------------------------------------------------------|\n");
	printf("         \t\t\t                          |");
	printf("\n    Name:\t\t\t%s                     |",name);
	printf("\n    Number Of Seats:\t\t%d                         |",num_of_seats);
	printf("\n    Train Number:\t\t%d                      |",train_num);
	specifictrain(train_num);

	printf("\n----------------------------------------------------------|\n");
	printf("\n    Charges:       \t\t%.2f",charges);
}

//*********************************************SPECIFICTRAINS*************************************************

void specifictrain(int train_num)
{

	if (train_num==1001)
	{
		printf("\n    Train:\t\t\tDoronto                   |");
		printf("\n    Destination:\t\tMUMBAI to AHEMDABAD       |");
		printf("\n    Departure:\t\t        23:25                     |");
	}
	if (train_num==1002)
	{
		printf("\n    Train:\t\t\tDoronto                   |");
		printf("\n    Destination:\t\tKOLKATA to PURI           |");
		printf("\n    Departure:\t\t        20:00                     |");
	}
	if (train_num==1003)
	{
		printf("\n    Train:\t\t\tRajdhani                  |");
		printf("\n    Destination:\t\tNEW DELHI to LUCKHNOW     |");
		printf("\n    Departure:\t\t        20:50                     |");
	}
	if (train_num==1004)
	{
		printf("\n    Train:\t\t\tRajdhani                  |");
		printf("\n    Destination:\t\tMUMBAI to NEW DELHI       |");
		printf("\n    Departure:\t\t        16:35                     |");
	}
	if (train_num==1005)
	{
		printf("\n    Train:\t\t\tShatabdi                  |");
		printf("\n    Destination:\t\tHOWRAH to RANCHI          |");
		printf("\n    Departure:\t\t        6:05                      |");
	}
	if (train_num==1006)
	{
		printf("\n    Train:\t\t\tShatabdi                  |");
		printf("\n    Destination:\t\tLUDHIANA to NEW DELHI     |");
		printf("\n    Departure:\t\t        16:40                     |");
	}
	if (train_num==1007)
	{
		printf("\n    Train:\t\t\tSuperfast                |");
		printf("\n    Destination:\t\tFIROZPUR to MUMBAI        |");
		printf("\n    Departure:\t\t        21:40                     |");
	}
	if (train_num==1008)
	{
		printf("\n    Train:\t\t\tSuperfast                 |");
		printf("\n    Destination:\t\tHOWRAH to JODHPUR         |");
		printf("\n    Departure:\t\t        23:30                     |");
	}
	if (train_num==1009)
	{
		printf("\n    Train:\t\t\tMail Express              |");
		printf("\n    Destination:\t\tPUNE to JAMMU             |");
		printf("\n    Departure:\t\t        17:20                     |");
	}

}
//************************************************LOGIN SCREEN*****************************************************
void login()
{
	int a=0,i=0;
    char uname[10],c=' ';
    char pword[10],code[10];
    char user[10]="sahib";
    char pass[10]="12345";
    do
{
    printf("\t\t -------------------------------------------------------------------\n");
	printf("\t\t|                                                                   |\n");
    printf("\t\t|   ======================= LOGIN PORTAL =======================    |\n");
    printf("\t\t|                                                                   |\n");
    printf("\t\t -------------------------------------------------------------------\n");

    printf(" \n                       ENTER USERNAME:-  ");
	scanf("%s", &uname);
	printf(" \n                       ENTER PASSWORD:-  ");
	while(i<10)
	{
	    pword[i]=getch();
	    c=pword[i];
	    if(c==13) break;
	    else printf("*");
	    i++;
	}
	pword[i]='\0';

	i=0;

		if(strcmp(uname,"sahib")==0 && strcmp(pword,"12345")==0)
	{
	printf("  \n\n\n \t\t\t      WELCOME TO THIS SYSTEM !! YOUR LOGIN IS VALIDATED");
	printf("\n\n\n\t\t\t\tPress any key to continue... ");
	getch();
	break;
	}
	else
	{
		printf("\n        SORRY !!!!  LOGIN IS NOT VALID");
		a++;

		getch();
		system("cls");
	}
}
	while(a<=2);
	if (a>2)
	{
		printf("\nSorry you have entered the wrong username and password for four times!!!");

		getch();


		}
		system("cls");
}
//*****************************************************CANCELLATION*************************************************
void cancel(void)
{

	system("cls");
	int trainnum;
	printf("-----------------------\n");
		printf("Enter the train number: \n");
			printf("-----------------------\n");
		fflush(stdin);
		scanf("%i",&trainnum);
		printf("\n\nCancelled");
		getch();
}





