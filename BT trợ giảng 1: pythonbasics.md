- link bt: https://tryhackme.com/room/pythonbasics<br>

*. task 2<br>
1. On the code editor, print "Hello World". What is the flag?<br>
```
print("Hello World")
```
As: THM{PRINT_STATEMENTS}<br>

*. task 3<br>
1. In the code editor, print the result of 21 + 43. What is the flag?<br>
```
print(21+43)
```
As: THM{ADDITI0N}<br>

2. Print the result of 142 - 52. What is the flag?<br>
```
print(142-52)
```
As: THM{SUBTRCT}<br>

3. Print the result of 10 * 342. What is the flag?<br>
```
print(10*342)
```
As: THM{MULTIPLICATION_PYTHON}<br>

4. Print the result of 5 squared. What is the flag?<br>
```
print(5**2)
```
As: THM{EXP0N3NT_POWER}<br>

*. task 4<br>
1. On another new line, print out the value of height. What is the flag that appears?<br>
```
height = 200
height += 50
print(height)
```
As: THM{VARIABL3S}<br>

*. task 6<br>
1. Once you've written the application in the code editor's shipping.py tab, a flag will appear, which is the answer to this question.
```
customer_basket_cost = 34
customer_basket_weight = 44

# Write if statement here to calculate the total cost
if customer_basket_cost > 100:
  total = customer_basket_cost
else:
  total = customer_basket_cost + customer_basket_weight * 1.2
print(total)
```
As: THM{IF_STATEMENT_SHOPPING}<br>

2. In shipping.py, on line 12 (when using the Code Editor's Hint), change the customer_basket_cost variable to 101 and re-run your code. You will get a flag (if the total cost is correct based on your code); the flag is the answer to this question.<br>
```
customer_basket_cost = 101
customer_basket_weight = 44

# Write if statement here to calculate the total cost
if customer_basket_cost > 100:
  total = customer_basket_cost
else:
  total = customer_basket_cost + customer_basket_weight * 1.2
print(total)
```
As:  THM{MY_FIRST_APP}<br>

*. task 7<br>
1. On the code editor, click back on the "script.py" tab and code a loop that outputs every number from 0 to 50.<br>
```
# Write your python code here
for i in range(51):
  print(i)
```
As: THM{L00PS_WHILE_FOR}<br>

*. task 8<br>
1. Once you've written the bitcoinToUSD function, use it to calculate the value of your Bitcoin in USD, and then create an if statement to determine if the value falls below $30,000; if it does, output a message to alert you (via a print statement).<br>
```
investment_in_bitcoin = 1.2
bitcoin_to_usd = 40000

# 1) write a function to calculate bitcoin to usd
def bitcoinToUSD(bitcoin_amount, bitcoin_value_usd):
  return bitcoin_amount * bitcoin_value_usd
# 2) use function to calculate if the investment is below $30,000
t = bitcoinToUSD(investment_in_bitcoin, bitcoin_to_usd)
print(t)
if t < 30000:
  print("thua roi")
```
As: THM{BITC0IN_INVESTOR}<br>

*. task 9<br>
1. In the code editor, write Python code to read the flag.txt file. What is the flag in this file?<br>
```
f = open("flag.txt", "r")
print(f.read())
```
As: THM{F1LE_R3AD}
