# Ex. No : 11	
# IMPLEMENTATION OF CALCULATOR USING LEX AND YACC 
## Register Number : 212222110038
## Date : 18.04.2024

## AIM   
To implement a calculator using LEX and YACC.

## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the various mathematical functions.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an expression as input and it is evaluated and the answer is displayed as output.

## PROGRAM
exp11.l
```
%{ 
/* Definition section */
#include<stdlib.h>
#include "y.tab.h"
extern int yylval;
%} 

/* Rule Section */
%% 
[0-9]+ { 
		yylval=atoi(yytext); 
		return NUMBER; 

	} 
'<=' return LE;
'>=' return GE;
'!=' return NE;
'==' return EQ;
[\t] ; 
[\n] return 0; 

. return yytext[0]; 
%% 

```
exp11.y
```
%{ 
   /* Definition section */
  #include<stdio.h> 
  int flag=0; 
%} 
  
%token NAME NUMBER 

%left GE LE EQ NE EE '<' '>'

%left '+' '-'
  
%left '*' '/' '%'
  
%left '(' ')'

%nonassoc UMINUS
/* Rule Section */
%% 
  
ArithmeticExpression: E{ 
  
         printf("Result=%d", $$); 
  
         return 0; 
  
        }; 
 E:E '+' E {$$=$1+$3;} 
  
 |E '-' E {$$=$1-$3;} 
  
 |E '*' E {$$=$1*$3;} 
  
 |E '/' E {$$=$1/$3;} 
  
 |E '%' E {$$=$1%$3;} 
  
 |'(' E ')' {$$=$2;} 
  
 | NUMBER {$$=$1;} 

 |E GE E {$$=$1 >= $3 ;} 

 |E LE E {$$=$1 <= $3 ;}

 |E NE E {$$=$1 != $3 ;} 
 
 |E EE E {$$=$1 == $3 ;} 

 |UMINUS E {$$=-$1 ;}
 ; 
  
%% 
  
//driver code 
int main() 
{ 
   //printf("\nEnter the Expression:\n"); 
   yyparse(); 
   //if(flag==0) 
   //printf("\nEntered arithmetic expression is Valid\n\n"); 
//    return 0;
} 
  
int yyerror() 
{ 
//    printf("\nEntered arithmetic expression is Invalid\n\n"); 
//    flag=1; 
} 
int yywrap(){
    return 1;
}
```

## OUTPUT 
![image](https://github.com/KISHOREM04/19CS409-Compiler-Design-Lab/assets/119404643/06a292d4-2126-4628-bd1a-51e03c173802)

## RESULT
The calculator is implemented using LEX and YACC and the output is verified.
