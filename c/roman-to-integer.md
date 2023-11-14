
  # roman-to-integer

  ```c
  int romanToInt(char *s) {
    int romanValue = 0;
    int prevValue = 0;

    for (int i = 0; s[i] != '\0'; i++) {
        int currentValue = 0;

        switch (s[i]) {
            case 'I':
                currentValue = 1;
                break;
            case 'V':
                currentValue = 5;
                break;
            case 'X':
                currentValue = 10;
                break;
            case 'L':
                currentValue = 50;
                break;
            case 'C':
                currentValue = 100;
                break;
            case 'D':
                currentValue = 500;
                break;
            case 'M':
                currentValue = 1000;
                break;
        }

        romanValue += currentValue;

        if (currentValue > prevValue) {
            romanValue -= 2 * prevValue;
        }

        prevValue = currentValue;
    }

    return romanValue;
}

  ```
  