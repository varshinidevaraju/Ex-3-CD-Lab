# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# Date:10/10/24
# NAME : Varshini D
# REGISTER NO : 212223230234
# AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
# PROGRAM
```
%{
#include "y.tab.h"
%}

%%

"=" { printf("\n Operator is EQUAL"); return '='; }
"+" { printf("\n Operator is PLUS"); return PLUS; }
"-" { printf("\n Operator is MINUS"); return MINUS; }
"/" { printf("\n Operator is DIVISION"); return DIVISION; }
"*" { printf("\n Operator is MULTIPLICATION"); return MULTIPLICATION; }
[a-zA-Z][a-zA-Z0-9]* { printf("\n Identifier is %s", yytext); return ID; }
. { return yytext[0]; }
\n { /* Ignore newlines */ }

%%

int yywrap() {
    return 1;  // End of input signal
}

%{
#include <stdio.h>
int yylex(void);
void yyerror(const char *s);
%}

%token ID PLUS MINUS MULTIPLICATION DIVISION

%%
statement: ID '=' E {
    printf("\nValid arithmetic expression\n");
    $$ = $3;
}
;

E: E PLUS ID
 | E MINUS ID
 | E MULTIPLICATION ID
 | E DIVISION ID
 | ID
;

%%

extern FILE* yyin;

int main() {
    yyin = stdin;
    do {
        yyparse();
    } while (!feof(yyin));
    return 0;
}

void yyerror(const char *s) {
    fprintf(stderr, "Error: %s\n", s);
}
```
# OUTPUT
![image](https://github.com/user-attachments/assets/0aa3b4a6-1424-4173-b8ba-cf99c1ed0740)

# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
