########1st Code#######
#include <stdio.h>
#include <stdlib.h>
int main()


{
    int *arr;
    int n, i, choice, pos, x, key, found = 0;
    printf("Enter the number of elements in the array:");
    scanf("%d", &n);
    /* Dynamic memory allocation */
    arr = (int *)malloc(n * sizeof(int));

    printf("Enter the elements");

    for (i = 0; i < n; i++)
    {
        scanf("%d", (arr + i));
        printf("The elements of the array are :\n");
    }
    for (i = 0; i < n; i++)
    {
        printf("*(arr+%d)=%d\n", i, *(arr + i));
    }
    while (1)
    {
        printf("1-> INSERT  2-> DELETE   3-> SEARCH    4->EXIT\n");
        printf("Give your choice:");
        scanf("%d", &choice);
        switch (choice)
        {
        case 1: //  Insert an element
            printf("Enter the element to be inserted:");
            scanf("%d", &x);
            printf("Enter the position to be inserted:");
            scanf("%d", &pos);
            n++;
            for (i = n - 1; i >= pos; i--)
                *(arr + i) = *(arr + i - 1);
            *(arr + pos - 1) = x;

            // print the updated array
            printf("The elements of the array are :\n");
            for (i = 0; i < n; i++)
            {
                printf("*(arr+%d)=%d\n", i, *(arr + i));
            }
            break;

        case 2: // Delete an element
            printf("Enter the position of the element to be deleted:");
            scanf("%d", &pos);
            for (i = pos; i <= n - 1; i++)
                *(arr + i - 1) = *(arr + i);
            n--;
            // print the updated array
            printf("The elements of the array are :\n");
            for (i = 0; i < n; i++)
            {
                printf("*(arr+%d)=%d\n", i, *(arr + i));
            }
            break;
        case 3: // Search an element
            found = 0;
            printf("Enter the  element to be searched:");
            scanf("%d", &key);
            for (i = 0; i <= n; i++)
                if (*(arr + i) == key)
                {
                    found = 1;
                    printf("\n Search key %d is found at position %d", i + 1);
                }
            if (found == 0)
                printf("Search key %d is not found", key);
            break;
        case 4:
            exit(1);
        } /* switch*/
    }     /*while*/
} /*main()*/

#####################2ND##################333

#include <stdio.h>
#include <stdlib.h>
void main()
{
    int i, j, k, m, n, p, q, sum, choice;
    int *A[3], *B[3], *C[3];
    printf("enter the order of matrix 1\n");
    scanf("%d%d", &m, &n);
    printf("enter the order of matrix 2\n");
    scanf("%d %d", &p, &q);
    for (i = 0; i < m; i++)
        A[i] = (int *)malloc(n * sizeof(int));
    for (i = 0; i < p; i++)
        B[i] = (int *)malloc(q * sizeof(int));
    printf("enter elements of matrix 1\n");
    for (i = 0; i < m; i++)
        for (j = 0; j < n; j++)
            scanf("%d", A[i] + j);

    printf("enter elements of matrix 2\n");
    for (i = 0; i < p; i++)
        for (j = 0; j < q; j++)
            scanf("%d", B[i] + j);
    while (1)
    {
        printf("\n 1->Addition of matrix  2->Multiplication of matrix   3->Exit");
        scanf("%d", &choice);

        switch (choice)
        {
        case 1:
            if (m != p || n != q)
                printf("Matrix order mismatch - Addition not possible\n");
            else
            {
                for (i = 0; i < m; i++)
                    C[i] = (int *)malloc(n * sizeof(int));

                for (i = 0; i < m; i++)
                    for (j = 0; j < n; j++)
                        *(C[i] + j) = *(A[i] + j) + *(B[i] + j);

                printf("\n Result of matrix addition:\n");
                for (i = 0; i < m; i++)
                {
                    for (j = 0; j < n; j++)
                    {
                        printf("\t%d", *C[i] + j);
                    }
                    printf("\n");
                }
            }
            break;
        case 2:
            if (n != p)
                printf("\nmatrices cannot be multiplied\n");
            else
            {
                for (i = 0; i < p; i++)
                {
                    C[i] = (int *)malloc(q * sizeof(int));
                }

                for (i = 0; i < m; i++)
                    for (j = 0; j < p; j++)
                    {
                        *(C[i] + j) = 0;
                        for (k = 0; k < n; k++)
                            *(C[i] + j) = *(C[i] + j) + *(A[i] + k) * *(B[k] + j);
                    }
                printf("\n Result of matrix Multiplicationn:\n");
                for (i = 0; i < m; i++)
                {
                    for (j = 0; j < q; j++)
                    {
                        printf("\t%d", *C[i] + j);
                    }
                    printf("\n");
                }
            }
            break;
        case 3:
            exit(1);
        }
    }
}

// 2. A mathematics teacher has 2 tables of integers and wants to perform basic operations on tables. Due to his busy schedule, he wants to use computer programs to perform this task. Help him to design and implement a C Program  to read two matrices  and perform the following operations. (Note : Use the concept of Array of pointers)
// a.	Addition of two matrices
// b.	Multiply two  matrices

#################################3RD CODE#####################
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define SIZE 5

struct BOOK
{
    int ISBN;
    char title[20];
    char author[20];
    float price;
};

struct stack
{
    struct BOOK b[SIZE];
    int top;
};

void push(struct stack *ps, struct BOOK b1);
struct BOOK pop(struct stack *ps);
void display(struct stack *ps);

void main()
{
    struct stack s;
    struct BOOK b1, r1;
    int choice;
    s.top = -1;
    do
    {
        printf("\n 1:PUSH\t 2:POP\t 3:DISPLAY\t 4:QUIT");
        printf("\n Enter your choice:");
        scanf("%d", &choice);
        switch (choice)
        {
        case 1:
            printf("Enter the ISBN, title, author and price of the book to push:");
            scanf("%d %s %s %f, ", &b1.ISBN, b1.title, b1.author, &b1.price);
            push(&s, b1);
            break;
        case 2:
            r1 = pop(&s);
            printf("The details of BOOK popped is :");
            printf("\n ISBN =%d,  Title=%s, Author=%s, Price=%f", b1.ISBN, b1.title, b1.author, b1.price);
            break;
        case 3:
            display(&s);
            break;
            printf("\n Stack empty");
        case 4:
            printf("\nQuitting operation stack\n");
            break;
        default:
            printf("No such option\n");
            break;
        }
    } while (choice != 4);
}

void push(struct stack *ps, struct BOOK b1)
{
    if (ps->top == SIZE - 1)
        printf("Stack Overflow\n");
    else
    {
        ++(ps->top);
        ps->b[ps->top].ISBN = b1.ISBN;
        strcpy(ps->b[ps->top].title, b1.title);
        strcpy(ps->b[ps->top].author, b1.author);
        ps->b[ps->top].price = b1.price;
    }
}

struct BOOK pop(struct stack *ps)
{
    struct BOOK r;
    if (ps->top == -1)
    {
        printf("\n Stack Underflow");
        exit(1);
    }
    r.ISBN = ps->b[ps->top].ISBN;
    strcpy(r.title, ps->b[ps->top].title);
    strcpy(r.author, ps->b[ps->top].author);
    r.price = ps->b[ps->top].price;
    (ps->top)--;
    return (r);
}

void display(struct stack *ps)
{
    int i;
    if (ps->top == -1)
        printf("\n Stack is empty");
    else
    {
        printf("Stack contents are:\n");
        for (i = ps->top; i >= 0; i--)
        {
            printf("\n ISBN= %d   Title=%s  Author=%s   Price=%f", ps->b[i].ISBN, ps->b[i].title, ps->b[i].author, ps->b[i].price);
        }
    }
}

/*Stack is a simple linear data structure used for storing data which follows the principle of Last In First Out. Assume that you are given the details of BOOK with members ISBN, Title, Author and Price.  Design an interactive C program to construct a stack data structure to store N BOOK items and write C functions to perform the following operations on it:
a) PUSH-To add a new BOOK to the stack
b) POP- To remove a BOOK  from the stack
Also demonstrate Overflow and Underflow conditions on Stack and display the status of Stack.*/

####################4th####################################
#include <stdio.h>

char stack[50];
int top = -1;

/* push() */
void push(char ch)
{
    stack[++top] = ch;
}

/* pop() */
char pop()
{
    if (top == -1)
        return '\0'; // Empty stack
    return (stack[top--]);
}

/* prcd() */
int prcd(char ch)
{
    int p;
    switch (ch)
    {
    case '$':
    case '^':
        p = 3;
        break;
    case '*':
    case '/':
        p = 2;
        break;
    case '+':
    case '-':
        p = 1;
        break;
    case '(':
        p = -1;
        break;
    default:
        p = 0;
        break;
    }
    return p;
}

/* conversion() */
void conversion(char infix[], char postfix[])
{
    int i = 0, p = 0;
    char ch;
    while ((ch = infix[i]) != '\0')
    {
        switch (ch)
        {
        case '(':
            push(ch);
            break;
        case ')':
            while (top != -1 && stack[top] != '(')
                postfix[p++] = pop();
            pop(); /* discard '(' */
            break;
        case '*':
        case '/':
        case '+':
        case '-':
        case '$':
        case '^':
            while (top != -1 && prcd(stack[top]) >= prcd(ch))
                postfix[p++] = pop();
            push(ch);
            break;
        default:
            postfix[p++] = ch;
            break;
        }
        i++;
    }
    while (top != -1)
        postfix[p++] = pop();
    postfix[p] = '\0';
}

int main()
{
    char infix[50], postfix[50];
    printf("Enter a valid infix expression:\n");
    scanf("%s", infix);
    conversion(infix, postfix);
    printf("Postfix expression: %s\n", postfix);
    return 0;
}
#######################5th(1)############
#include <stdio.h>
#include <math.h>
#include <ctype.h>

float eval(char postfix[]);
float oper(char symb, float op1, float op2);
void push(float x);
float pop();

int main()
{
    char postfix[50];
    int choice;
    float res;
    do
    {
        printf("Enter postfix expression: ");
        scanf("%s", postfix);
        res = eval(postfix);
        printf("Result = %f\n", res);
        printf("Do you want to enter another expression? (1/0): ");
        scanf("%d", &choice);
    } while (choice != 0);
    return 0;
}

float eval(char postfix[])
{
    float op1, op2, value;
    char ch;
    int i = 0;
    while ((ch = postfix[i]) != '\0')
    {
        if (isdigit(ch))
            push(ch - '0');
        else
        {
            op2 = pop();
            op1 = pop();
            value = oper(ch, op1, op2);
            push(value);
        }
        i++;
    }
    return pop();
}

float oper(char symb, float op1, float op2)
{
    float result;
    switch (symb)
    {
    case '$':
    case '^':
        result = pow(op1, op2);
        break;
    case '*':
        result = op1 * op2;
        break;
    case '/':
        if (op2 != 0)
            result = op1 / op2;
        else
        {
            printf("Error: Division by zero\n");
            return 0; // Returning 0 for division by zero
        }
        break;
    case '+':
        result = op1 + op2;
        break;
    case '-':
        result = op1 - op2;
        break;
    default:
        printf("Error: Invalid operator\n");
        return 0; // Returning 0 for invalid operator
    }
    return result;
}

float stack[50];
int top = -1;

void push(float x)
{
    stack[++top] = x;
}

float pop()
{
    return stack[top--];
}

/*Design, Develop and Implement a Program in C for the following Stack Applications
a.	Evaluation of postfix expression with single digit operands and operators: +, -, *, /, %, ^ or $
b.	Solving Tower of Hanoi problem with n disks  */
#######################5th(2nd)#####################
#include <stdio.h>

void towers(int n, char source, char destination, char auxiliary);

int main()
{
    int n;
    printf("Enter the number of disks: ");
    scanf("%d", &n);

    if (n < 1)
    {
        printf("Invalid input. Number of disks must be positive.\n");
        return 1; // Returning non-zero to indicate error
    }

    printf("Moves made:\n");
    towers(n, 'A', 'C', 'B');

    return 0; // Indicating successful execution
}

void towers(int n, char source, char destination, char auxiliary)
{
    if (n == 1)
    {
        printf("MOVE DISK 1 FROM PEG %c TO PEG %c\n", source, destination);
        return;
    }

    towers(n - 1, source, auxiliary, destination);
    printf("MOVE DISK %d FROM PEG %c TO PEG %c\n", n, source, destination);
    towers(n - 1, auxiliary, destination, source);
}

#### 6th CODE
/*A Call centre phone system has to hold the phone calls from customers and provide service based on the arrival time of the calls. Design and implement a C program to simulate this system using a Circular queue. Program should have options to add and remove the phone calls in appropriate order for their service. (Array Implementation of Queue with maximum size MAX). Include C functions to perform the following operations.
a.	Add a call
b.	Delete a call 
c.	Display the current status of  calls 
Demonstrate Overflow and Underflow conditions*/

#include <stdio.h>
#include <stdlib.h>

#define MAX 5

struct Queue {
    int front, rear;
    int calls[MAX];
};

void initializeQueue(struct Queue *q) {
    q->front = q->rear = -1;
}

int isFull(struct Queue *q) {
    return (q->front == (q->rear + 1) % MAX);
}

int isEmpty(struct Queue *q) {
    return (q->front == -1);
}

void enqueue(struct Queue *q, int call) {
    if (isFull(q)) {
        printf("Overflow: Queue is full. Cannot add more calls.\n");
    } else {
        if (isEmpty(q)) {
            q->front = q->rear = 0;
        } else {
            q->rear = (q->rear + 1) % MAX;
        }
        q->calls[q->rear] = call;
        printf("Call added successfully.\n");
    }
}

void dequeue(struct Queue *q) {
    if (isEmpty(q)) {
        printf("Underflow: Queue is empty. No calls to remove.\n");
    } else {
        printf("Call %d removed.\n", q->calls[q->front]);
        if (q->front == q->rear) {
            initializeQueue(q);
        } else {
            q->front = (q->front + 1) % MAX;
        }
    }
}

void displayQueue(struct Queue *q) {
    if (isEmpty(q)) {
        printf("Queue is empty.\n");
    } else {
        printf("Current status of calls: ");
        int i = q->front;
        do {
            printf("%d ", q->calls[i]);
            i = (i + 1) % MAX;
        } while (i != (q->rear + 1) % MAX);
        printf("\n");
    }
}

int main() {
    struct Queue callQueue;
    initializeQueue(&callQueue);

    int choice, call;

    do {
        printf("\n----- Call Center Simulation -----\n");
        printf("1. Add a call\n");
        printf("2. Delete a call\n");
        printf("3. Display current status of calls\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter the call number: ");
                scanf("%d", &call);
                enqueue(&callQueue, call);
                break;
            case 2:
                dequeue(&callQueue);
                break;
            case 3:
                displayQueue(&callQueue);
                break;
            case 4:
                printf("Exiting the program.\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }

    } while (choice != 4);

    return 0;
}


##7-----------
/*A music club is interested in creating a song playlist. The facilities to be provided for the users of the playlist are 
a.	Create a playlist
b.	Play a song from starting of the playlist.
c.	Play a song from end of the playlist 
d.	Delete a song from the starting of the playlist
e.	Delete a song from the end of the playlist

Design and Implement a menu driven Program in C for the above operations using Singly Linked List.*/


#include<stdio.h>
#include<stdlib.h>
#include<string.h>
struct node
{
  char song[25];
  struct node *next;
};

typedef struct node *NODEPTR;
NODEPTR list=NULL;


/*getnode()*/
NODEPTR getnode()
{
  NODEPTR r;
  r=(NODEPTR)malloc(sizeof(struct node));
  if(r==NULL)
  {
    printf("Allocation failed\n");
    return;
  }
  return r;
}


//create a list

NODEPTR create(NODEPTR list, char song[])
{
	NODEPTR p,q;
	p=getnode();
	strcpy(p->song,song);
	p->next=NULL;
	if(list==NULL)
		list=p;
	else{
		for(q=list; q->next!=NULL; q=q->next)
		;
		q->next=p;
	}
	return(list);
}

void playbegin(NODEPTR list)
{
 NODEPTR p;
 p=list;
 if(list==NULL)
   printf("Empty playlist");
 else
 printf("\n Playing %s\n",p->song);
}

void playend(NODEPTR list)
{
 NODEPTR p;
 p=list;
 if(list==NULL)
  printf("Empty playlist");
 else {
 while(p->next!=NULL)
    p=p->next;
 printf("\n Playing %s\n",p->song);
}
}

NODEPTR deletebegin(NODEPTR list)
{
	NODEPTR p;
	p=list;
        if(list==NULL)
  		printf("\n Empty playlist");
 	else{
 	printf("\n Song deleted =%s",p->song); 
	list=p->next;
	free(p);
	return(list);
       }
}

NODEPTR deleteend(NODEPTR list)
{
	NODEPTR p,q;
	p=list;
	q=NULL;
	if(list==NULL)
  		printf("Empty playlist");
  	else if(list->next==NULL)	
  	   {
  	     printf("\n Song deleted =%s",p->song); 
      	 list=p->next;
    	 free(p);
    	 return(list); 
  	   }
 	else{
	    while(p->next!=NULL)
	    {
	        q=p;  
            p=p->next;
	    } 
           q->next=p->next;
            printf("\n Song deleted =%s",p->song);
	free(p);
	return(list);
   }
}

void display(NODEPTR list)
{
    NODEPTR p;
    if(list==NULL)
    {
        printf("Empty list");
    }
    else{
    printf("The playlist contains:\n");
    for(p=list;p!=NULL;p=p->next)
       printf("%s->",p->song);
       printf("\n");
    }
}

main()
{
    int choice;
    char cont;
    char song[25];
    do{
    printf("1->CREATE PLAYLIST 2->PLAY FROM BEGINNINNG 3->PLAY FROM END 4->DELETE FROM BEGINNING  5->DELETE FROM END  6->DISPLAY  7->QUIT\n");
    printf("Enter your choice:");
    scanf("%d",&choice);
    switch(choice)
    {
     case 1:  do{
              	  printf("Enter a song:");
              	  scanf("%s",song);
              	  list = create(list,song);
              	  printf("Do you want to enter another song[Y/N]:");
               	 scanf(" %c",&cont);
               }while(cont=='Y' || cont=='y');
               break;

     case 2:   playbegin(list);
               break;

     case 3:   playend(list);
               break;

     case 4:   list=deletebegin(list);
               break;

     case 5:   list=deleteend(list);
               break;     
    
     case 6:   display(list);
               break;
     
     case 7:   exit(1);
     
     default : printf("\nNo such option");
               break;

   }
}while(choice!=7);
}


##8----
/*You are assigned the task to design a browser history where a person can visit any page and go backward or forward in browser history in any number of steps. Suppose we have to go forward x steps, but we can go only y(where y<x) steps forward because of the last Node, then we return the last node. Similarly, we will return the first node while traveling back.

Design and implement a menu driven Program in C to implement the above operations using Doubly Linked List.*/


#include<stdio.h>
#include<stdlib.h>


struct node
{
int page;
struct node *left;
struct node *right;
};


typedef struct node *NODEPTR;
NODEPTR list=NULL;


NODEPTR createlist(NODEPTR list,int page);
NODEPTR moveforward(NODEPTR list, int cp ,int steps);
NODEPTR movebackward(NODEPTR list, int cp, int steps);
void display();
NODEPTR getnode();

NODEPTR createlist(NODEPTR list, int page)
{
	NODEPTR p,q;
	p=getnode();
	p->page=page;
	p->left=NULL;
	p->right=NULL;
	if(list==NULL)
		list=p;
	else{
		for(q=list; q->right!=NULL; q=q->right)
		;
		q->right=p;
		p->left=q;

	}
	return(list);
}

	
NODEPTR moveforward(NODEPTR list, int cp,int steps)
{
	NODEPTR p,q;
 	int count=0,s;
	if(list==NULL)
		printf("\n Empty list");
	else{
		p=list;
                for(p=list,count=0;count<cp-1; count++)
                  p=p->right;
             
                for(q=p,s=0;s<steps;s++)
                 {
                    if(q->right==NULL)
		    	return(q);
		    q=q->right;
 		   }
                 return(q);
}
}

NODEPTR movebackward(NODEPTR list, int cp,int steps)
{
	NODEPTR p,q;
 	int count=0,s;
	if(list==NULL)
		printf("\n Empty list");
	else{
		p=list;
                for(p=list,count=0;count<cp-1; count++)
                  p=p->right;
             
                for(q=p,s=0;s<steps;s++)
                 {
                    if(q->left==NULL)
		            	return(q);
		           q=q->left;
 		   }
                 return(q);
    }
}


void display(NODEPTR list)
{
	NODEPTR p;
	p=list;
	if(p==NULL)
		printf("\nEmpty list");
	else
	{
		printf("\n The page list contains: ");
		for(p=list;p!=NULL;p=p->right) 
		{
			printf("%d<->",p->page);
		}
	}
}

NODEPTR getnode()
{
	NODEPTR r;
	r=(NODEPTR)malloc(sizeof(struct node));
	if(r==NULL)
	{
		printf("\n Node allocation failed");
		exit(0);
	}
	return(r);
}


void main()
{
		int page,choice,steps,cp;
 		char cont;
		NODEPTR p;
		do{
		printf("\n ...........MENU...........");
		printf("\n 1->CREATE LIST\t  2->MOVE FORWARD\t  3->MOVE BACKWARD\t 4->DISPLAY 5->EXIT");
		printf("\n Enter your choice");
		scanf("%d",&choice);
		switch(choice)
		{
		case 1:printf("\n CREATION OF DOUBLY LINKED LIST OF PAGES IS IN PROGRESS:\n");
			do{
              	        	  printf("Enter a page number:");
                        	  scanf("%d",&page);
              	 	 	  list = createlist(list,page);
              	 		  printf("Do you want to enter another page[Y/N]:");
               	 		  scanf(" %c",&cont);
              		 }while(cont=='Y' || cont=='y');
               		  display(list); 
			  break;
		 	
		case 2: printf("\n MOVE FORWARD:\n");
			printf("\nEnter the current page:");
                        scanf("%d",&cp);
			printf("Enter the number of steps to move forward");
			scanf("%d",&steps);
			p=moveforward(list,cp,steps);
			printf("\n Moved forward to  page %d from %dth page",p->page, cp);
			break;
		case 3: printf("\n MOVE BACKWARD:\n");
			printf("\nEnter the current page:");
                        scanf("%d",&cp);
			printf("Enter the number of steps to move backward");
			scanf("%d",&steps);
			p=movebackward(list,cp,steps);
			printf("\n Moved backwards to  page %d from %dth page",p->page, cp);
			break;
		case 4: display(list);
		        break;
		case 5:printf("\n Quitting operation List.....\n");
			break;
		default:printf("\n Invalid choice");
			break;
		}		
	}while(choice!=5);
}

 ##9---

#include<stdio.h>
#include<stdlib.h>
#include<math.h>
struct node
{
             int coef;
             int xexp, yexp, zexp;
             struct node *link;
};
typedef struct node *NODE;

NODE getnode()
{
            NODE x;
            x = (NODE) malloc(sizeof(struct node));
            if(x == NULL)
            {
                        printf("Running out of memory \n");
                        return NULL;
            }
            return x;
}

NODE attach(int coef, int xexp, int yexp, int zexp, NODE head)
{
            NODE temp, cur;
            temp = getnode();
            temp->coef = coef;
            temp->xexp = xexp;
            temp->yexp = yexp;
            temp->zexp = zexp;
            cur = head->link;
            while(cur->link != head)
            {
                        cur = cur->link;
            }
            cur->link = temp;
            temp->link = head;
            return head;
}

NODE read_poly(NODE head)
{
            int i, j, coef, xexp, yexp, zexp, n;
            printf("\nEnter the no of terms in the polynomial: ");
            scanf("%d", &n);
            for(i=1; i<=n; i++)
            {
                        printf("\n\tEnter the %d term: ",i);
                        printf("\n\t\tCoef =  ");
                        scanf("%d", &coef);
                        printf("\n\t\tEnter Pow(x) Pow(y) and Pow(z): ");
                        scanf("%d", &xexp);
                        scanf("%d", &yexp);
                        scanf("%d", &zexp);
                        head = attach(coef, xexp, yexp, zexp, head);
            }
              return head;
}

void display(NODE head)
{
            NODE temp;
            if(head->link == head)
            {
                         printf("\nPolynomial does not exist.");
                         return;
            }
            temp = head->link;

            while(temp != head)
            {
                         printf("%dx^%dy^%dz^%d", temp->coef, temp->xexp, temp->yexp, temp->zexp);
                         temp = temp->link;
                         if(temp != head)
                                    printf(" + ");
            }
}

int poly_evaluate(NODE head)
{
            int x, y, z, sum = 0;
            NODE poly;

            printf("\nEnter the value of x,y and z: ");
            scanf("%d %d %d", &x, &y, &z);

            poly = head->link;
            while(poly != head)
            {
                        sum += poly->coef * pow(x,poly->xexp)* pow(y,poly->yexp) * pow(z,poly->zexp);
                        poly = poly->link;
            }
            return sum;
}
void main()
{
  NODE head;
  int res, ch;
  head =  getnode();     /* For polynomial evalaution */
  head->link=head;
 

  while(1)
  {
        printf("\n~~Menu~~");
        printf("\n1.Represent and Evaluate a Polynomial P(x,y,z)");
        printf("\n2.exit");
        printf("\nEnter your choice:");
        scanf("%d",&ch);
        switch(ch)
        {
            case 1:             printf("\n~~~Polynomial evaluation P(x,y,z)~~\n");
                                    head = read_poly(head);
                                    printf("\nRepresentation of Polynomial for evaluation: \n");
                                    display(head);
                                    res = poly_evaluate(head);
                                    printf("\nResult of polynomial evaluation is : %d \n", res);
                                    break;
                                                                        

            
            case 2:         exit(1);
        }
    }
}


 ##10-----
10. 

Dictionary can be implemented using binary search tree.  A binary search tree is a binary tree such that each node stores a key of a dictionary. Key 'k' of a node is always greater than the keys present in its left sub tree. Similarly, key 'k' of a node is always lesser than the keys present in its right sub tree.
Design, Develop and Implement a menu driven Program in C  to perform the  following operations using  Binary Search Tree (BST).
a.	Create a dictionary of words 
b.	Traverse the dictionary  in Inorder, Preorder and Post Order
c.	Search the dictionary for a given word (KEY) and display the appropriate message

#include<stdio.h>
#include<stdlib.h>
#include<string.h>
struct node
{
char  info[20];
struct node *left;
struct node *right;
};

typedef struct node *NODEPTR;
NODEPTR maketree(char word[]);
NODEPTR createtree(char word[]);
void setleft(NODEPTR p,char word[]);
void setright(NODEPTR p,char word[]);
void intrav(NODEPTR p);
void pretrav(NODEPTR p);
void posttrav(NODEPTR p);
void search(NODEPTR p,char key[]);


void main()
{
	NODEPTR ptree;
	NODEPTR p,q;
	char word[20],key[20];
	int opt,f;
        do{

	printf("\n1->CREATE DICTIONARY  2->TRAVERSE 3->SEARCH  4->EXIT ");
	printf("\nEnter your option:");
	scanf("%d",& opt);
	switch(opt)
	{
	case 1: printf("\nEnter a word :");
	        scanf("%s",word);
	        ptree=maketree(word);
		while(strcmp(word,"END")!=0)
		{
			printf("\nEnter a word(Type END to stop):");
			scanf("%s",word);
			if(strcmp(word,"END")==0)
			break;
			p=q=ptree;
			while((strcmp(word,p->info)!=0)  && q!=NULL)
			{
				p=q;
				if(strcmp(word,p->info)<0)
					q=p->left;
				else
					q=p->right;
			}
		if(strcmp(word,p->info)<0)
			setleft(p,word);
		else if(strcmp(word,p->info)>=0)
			setright(p,word);
		}
		printf("\n DICTIONARY CREATED SUCCESSFULLY");
		break;
	case 2 : printf("\n PREORDER TRAVERSAL OF THE DICTIONARY IS:");
		pretrav(ptree);
                
		printf("\n INORDER TRAVERSAL OF THE DICTIONARY IS:");
		intrav(ptree);
	
		printf("\n POSTORDER TRAVERSAL OF THE DICTIONARY IS:");
		posttrav(ptree);
		break;
	case 3: printf("\n Enter the key to search in the dictionary:");
		scanf("%s",key);
		search(ptree,key);
		//if(f==-1)
		//	printf("\n Key %s is not found in the dictionary");
		//else
		//	printf("\n Key %s is found in the dictionary");
        break;
	case 4: printf("\nEXITING BINARY TREE");
		exit(1);
	}
        }while(opt!=4);

}
NODEPTR maketree(char w[])
{
	NODEPTR t;
	t=(NODEPTR)malloc(sizeof(struct node));
	if(t==NULL)
	{
		printf("\n Node allocation failed");
		exit(0);
	}
		strcpy(t->info,w);
		t->left=NULL;
		t->right=NULL;
		return(t);
}

void setleft(NODEPTR p,char w[])
{
	if(p==NULL)
		printf("Void Insertion");
	else if(p->left!=NULL)
		printf("Invalid Insertion");
	else
		p->left=maketree(w);
}

void setright(NODEPTR p,char w[])
{
	if(p==NULL)
		printf("Void Insertion");
	else if(p->right!=NULL)
		printf("Invalid Insertion");
	else
		p->right=maketree(w);
}

void intrav(NODEPTR tree)
{
	if(tree!=NULL)
	{
		intrav(tree->left);
		printf("%s\t",tree->info);
		intrav(tree->right);
	}
}

void pretrav(NODEPTR tree)
{
	if(tree!=NULL)
	{
		printf("%s\t",tree->info);
		pretrav(tree->left);
		pretrav(tree->right);
	}
}

void posttrav(NODEPTR tree)
{
	if(tree!=NULL)
	{
		posttrav(tree->left);
		posttrav(tree->right);
		printf("%s\t",tree->info);
	}
}

void search(NODEPTR tree,char key[])
{
 NODEPTR p,q;
 p=q=tree;
 while((strcmp(key,p->info)!=0)  && q!=NULL)
   {
	p=q;
	if(strcmp(key,p->info)<0)
		q=p->left;
	else
		q=p->right;
   }
     if(strcmp(key,p->info)==0)
	printf("\n Key %s is found in the dictionary",key);
    else
	printf("\n Key %s is not found in the dictionary",key);
}

 
 
  







 
