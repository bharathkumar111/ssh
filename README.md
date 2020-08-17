Design a compiler (Lexical  and Parser phase) for the given           hypothetical languages.


                     var=Data_Type(input("String "))
                      if (boolean_cond):
                               print("string", var)
                       else:
                              var=num

    LEXICAL PROGRAM FOR THE ABOVE PROBLEM STATEMENT
 
#include<stdio.h>
#include<ctype.h>
#include<string.h>
void keyw(char *p);
int i=0,id=0,kw=0,num=0,op=0;
char keys[5][10]= {"Data_Type","input",
                   "if","print","else"
                  };
int main()
{
    char ch,str[25],seps[15]=" \t\n,;(){}[]#\"<>",oper[]="!%^&*-+=~|.<>/?";
    int j;
    char fname[50];
    FILE *f1;
    //clrscr();

    f1 = fopen("C:\\Users\\hp\\Desktop\\jj7.txt","r");
    //f1 = fopen("C:\\Users\\surak\\Desktop\\Complier design project\\lex part final\\input.txt","r");
    if(f1==NULL)
    {
        printf("file not found");
        exit(0);
    }
    while((ch=fgetc(f1))!=EOF)
    {
        for(j=0; j<=14; j++)
        {
            if(ch==oper[j])
            {
                printf("%c is an operator\n",ch);
                op++;
                str[i]='\0';
                keyw(str);
            }
        }
        for(j=0; j<=14; j++)
        {
            if(i==-1)
                break;
            if(ch==seps[j])
            {
                str[i]='\0';
                keyw(str);
            }
        }
        if(i!=-1)
        {
            str[i]=ch;
            i++;
        }
        else
            i=0;
    }
    printf("Keywords: %d\nIdentifiers: %d\nOperators: %d\nNumbers: %d\n",kw,id,op,num);
    //getch();
}
void keyw(char *p)
{
    int k,flag=0;
    for(k=0; k<=4; k++)
    {
        if(strcmp(keys[k],p)==0)
        {
            printf("%s is a keyword\n",p);
            kw++;
            flag=1;
            break;
        }
    }
    if(flag==0)
    {
        if(isdigit(p[0]))
        {
            printf("%s is a number\n",p);
            num++;
        }
        else
        {
            //if(p[0]!=13&&p[0]!=10)
            if(p[0]!='\0')
            {
                printf("%s is an identifier\n",p);
                id++;
            }
        }
    }
    i=-1;
}
