
  # to-be-or-not-to-be

  ```typescript
  type ToBeOrNotToBe = {
    toBe: (val: any) => boolean;
    notToBe: (val: any) => boolean;
};

function expect(val: any): ToBeOrNotToBe {
    return {
        toBe: (expected: any) => {
        if (val !== expected) {
            throw new Error("Not Equal");
        }
        return true;
        },
        notToBe: (unexpected: any) => {
        if (val === unexpected) {
            throw new Error("Equal");
        }
        return true;
        }
    };
}

/**
 * expect(5).toBe(5); // true
 * expect(5).notToBe(5); // throws "Equal"
 */
  ```
  