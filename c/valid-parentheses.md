
  # valid-parentheses

  ```c
  // Define a structure for the stack
typedef struct {
    char data[10000];
    int top;
} Stack;

// Initialize the stack
void initialize(Stack* stack) {
    stack->top = -1;
}

// Push an element onto the stack
void push(Stack* stack, char element) {
    stack->data[++stack->top] = element;
}

// Pop an element from the stack
char pop(Stack* stack) {
    return stack->data[stack->top--];
}

// Check if the stack is empty
bool isEmpty(Stack* stack) {
    return stack->top == -1;
}

// Function to check if the input string is valid
bool isValid(char* s) {
    int len = strlen(s);
    Stack stack;
    initialize(&stack);

    for (int i = 0; i < len; i++) {
        char current = s[i];

        if (current == '(' || current == '[' || current == '{') {
            push(&stack, current);
        } else {
            if (isEmpty(&stack)) {
                return false;
            }

            char top = pop(&stack);

            if ((current == ')' && top != '(') ||
                (current == ']' && top != '[') ||
                (current == '}' && top != '{')) {
                return false;
            }
        }
    }

    return isEmpty(&stack);
}
  ```
  