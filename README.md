EXP2 program on count number


Program:
/*lex program to count number of words*/
%{
#include<stdio.h>
#include<string.h>
int i = 0;
%}
/* Rules Section*/
%%
([a-zA-Z0-9])* {i++;} /* Rule for counting number of words*/

"\n" {printf("%d\n", i); i = 0;}
%%
int yywrap(void){}
int main()
{
// The function that starts the analysis
yylex();
return 0;
}

Commands: flex hello.l
          gcc lex.yy.c
          a.exe


EXP3

hello.l
%{
#include "y.tab.h"
int yyerror(char *errormsg);
%}
%%
("hi"|"oi")"\n" {return HI;}
("tchua"|"bye")"\n" {return BYE;}
. {yyerror("Unknown char"); }
%%

int yywrap(void)
{ return 1;
}


hello.y
%{
#include <stdio.h>
#include <stdlib.h>
int yylex(void);
int yyerror(const char *s);
%}
%token HI BYE
%%
program:
hi bye
;
hi:
HI { printf("Hello World\n"); }
;
bye:
BYE { printf("Bye World\n"); exit(0); }
;

%%
int main(void) {
yyparse();
return 0;
}
int yyerror(const char *s) {
fprintf(stderr, "%s\n", s);
return 1;
}

commands: flex hello.l
          bison -dy hello.y
          gcc lex.yy.c y.tab.c
          a.exe

EXP 4

input.txt:
COPY    START   1000
FIRST   LDA     ALPHA
        STA     BETA
ALPHA   WORD    5
BETA    RESW    1
        END     FIRST

optab.txt:
LDA 3
STA 3

Code:
#include<stdio.h>
#include<string.h>
void main()
{
FILE *f1,*f2,*f3,*f4;
int lc,sa,l,op1,o,len;
char m1[20],la[20],op[20],otp[20];
f1=fopen("input.txt","r");
f3=fopen("symtab.txt","w");
fscanf(f1,"%s%s%d",la,m1,&op1);
if(strcmp(m1,"START")==0)
{
sa=op1;
lc=sa;
printf("\t%s\t%s\t%d\n",la,m1,op1);
}
else
{
lc=0;

}
fscanf(f1,"%s%s",la,m1);
while(!feof(f1))
{
fscanf(f1,"%s",op);
printf("\n%d\t%s\t%s\n",lc,la,m1,op);
if(strcmp(la,"-")!=0)
{
fprintf(f3,"\n%d\t%s\n",lc,la);
}
f2=fopen("optab.txt","r");
fscanf(f2,"%s%d",otp,&o);
while(!feof(f2))
{
if(strcmp(m1,otp)==0)
{
lc=lc+3;
break;
}
fscanf(f2,"%s%d",otp,&o);
}
fclose(f2);
if(strcmp(m1,"WORD")==0)
{
lc=lc+3;
}
else if(strcmp(m1,"RESW")==0)
{
op1=atoi(op);
lc=lc+(3*op1);
}
else if(strcmp(m1,"BYTE")==0)
{
if(op[0]=='X')
{
lc=lc+1;
}
else
{
len=strlen(op)-2;
lc=lc+len;
}
}
else if(strcmp(m1,"RESB")==0)
{
op1=atoi(op);
lc=lc+op1;

}
fscanf(f1,"%s%s",la,m1);
}
if(strcmp(m1,"END")==0)
{
printf("program length=\n%d",lc-sa);
}
fclose(f1);
fclose(f3);
}                                                                                                                                                   Input.txt 

COPY    START   1000
FIRST   LDA     ALPHA
        STA     BETA
ALPHA   WORD    5
BETA    RESW    1
        END     FIRST


Optab.txt

LDA 3
STA 3

commands: gcc assembler.c -o assembler.exe
          assembler.exe

EXP 5

Code:
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
void main()
{
FILE *f1,*f2,*f3,*f4; 
char ch[100],chp[100];
int addr=1000;
f1=fopen("input1.txt","r");
f2=fopen("optab1.txt","r");
f3=fopen("littab2.txt","w");
f4=fopen("symtab2.txt","w");
while (fscanf(f1,"%s",ch) !=EOF)
{
if(strcmp(ch,"-")==0)
{
addr++;

}
if(strcmp(ch,"db")==0)
{
fprintf(f4,"%s\t%d\n",chp,addr);
}
if(strcmp(chp,"LTORG")==0)
{
fprintf(f3,"%s\t%d\n",ch,addr);
}
strcpy(chp,ch);
}
fclose(f4);
fclose(f3);
fclose(f2);
fclose(f1);
}
