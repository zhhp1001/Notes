Ideally, with the inline keyword, the compiler pastes the contents of the inlined function at the point where the function is called.

Given:
```C++
void Print(void)
{
  cout << "Hello World!\n";
}

int main(void)
{
  Print();
  return 0;
}
```
The compiler would emit an assembly instruction to call the Print function inside the main function.

When declaring the Print function as inline, the compiler would generate the conceptual main() function below:
```C++
int main(void)
{
  // Substitute content of Print function because it's declared as inline
  cout << "Hello World!\n";

  return 0;
}
```
Remember that the inline keyword is **a suggestion** to the compiler and the compiler can ignore it. The compiler may already inline small functions without using the inline keyword.

Long ago, the inline keyword was used to force compilers to paste code where the function was invoked. This technique was used to eliminate function call overhead. This was in the times when compilers were less intelligent about optimizing.