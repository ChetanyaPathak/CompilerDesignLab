%{
/* LEX program to convert uppercase to
   lowercase except inside comments
*/
#include <stdio.h>
#include <stdlib.h>

%}
%option noyywrap
%%
[A-Z] {
 putchar(tolower(yytext[0]));
}
"/*" {
 char c;
 int endOfComment = 0;
 ECHO;
 do {
  while ((c = input()) != '*')
   putchar(c);
  putchar(c);
  while ((c = input()) == '*')
   putchar(c);
  putchar(c);
  if (c == '/') endOfComment = 1;
 } while (!endOfComment);
}
%%
int main() 
{ 
 yyin=fopen("Check.c","r");
 yylex(); 
 return 0; 
}
