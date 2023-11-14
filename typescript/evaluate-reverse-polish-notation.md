
  # evaluate-reverse-polish-notation

  ```typescript
  function evalRPN(tokens: string[]): number {
  const stack: number[] = [];

  for (const token of tokens) {
    if (isOperator(token)) {
      const operand2 = stack.pop()!;
      const operand1 = stack.pop()!;
      const result = evaluateExpression(operand1, operand2, token);
      stack.push(result);
    } else {
      stack.push(parseInt(token));
    }
  }

  return stack.pop()!;
}

function isOperator(token: string): boolean {
  return token === "+" || token === "-" || token === "*" || token === "/";
}

function evaluateExpression(operand1: number, operand2: number, operator: string): number {
  switch (operator) {
    case "+":
      return operand1 + operand2;
    case "-":
      return operand1 - operand2;
    case "*":
      return operand1 * operand2;
    case "/":
      return Math.trunc(operand1 / operand2);
    default:
      throw new Error("Invalid operator");
  }
}

  ```
  