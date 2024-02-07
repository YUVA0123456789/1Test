####6th Code

/*A Call centre phone system has to hold the phone calls from customers and provide service based on the arrival time of the calls. Design and implement a C program to simulate this system using a Circular queue. Program should have options to add and remove the phone calls in appropriate order for their service. (Array Implementation of Queue with maximum size MAX). Include C functions to perform the following operations.
a.	Add a call
b.	Delete a call 
c.	Display the current status of  calls 
Demonstrate Overflow and Underflow conditions .*/

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





 #### 7th CODE

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
    return NULL;
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

int main()
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
   return 0; // Add a return statement at the end of main
}





#### 8th CODE

You are assigned the task to design a browser history where a person can visit any page and go backward or forward in browser history in any number of steps. Suppose we have to go forward x steps, but we can go only y(where y<x) steps forward because of the last Node, then we return the last node. Similarly, we will return the first node while traveling back.

Design and implement a menu driven Program in C to implement the above operations using Doubly Linked List.


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
                return q;
            q=q->right;
        }
        return q;
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
                return q;
            q=q->left;
        }
        return q;
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
        printf("\nThe page list contains: ");
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

int main()
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
        case 1:
            printf("\n CREATION OF DOUBLY LINKED LIST OF PAGES IS IN PROGRESS:\n");
            do{
                printf("Enter a page number:");
                scanf("%d",&page);
                list = createlist(list,page);
                printf("Do you want to enter another page[Y/N]:");
                scanf(" %c",&cont);
            } while(cont=='Y' || cont=='y');
            display(list);
            break;
        case 2:
            printf("\n MOVE FORWARD:\n");
            printf("\nEnter the current page:");
            scanf("%d",&cp);
            printf("Enter the number of steps to move forward");
            scanf("%d",&steps);
            p=moveforward(list,cp,steps);
            printf("\n Moved forward to  page %d from %dth page",p->page, cp);
            break;
        case 3:
            printf("\n MOVE BACKWARD:\n");
            printf("\nEnter the current page:");
            scanf("%d",&cp);
            printf("Enter the number of steps to move backward");
            scanf("%d",&steps);
            p=movebackward(list,cp,steps);
            printf("\n Moved backwards to  page %d from %dth page",p->page, cp);
            break;
        case 4:
            display(list);
            break;
        case 5:
            printf("\n Quitting operation List.....\n");
            break;
        default:
            printf("\n Invalid choice");
            break;
        }		
    } while(choice!=5);
    return 0;
}





#### 9th CODE

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
        printf("\n~Menu~");
        printf("\n1.Represent and Evaluate a Polynomial P(x,y,z)");
        printf("\n2.exit");
        printf("\nEnter your choice:");
        scanf("%d",&ch);
        switch(ch)
        {
            case 1:             printf("\n~Polynomial evaluation P(x,y,z)~\n");
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





#### 10th CODE

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
