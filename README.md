# language_guesser_code
This code guesses whether the text you have entered is in English or German.

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <string.h>
typedef struct node
{ void* dataPtr;
 struct node* link;
 } STACK_NODE;
 typedef struct {
     int count;
     STACK_NODE* top;
} STACK;

STACK* createStack (void){
    //Local Definitions
    STACK* stack;//Statements
    stack = (STACK*) malloc( sizeof (STACK));
    if (stack) {
        stack->count = 0;
        stack->top = NULL;
        }// if
        return stack;}




        bool pushStack (STACK* stack, void* dataInPtr){
            //Local Definitions
            STACK_NODE* newPtr;//Statements
            newPtr = (STACK_NODE* ) malloc(sizeof( STACK_NODE));
            if (!newPtr)
            return false;
            newPtr->dataPtr = dataInPtr;
            newPtr->link = stack->top;
            stack->top = newPtr;
            (stack->count)++;
            return true;

            }

            void* stackTop (STACK* stack){//Statements
                if (stack->count == 0)
                    return NULL;
                else return stack->top->dataPtr;
                }
void* popStack (STACK* stack){//Local Definitions
    void* dataOutPtr;
    STACK_NODE* temp;//Statements
    if (stack->count == 0)
        dataOutPtr = NULL;
    else {
        temp = stack->top;
        dataOutPtr = stack->top->dataPtr;
        stack->top = stack->top->link;
        free (temp);
        (stack->count)--;
        }// else

    return dataOutPtr;}

bool emptyStack (STACK* stack){
     //Statements
     return (stack->count == 0);
     }


 bool balanced(const char p[], int size) {
    STACK* stack;

    stack = createStack();
    for(int i = 0; i < size; i++) {

                if(p[i] == '(' || p[i] == '{') {
                char* kar;
                kar = (char*)malloc(sizeof(char));
                *kar = p[i];
                pushStack(stack, kar);

               }
            else if(p[i] == ')') {
                char* kar1;
                if(stack->count != 0) {
                    kar1 = (char*)popStack(stack);        //   () ({}) (()))
                    if(*kar1 != '(')
                    return false;

                }
                else
                    return false;

            }
            else if (p[i] == '}'){
                char* kar2;
                if(stack->count != 0) {
                kar2 = (char*)popStack(stack);
                if(*kar2 != '{')
                    return false;

                }
                else
                    return false;


            }

            else
                return false;







        }
        if(stack->count == 0)
            return true;
        else
            return false;


    }





int main()
{
    const char p[50];
    printf("metni gir: \n");
    scanf("%s", p);

   bool  aa;

    aa = balanced(p, strlen(p));
    printf("%d", aa);

}
