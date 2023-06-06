#include<stdio.h>
#include<stdlib.h>
struct node
{
    int data;
    struct node *left;
    struct node *right;
    
    
};
struct node *root=NULL,*ptr;
struct node *createnode(int item)
{
    struct node *newn=(struct node*)malloc(sizeof(struct node));
    if(newn==NULL)
    {
        printf("\n No memory");
        return NULL;
        
    }
    else
    {
        newn->data=item;
        newn->left=NULL;
        newn->right=NULL;
        
    }
    return newn;
}
struct node* insert(struct node *tnode,int item)
{
    if(tnode==NULL)
    return createnode(item);
    if(item<tnode->data)
    tnode->left=insert(tnode->left,item);
    else
    tnode->right=insert(tnode->right,item);
    return tnode;
    
}
struct node *minvaluenode(struct node *node)
{
    struct node *current=node;
    while(current && current ->left!=NULL)
    current=current->left;
    return current;
}
struct node *deletenode(struct node *root , int val)
{
    if (root ==NULL)
    return root;
    if(val<root->data)
    root->left=deletenode(root->left,val);
    else if(val>root->data)
    root->right=deletenode(root->right,val);
    else
    {
        if(root->left==NULL)
        {
        
            struct node *temp=root->right;
            free(root);
            return temp;
        }
            
        else if(root->right==NULL)
        {
            struct node *temp=root->left;
            free(root);
            return temp;
        }
        struct node *temp=minvaluenode(root->right);
        root->data=temp->data;
        root->right=deletenode(root->right,temp->data);
        
        
    }
    return root;
}
void inorder(struct node *root)
{
    if(root!=NULL)
    {
        inorder(root->left);
        printf("%3d->",root->data);
        inorder(root->right);
    }
}
void preorder(struct node *root)
{
    if(root!=NULL)
    {
        printf("%3d->",root->data);
        preorder(root->left);
        preorder(root->right);
    }
}
void postorder(struct node *root)
{
    if(root!=NULL)
    {
        postorder(root->left);
        postorder(root->right);
        printf("%3d->",root->data);
    }
}
int main()
{
    int ch ,val;
    printf("\n1.insert");
    printf("\n2.delete");
    printf("\n3.inorder");
    printf("\n4.post order");
    printf("\n5.pre order");
    printf("\n6.exit");
    while(1)
    {
        printf("\n enter ur choice :");
        scanf("%d",&ch);
        switch(ch)
        {
            case 1:printf("\n enter an element to insert :");
                    scanf("%d",&val);
                    root=insert(root,val);
                    break;
            case 2:printf("\n enter an element to delete:");
                    scanf("%d",&val);
                    root=deletenode(root,val);
                    break;
            case 3:printf("\ninorder traversal :");
                    inorder(root);
                    break;
            case 4:printf("\npostorder traversal :");
                    postorder(root);
                    break;
            case 5:printf("\npreorder traversal :");
                    preorder(root);
                    break;
            case 6:exit;
        }
    }
}
