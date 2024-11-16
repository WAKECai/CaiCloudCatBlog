---
date:
    created: 2024-11-16
    updated: 2024-11-16
readtime: 15
---

下面是一般的语法测试功能

<!-- more -->
# Mkdocs for material 的语法测试

# Part1

Example of an admonition/callout with a title:

!!! not "Title of the callout"

    Lorem ipsum dolor sit amet, consectetur adipisicing elit.
    Nulla et eusimod nulla.
    Curabitur gawgea , taeag.

??? info "Collapsible callout"

    Lorem ipsum dolor sit amet, consectetur adipisicing elit.
    Nulla et eusimod nulla.
    Curabitur gawgea , taeag.


# Part2
An Example of a codeBlock for Python:

```python title="add_numbers.py" linenums="1"
# Function to add two numbers
def add_two_numbers(num1, num2):
    return num1 + num2

# Example usage
result = add_two_numbers(5, 3)
print('The sum is:', result)
```

```js title="concatenate_strings.js" linenums="1" hl_lines="2-4"
// Function to concatenate two strings
function concatenateStrings(str1, str2) {
    return str1 + str2;
}
// Example usage
const result = concatenateStrings("Hell0,", "World!")
console.log("The concenate string is " + result)
```

# Part3

## Content Tabs
### Generic Content

=== "Plain text"

    This is some plain text

=== "Unordered list"

    * First item 
    * Second item
    * Third item 

=== "Ordered list"

    1. First item
    2. Second item 
    3. Third item

### Code Blocks in Content Tabs

=== "Python"

    ```py
    def main():
        print("Hello world!")

    if __name__ == "__main__":
        main()
    ```

=== "JavaScript"

    ```java
    function main() {
        console.log("Hello world!")
    }

    main();
    ```
# Part4 Diagram Example

## Flowcharts

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;

```

## Sequence Diagrams

```mermaid
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop HealthCheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/>prevail!
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
```