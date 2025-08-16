#include<stdio.h>
#include<stdlib.h>
struct node
{
    int data;
    struct node *next;
};

struct node* createnode(int value,struct node** start)
{
    struct node* newnode=(struct node*)malloc(sizeof(struct node));
    newnode->data=value;
    newnode->next=NULL;
    return newnode;
}
void insertatfirst(int value,struct node** start)
{
    struct node* newnode=createnode(value,start);
    newnode->next=start;
    start=newnode;
}
void insertatlast(int value,struct node** start)
{
    struct node* newnode=createnode(value,start);
    if(start==NULL)
    {
        start=newnode;
        return;
    }
    
        struct node* temp=start;
        while(temp->next!=NULL)
        {
            temp=temp->next;
        }
        temp->next=newnode;
    
    
}


void insertatposition(int value,int position,struct node** start)
{
    struct node* newnode=createnode(value,*start);
    if(position==1)
    {
        newnode->next=*start;
        *start=newnode;
        return;
    }
     newnode=createnode(value,*start);
    struct node* temp=start;
    for(int i=1;temp!=NULL&&i<position-1;i++)
    {
        temp=temp->next;
    }
    if(temp==NULL)
    {
        printf("invalid position");
        free(newnode);
    }
    else
    {
        newnode->next=temp->next;
        temp->next=newnode;
    }
}
void deleteatfirst(struct node** start)
{
    if(start==NULL)
    {
        printf("list is empty");
        return;
    }
    struct node* temp=*start;
    *start=temp->next;
    free(temp);
}
void deleteatlast(struct node** start)
{
    if(*start==NULL)
    {
        printf("list is empty");
        return;
    }
    struct node* temp=start;
    while(temp->next->next!=NULL)
    {
        temp=temp->next;
    }
    free(temp->next);
    temp->next=NULL;
}
void deleteatposition(int position,struct node** start)
{
    if(*start==NULL)
    {
        printf("list is empty");
        return;
    }
    if(position==1)
    {
        deleteatfirst(*start);
        return;
    }
    struct node* temp=*start;
    for(int i=1;temp!=NULL&&i<position-1;i++)
    {
        temp=temp->next;
    }
    if(temp==NULL||temp->next==NULL)
    {
        printf("invalid position");
        return;
    }
    struct node* todelete=temp->next;
    temp->next=todelete->next;
    free(todelete);
}
void display(struct node** start)
{
    struct node* temp=*start;
    if(*start==NULL)
    {
        printf("list is empty");
        return;
    }
    while(temp!=NULL)
    {
        printf("%d->",temp->data);
        temp=temp->next;
    }
    printf("NULL");
    printf("\n");
}
int main()
{
    struct node* start=NULL;
    int choice,value,position;
    while(1)
    {
        printf("1.insert at first\n");
        printf("2.insert at last\n");
        printf("3.insert at position\n");
        printf("4.delete at first\n");
        printf("5.delete at last\n");
        printf("6.delete at position\n");
        printf("7.display\n");
        printf("8.exit\n"); 
        printf("enter your choice");
        scanf("%d",&choice);
        switch(choice)
        {
            case 1:
                printf("enter the value to insert at first");
                scanf("%d",&value);
                insertatfirst(value,&start);
                break;
            case 2:
                printf("enter the value to insert at last");
                scanf("%d",&value);
                insertatlast(value,&start);
                break;
            case 3:
                printf("enter the value to insert at position");   
                scanf("%d",&value);
                printf("enter the position to insert at");
                scanf("%d",&position);
                insertatposition(value,position,&start);
                break;
            case 4:
                deleteatfirst(&start    );
                break;
            case 5:
                deleteatlast(&start);
                break;
            case 6:
                printf("enter the position to delete at");
                scanf("%d",&position);
                deleteatposition(position,&start);
                break;
            case 7:
                display(&start);
                break;
            case 8:
                exit(0);
            default:
                printf("invalid choice");
        }
    }
    return 0;
}
