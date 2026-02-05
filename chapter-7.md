# Solidity variables and functions, Part 1

### Why should you care about learning Solidity? <a href="#why-should-you-care-about-learning-solidity" id="why-should-you-care-about-learning-solidity"></a>

You already understand how blockchain works through Bitcoin and Ethereum. Solidity takes you a step further – from understanding blockchain to creating with it. There are other benefits too, which are described below.

* You shift from understanding “how blockchain works” to “shaping what it can do.” Bitcoin taught you trustless value transfer. Solidity lets you design trustless systems – automated payments, supply-chain tracking, tokenized assets, and decentralized marketplaces.
* You shift from being a consumer to becoming a creator. Instead of describing how blockchain could improve business processes, you will build and test your own logic for how it does – through smart contracts that enforce agreements automatically.
* You are able to understand the real engines of DeFi and tokenized economies. DeFi platforms, NFTs, and novel governance mechanisms that run on code (these are called DAOs or decentralized autonomous organizations) all run on Solidity. Learning it helps you understand how these systems operate.
* You build skills for digital leadership. Even if you never become a developer, knowing Solidity helps you:
  * Communicate effectively with technical teams.
  * Assess the cost and feasibility of blockchain projects.
  * Contribute credibly to innovation, fintech, and product-management roles.
* You will prepare yourself to meet a growing market demand. Solidity developers are among the most sought-after professionals in the blockchain space, with salaries that often exceed those of general software engineers. By understanding Solidity – even at a conceptual level – you can evaluate and lead projects that rely on smart contracts. The combination of your business knowledge and technical fluency positions you to bridge the gap between strategic vision and technical execution.

In short, Solidity turns your knowledge of blockchain from conceptual to actionable. It is how business ideas become programmable realities.

We will begin our journey into Solidity by first focusing on variables in Solidity and then move on to creating functions.

### Variables in Solidity <a href="#variables-in-solidity" id="variables-in-solidity"></a>

Solidity allows one to use different types of variables -- integers, strings, booleans, arrays, structs, mapping, etc. Rather than providing you with an exhaustive list of the types of variables and providing definitions or descriptions that may prove to be abstract, we will begin by writing programs and introduce the different types of variables to you as and when they are needed. This way, their introduction will be contextualized within the reason for introducing them and, therefore, more meaningful to you.

There is one thing that you should know though. Unlike in something like Excel where we simply type away values for variables such as ‘Sales’ or ‘Student Name’ without having to specify them as a number or a string, we have to declare the type of the variable in Solidity.

Let us first introduce variables that are of the ‘integer’ type. We will shift out of the introduction of this type of variables to introduce other notions about Solidity and then introduce new types as and when needed.

### Integers in Solidity <a href="#integers-in-solidity" id="integers-in-solidity"></a>

Typically, we tend to employ the following ways to declare integers.

* By using 'int' for integers that can be positive, negative, or zero.
* By using 'uint' for integers that can be positive or zero.

Type the following and compile.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

   //Integers
   
   uint sales; //sales in wei  
    
   uint expenses; //expenses in wei  
    
   int profits; //profits in wei; it is in int because it can be negative  

}
```

You will see that the compilation is successful. Which means that our specification of the type for different variables is fine.

Go ahead and deploy the contract. To deploy, carry out the following steps.

* Click on the deploy icon on the left. Use Remix VM (Prague) under Environment (this is the default setting – just accept it). This simulates an Ethereum virtual machine on your computer (actually, within your browser).
* Click on the orange ‘Deploy’ button in the middle of the window on the left.
* You will see the contract under 'Deployed Contracts'. Click on the arrow to the left of the name of the contract.
* You will see the interface to the contract. At this point, you see nothing except that the balance for this contract is 0 ETH.

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

* We don’t see anything about profits, which is what we are trying to compute. That is not surprising. We have not entered any values for sales or expenses. Nor have we entered any formula for computing profits. Let us first assign values to sales and expenses.
* Delete the deployed contract. Click on x to the right of the deployed contract. Or click on the icon for trash. This clears everything for us to let us start again on a clean slate.

Incidentally, when we use int and uint, we are actually saying int256 – or an integer represented by 256 bits – and uint256 – or an unsigned integer represented by 256 bits.

* If this indirectly suggests to you that there are the following types of variables, then you are right:
  * int8, int16, int24, int32, and so on
    * int8 takes values from (-2^7) to (2^7 - 1) or -128 to 127
    * int16 takes values from (-2^15) to (2^15 - 1) or -256 to 255
    * int32 takes values from (-2^31) to (2^31 - 1) or -2147483648 to 2147483647
    * and so on
  * uint8, uint16, uint24, uint32, and so on
    * uint8 takes values from 0 to (2^8 - 1) or 0 to 255
    * uint16 takes values from 0 to (2^16 - 1) or 0 to 65535
    * uint32 takes values from 0 to (2^32 - 1) or 0 to 4294967295
    * and so on

If we don’t put a number at the end of int or uint, then it means int256 or uint256 (which ranges from 0 to 1.1579209e+77). That is the default.

* int256 ranges from -2^255 to 2^255 - 1 or -5.7896045e+76 to 5.7896045e+76 – the latter two are not very precise but give you an indication of the size
* uint256 ranges from 0 to 2^256 - 1 or 0 to 1.1579209e+77 – the latter is not very precise but gives you an indication of the size

While the differences are minimal, using larger numbers will generally cost more gas.

### Assigning values to variables <a href="#assigning-values-to-variables" id="assigning-values-to-variables"></a>

There are various ways for assigning values to variables.

#### Assigning value during declaration of type <a href="#assigning-value-during-declaration-of-type" id="assigning-value-during-declaration-of-type"></a>

One way to assign values to variables is to do so when declaring the type of variable.

Type the following and compile.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

   //Integers
   
   uint sales \= 12 \* 10\*\*18; //sales in wei  
    
   uint expenses \= 10 \* 10\*\*18; //expenses in wei  
    
   int profits; //profits in wei; it is in int because it can be negative  

}
```

Compile and deploy the contract and view the contract via the interface.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Still, we see no mention of profits. Well, that is not surprising because we have not specified the calculation of profits from sales and expenses.

Delete the deployed contract before proceeding.

#### Assigning value via calculation when we declare the type <a href="#assigning-value-via-calculation-when-we-declare-the-type" id="assigning-value-via-calculation-when-we-declare-the-type"></a>

Profits are determined via a calculation: you deduct expenses from sales to get profits. We can specify this in the line where we specify the type for profits.

Type the following and compile.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

  //Integers

  uint sales \= 12 \* 10\*\*18; //sales in wei  
 
  uint expenses \= 10 \* 10\*\*18; //expenses in wei  
 
  int profits \= sales \- expenses; //profits in wei; it is in int because it can be negative  

}
```

This does not compile because there is an issue with the types of variables involved in computing profits. Profits are of the int type. Sales and expenses are of the uint type. By specifying profits as equal to sales - expenses we are implicitly asking Solidity to convert sales and expenses to int. It tells us that such a conversion can produce wrong results. You can also click on “RemixAI” for greater clarification. At this point, just accept that converting from int to uint or vice versa is fraught with unexpected results. It is best to keep it clean by using one type consistently. Since profits cannot be uint (when they are negative, they cannot be uint), we should make sales and expenses as int.

| <p><strong>Note about converting from one integer type to another</strong> </p><p>We don’t need to get into why a conversion that seems so simple can produce unexpected results. However, if you are interested, go to chatGPT and ask the following question. You don’t have to restrict yourself to just one question but the following is a good start: </p><ul><li>Why does solidity have problems doing implicit integer conversion? Explain with an example.</li></ul> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Type the following and compile.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

   //Integers
   
   int sales \= 12 \* 10\*\*18; //sales in wei  
    
   int expenses \= 10 \* 10\*\*18; //expenses in wei  
    
   int profits \= sales \- expenses; //profits in wei; it is in int because it can be negative  

}
```

You will see that it compiles now.

Deploy the contract and interface with it via Remix.

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

We cannot see the profits. We know what the sales and expenses are but we are unable to see the result for profits.

Delete the deployed contract before proceeding.

To address the problem of not being able to view profits, we make profits as public. In other words, we now say that the variable profits is accessible (i.e., usable and, therefore, viewable) from outside. What does outside mean? It means that it is accessible from addresses other than that of the contract.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

   //Integers
   
   int sales \= 12 \* 10\*\*18; //sales in wei  
    
   int expenses \= 10 \* 10\*\*18; //expenses in wei  
    
   int public profits \= sales \- expenses; //profits in wei; it is in int because it can be negative

}
```

Compile and deploy the contract. View it in the Remix interface. Click on profits to see the value.

Delete the deployed contract before proceeding.

#### Creating a function for greater flexibility <a href="#creating-a-function-for-greater-flexibility" id="creating-a-function-for-greater-flexibility"></a>

What if someone wants to enter different figures for sales and expenses? With the above code, we have hardwired the values for sales and expenses. Therefore, when we want to enter different figures for sales and expenses, we have no choice but to type a new contract with the new figures, recompile it, and then redeploy it. That is expensive.

Also, what if someone types the sales as a negative number or the expenses as a negative number?

We can address the above two issues by setting up a function to calculate profits. That function will have sales and expenses as arguments. We can also set up a requirement in the function that sales and expenses should be positive.

We will first create a function that provides us with the flexibility to enter sales and expenses as arguments. We will worry about requiring sales and expenses as positive later. Note that we have removed the statements in which we were specifying the types for sales and expenses and also specifying their values.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

     //Integers  
          
     int public profits; //profits in wei; it is in int because it can be negative  
      
     function determineProfits(int sales, int expenses) {  
         profits \= sales \- expenses;  
     }  

}
```

The above code gave us an error. That error pertained to the visibility of the function determineProfits. Essentially, the compiler wants to know if the function is private or public.

Add the word ‘private’ in your code as shown below. You add it in the line where you declare the function.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

     //Integers  
          
     int public profits; //profits in wei; it is in int because it can be negative  
      
     function determineProfits(int sales, int expenses) private {  
         profits \= sales \- expenses;  
     } 

}
```

The program runs fine.

Deploy it. Then click on the down arrow to the left of the deployed contract. We see a button for profits but find that there is no way for us to enter sales or expenses. ‘Private’ made the function private and it is now accessible only to code within the contract and not to outsiders like us who are trying to access it from the outside after it is placed on the Ethereum network. Understand we are trying to run it using our EOA. We are outsiders. If we were part of the code within the contract (i.e., contract Types) that is trying to run the function, it would be accessible to us

Before we do any changes to the function, go back to the deployed contract. You see a button for profits. Click on it. What do you see? You see 0. That is because the contract is using the default value for profits. The default value is 0. That is the default value for any variable of type int.

So, for us to be able to access it, we make the function ‘public’. Change the word ‘private’ in the function to ‘public’.

Delete the old deployed contract.

We compile the new contract and deploy it. We click on the down arrow to the right of the contract to be able to interface with it. We go ahead and enter figures for sales and expenses as below. We will keep the numbers small and enter 12 weis and 10 weis respectively.

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

At this point, we have entered the figures for sales and expenses. But we have not run the function determineProfits yet. To confirm that to be the case, click on profits. We will see profits as 0.

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Since we have not invoked the function yet, profit remains uncalculated and has the default value, which is 0.

Click on determineProfits. Then click on profits. You will see the following.

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Change the expenses to -10. Click on determineProfits. Then click on profits. You see 22 as profits, which is not correct because the expenses cannot be -10.

We can guard against that by using the following code. The ‘require’ statement will protect us against someone entering any of those numbers as a negative number.

Delete the old deployed contract.

Add the ‘require’ statement as below to your contract. Compile it.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

    //Integers  
         
    int public profits; //profits in wei; it is in int because it can be negative  
     
    function determineProfits(int sales, int expenses) public {  
        require(sales\>=0 && expenses\>=0);  
        profits \= sales \- expenses;  
    } 

}
```

We are able to compile the above code. Deploy it and interface with it via Remix.

Enter 12 and -10 as sales and expenses. Then click on determineProfits.

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

What do you see?

Since the requirement of positive value for expenses is not met, the function execution terminates. You will see an error message in the window in the bottom right portion of the Remix interface.

Enter 12, 10 for sales and expenses. Then click on determineProfits. Then click on profits. You will see the value 2 for profits.

Enter 10 and 12 for sales and expenses. See the results.

We are all set at this point.

Delete the deployed contract before proceeding.

### State versus local variables <a href="#state-versus-local-variables" id="state-versus-local-variables"></a>

When you consider sales and expenses in the following code, you notice that they have utility inside the function statement. They don't exist outside the function. In other words, they are local to the function. Consequently, they are known as local variables. Profit exists outside the function. It exists outside the function within the contract. It is a state variable. It is going to exist in the state database.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

    //Integers  
         
    int public profits; //profits in wei; it is in int because it can be negative  
     
    function determineProfits(int sales, int expenses) public {  
        require(sales\>=0 && expenses\>=0);  
        profits \= sales \- expenses;  
    } 

}
```

Why should we be concerned about state versus local variables?

* State variables cost more gas on the Ethereum platform. They are going to be stored on the state database and that costs gas.
* The local variables are not stored in the state database and their value is discarded after they are used. There is no cost to store them. There is a cost to process them in the calculation but there is no cost to store them.

At this point, we can define state and local variables as follows:

* State variables are those that are defined at the contract level, outside of any function, and their values are stored on the blockchain.
* Local variables are those that are defined inside a function, and their values are temporary, existing only during the execution of that function.

### Boolean variables <a href="#boolean-variables" id="boolean-variables"></a>

Boolean variables can take two values, true or false. Let us use this in our function. We will create a new variable called isProfitable which will indicate with true or false whether the company is profitable.

Add the if statement as shown below. It specifies when isProfitable will be true or false.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

    //Integers & booleans  
     
    int public profits; //profits in wei; it is in int because it can be negative  
        
    //in the following sales and expenses are in weis  
    
    function determineProfits(int sales,int expenses) public {  
        require(sales\>=0 && expenses\>=0);  
        profits \= sales \- expenses;  
         
        if (profits \> 0) {isProfitable \= true;} else {isProfitable \= false;}  
    }  

}
```

Compile the code. It does not compile. Why? That is because we have not declared the type of isProfitable. Its type is bool, which is short for boolean. Let us also assume that isProfitable is to be visible to anyone outside the contract. Therefore, we will also need to make it public.

Make changes as shown below.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

    //Integers & booleans  
     
    int public profits; //profits in wei; it is in int because it can be negative  
     
    bool public isProfitable; // boolean variable that is true when profits \> 0      
                              // and false otherwise  
     
    //in the following sales and expenses are in weis  
    
    function determineProfits(int sales,int expenses) public {  
        require(sales\>=0 && expenses\>=0);  
        profits \= sales \- expenses;  
         
        if (profits \> 0) {isProfitable \= true;} else {isProfitable \= false;}  
    }  

}
```

Now compile the contract. Then deploy it and interface with it via Remix. Enter some values for sales and expenses and execute the determineProfits function (by clicking on it). Then view values for isProfitable and profits.

Delete the deployed contract.

### String variables <a href="#string-variables" id="string-variables"></a>

What if we wish to communicate a message (e.g., Well done! or Got to do better next time) depending on whether or not we make profits? For that, we first define a string variable called message. We make it public so that it is accessible from outside the contract (for us that means that it is accessible via the Remix interface; if we don’t make it public, we will not be able to see it in our Remix interface). Then we use it in our function for determining profits. See below.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

    //Integers, booleans, & strings  
     
    int public profits; //profits in wei; it is in int because it can be negative  
    
    bool public isProfitable; // boolean variable that is true when profits \> 0  
                              // and false otherwise  
     
    string public message; //message about performance  
     
    //in the following sales and expenses are in weis  
    
    function determineProfits(int sales,int expenses) public {  
        require(sales\>=0 && expenses\>=0);  
        profits \= sales \- expenses;  
         
        if (profits \> 0) {  
            isProfitable \= true;  
            message \= "Well done\!";}  
            else {  
                isProfitable \= false;  
                message \= "Got to do better next time";}  
    }  

}
```

Compile the code. Deploy it and access it via the Remix interface. Enter some values for sales and expenses. Execute the determineProfits function and observe the results.

Delete the deployed contract before proceeding.

| <p>Exercise: Putting your knowledge to work </p><p>This exercise gives you a chance to apply what you have learned about variables, data types, conditional logic, function visibility, and the use of “require” statements in Solidity. The contract you see below is meant to evaluate whether a project stayed within its budget. It compares the project’s budget and actual cost, calculates the resulting savings, and provides a message that indicates whether the project was under or over budget. Your task is to complete the missing parts of the code by filling in the blanks. Use the correct Solidity keywords, logical expressions, and values where appropriate. Once you have filled in all blanks, compile and deploy your contract in Remix to test whether it behaves as expected. Then answer the questions provided after the following code.</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED 
// Purpose: To evaluate whether a project stayed within its budget 
pragma solidity >=0.8.2 <0.9.0; 
contract BudgetEvaluator { 
    // Step 1: Declare variables 
    ______ ______ savings; // can be positive or negative 
    ______ ______ isUnderBudget; // true if project cost <= budget 
    ______ ______ message; // conveys result message 
    // Step 2: Create the function 
    function evaluateProject(______ budget, ______ actualCost) ______ { 
        // Step 3: Statement to guard against negative inputs 
        require(______________, "Inputs must be non-negative"); 
        // Step 4: Compute savings savings = ______________; 
        // Step 5: Determine message and boolean result if (savings >= 0) { 
             isUnderBudget = ______ ; 
             message = "______"; 
         } else { 
             isUnderBudget = ______ ; 
             message = "______"; 
         } 
     } 
}
```

| <p>Questions-</p><ol><li>Which variables are state variables, and which are local?</li><li>What happens if you switch the visibility of the function private?</li><li>If a project exceeds its budget, what values do you expect for savings, isUnderBudget, and message?</li><li>How would you modify the code to prevent future updates once the evaluation is done? (hint: create a boolean variable called "evaluationDone" and make it “true” once the function is executed)<br></li></ol> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### Arrays <a href="#arrays" id="arrays"></a>

An array is a data structure that stores a sequential collection of elements of the same type.

* For instance, a collection of sales over four quarters can be considered as an array.
* Likewise, a collection of expenses over four quarters can also be considered as an array.

See the following illustration. Make a note of the language that is used. Pay attention to the ideas of array length, array element, and index.

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

The arrays that we see in the above figure are fixed length arrays because their length can be specified a priori.

But we often have situations in which it is not possible to specify the length of the array. The length of the array may vary depending on the situation. An array used in such a case is called a dynamic array.

#### Defining an array in Solidity <a href="#defining-an-array-in-solidity" id="defining-an-array-in-solidity"></a>

| Definition in Solidity   | What does it refer to?                                                                                |
| ------------------------ | ----------------------------------------------------------------------------------------------------- |
| int\[4] profits          | An array called profits consisting of 4 integers, one for each quarter’s profits                      |
| uint\[3] examGrades      | An array called examGrades consisting of 3 unsigned integers for the three exams in a class           |
| bool\[3] healthy         | An array called healthy indicating whether someone is healthy or not for members of a 3-person family |
| string\[5] gender        | An array called gender indicating gender of individuals in a 5-person group                           |
| int\[] manyInt           | An array called manyInt consisting of unspecified number of integers                                  |
| uint\[] severalUint      | An array called severalUint consisting of unspecified number of unsigned integers                     |
| bool\[] tooManyBool      | An array called tooManyBool consisting of unspecified number of boolean values                        |
| string\[] severalStrings | An array called severalStrings consisting of unspecified number of strings                            |

| <p>Exercise: Declaring arrays</p><p>Type the following into Remix.</p> |
| ---------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED 
pragma solidity >=0.8.2 <0.9.0;
contract arrayDetour {
    int[3] public aNumericArray = [3,5,7];
    string[2] public aStringArray;
    bool[4] public aBooleanArray; 
}
```

| Try to compile the code. It will give you a compilation error. That is because 3, 5, 7 for aNumericArray can be both int and uint. That is confusing the compiler, even though you define the array as consisting of int values. We have to take one more explicit step as shown below. |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED 
pragma solidity >=0.8.2 <0.9.0;
contract arrayDetour {
    int[3] public aNumericArray = [int(3),int(5),int(7)];
    string[2] public aStringArray;
    bool[4] public aBooleanArray;
}
```

| We have to be explicit when specifying the elements even though we have declared the array as int\[3] because the Solidity compiler builds the array literal \[3, 5, 7] first, and only then tries to match it to int\[3]. At the moment it constructs \[3, 5, 7], it does not yet know that you intend those numbers to be signed integers — each literal 3, 5, and 7 is “typeless” for it. And, therefore, we have to specify its type explicitly. We can also do the following for greater efficiency. |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED 
pragma solidity >=0.8.2 <0.9.0;
contract arrayDetour {
    int[3] public aNumericArray = [int(3),5,7];
    string[2] public aStringArray;
    bool[4] public aBooleanArray;
}
```

| <p>Compile, deploy, and access via the Remix interface. Then do the following:</p><ul><li>Click on the > sign to the left of the newly deployed contract in the contract panel.</li><li>Enter 0 in the space to the right of the button aBooleanArray and press the aBooleanArray button. What do you see?</li><li>Enter 1 in the space to the right of the button aBooleanArray and press the aBooleanArray button. What do you see?</li><li>Enter 2 in the space to the right of the button aBooleanArray and press the aBooleanArray button. What do you see?</li><li>Why do you see what you see? <br>Hint: when you are entering a value, you are entering an index and Ethereum shows you the element at that index position. If nothing has been entered into an array, you see default values. For boolean arrays, the default is false. For string arrays, the default is blank. For numeric arrays, the default is 0</li><li>Repeat the process for the other two arrays and make sense of your experience. Be ready to share your experience.</li><li>Delete the deployed contract before proceeding.</li></ul> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| <p>Exercise: Entering values into arrays when declaring them </p><p>One way to add values for the arrays (as in the case of booleans, strings, and integers) is when we declare them. When we do this, we say that the values are provided “inline.” </p><p>The following code illustrates this possibility. Type it into Remix.</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

```
// SPDX-License-Identifier: UNLICENSED
pragma solidity >=0.8.2 <0.9.0;
contract arrayDetour {
    int[3] public aNumericArray = [int(3),5,7];
    string[2] public aStringArray = ['I am', 'I do'];
    bool[4] public aBooleanArray = [true, false, true, false];
}
```

| <p>Compile, deploy, and access via the Remix interface. Then do the following:</p><ul><li>Click on the > sign to the left of the newly deployed contract in the contract panel.</li><li>Enter 0 in the space to the right of the button aBooleanArray and press the aBooleanArray button. What do you see?</li><li>Enter 1 in the space to the right of the button aBooleanArray and press the aBooleanArray button. What do you see?</li><li>Enter 2 in the space to the right of the button aBooleanArray and press the aBooleanArray button. What do you see?</li><li>Enter 3 in the space to the right of the button aBooleanArray and press the aBooleanArray button. What do you see?</li><li>Enter 4 in the space to the right of the button aBooleanArray and press the aBooleanArray button. What do you see? Look at the feedback for the transaction in the terminal at the bottom right. You will see that there was an error. That is because you are using an undefined index for aBooleanArray which has elements whose indexes are 0, 1, 2, and 3. There are no additional elements and, therefore, the element at index = 4 is undefined.</li><li>Why do you see what you see?</li><li>Repeat the process for the other two arrays and make sense of your experience. Be ready to share your experience.</li><li>Delete the deployed contract before proceeding.</li></ul> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

**We have so far set values of variables “inline”. This method sets values of variables when they are declared. But that is not the only method. We can also set values using a function. The following exercises illustrate that method. We first use that method to set values for variables that are integer, boolean, and string. We then use that method to set values for an array.**

| <p>Exercise: Entering using a function (part 1) </p><p>The following code illustrates setting values of integers, strings, and booleans using a function.</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED
pragma solidity >=0.8.2 <0.9.0;
contract assignValues {
    int public anInteger; 
    string public aString;
    bool public aBoolean;
    function setValues() public {
        anInteger=3;
        aString='I am';
        aBoolean=true;
    }
}
```

| <p>Compile, deploy, and access via the Remix interface.</p><ul><li>Check the values of the variables by clicking on the buttons representing them. What do you observe for anInteger? <br>What do you observe for aString? <br>What do you observe for aBoolean?<br>Be sure to explain your answers.<br>Click on setValues.</li><li>Check the values that have been assigned to the variables.</li><li>How does this method of setting values compare to the “inline”method in terms of the usage of gas? Who pays for the execution of the setValues function?</li><li>If using a function to enter values is more expensive, why use it? The answer is implied in the exercise after the next one below (answer: it gives you the flexibility to keep the values variable – in other words, you can write a function to accept values from a user and set or change them to whatever a user wants)</li><li>Delete the deployed contract before proceeding.</li></ul> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| <p>Exercise: Entering values into arrays using a function </p><p>We will now see how to add values for arrays using a function. </p><p>Copy the following code into Remix.</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

```
// SPDX-License-Identifier: UNLICENSED
pragma solidity >=0.8.2 <0.9.0;
contract arrayDetour {
    int[3] public aNumericArray;
    string[2] public aStringArray;
    bool[4] public aBooleanArray;
    function setValues() public {
        aNumericArray=[int(3),5,7];
        aStringArray=['I am', 'I do'];
        aBooleanArray = \[true, false, true, false];
    }
}
```

| <p>Compile, deploy, and access it via the Remix interface. Then do the following:</p><ul><li>Click on the > sign to the left of the newly deployed contract in the contract panel.</li><li>Enter 0 in the space to the right of the button aBooleanArray and press the aBooleanArray button. What do you see? Why?</li><li>Enter 1 in the space to the right of the button aBooleanArray and press the aBooleanArray button. What do you see? Why?</li><li>Enter 1 in the space to the right of the button aStringArray and press the aStringArray button. What do you see? Why?</li><li>Click on setValues.</li><li>Enter 0 in the space to the right of the button aBooleanArray and press the aBooleanArray button. What do you see? Why?</li><li>Enter 1 in the space to the right of the button aBooleanArray and press the aBooleanArray button. What do you see? Why?</li><li>Repeat the process to check if the remaining elements of aBooleanArray and the elements of aNumericArray and aStringArray have been set properly.</li><li>Delete the deployed contract before proceeding.</li></ul> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| <p>Exercise </p><p>What does the following contract accomplish? Try to understand its logic and compare its method of entering values into an array with the previous two methods you have learned so far. Compile, deploy, and access it via the Remix interface to learn more about it.</p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED
pragma solidity >=0.8.2 <0.9.0;
contract arrayDetour {
    int[3] public aNumericArray;
    function setValues(int x, int y, int z) public {
    aNumericArray= [x,y,z];
    }
}
```

| Delete the deployed contract before proceeding. |
| ----------------------------------------------- |

#### Use of arrays in a smart contract <a href="#use-of-arrays-in-a-smart-contract" id="use-of-arrays-in-a-smart-contract"></a>

To illustrate the use of arrays, we will use arrays for sales and expenses in our contract.

| Exercise Type the following contract into Remix. |
| ------------------------------------------------ |

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables pragma solidity >=0.8.2 <0.9.0;
contract Types{
     //Integers
     int public profits;
     //profits in wei; it is in int because it can be negative
     bool public isProfitable; // boolean variable that is true when profits > 0 and false otherwise
     string public message; //message about performance
     int[4] quarterSales = [int(4),3,2,5];
     int[4] quarterExpenses = [int(2),3,3,4];
     //in the following sales and expenses are in weis
     function determineProfits() public {
          int sales = quarterSales[0] + quarterSales[1] + quarterSales[2] + quarterSales[3];
          int expenses = quarterExpenses[0] + quarterExpenses[1] + quarterExpenses[2] + quarterExpenses[3]; 
          require(sales>=0 && expenses>=0);
          profits = sales - expenses;
          if (profits > 0) {
               isProfitable = true;
               message = "Well done!";
          } 
          else { 
               isProfitable = false;
               message = "Got to do better next time";
          }
     }
}
```

| <p>A few things to note. </p><ul><li>Since any of the arrays is to contain integers and its length is 4, we declared it as int[4]. </li><li>The values of the elements of the array have been entered inline, i.e., along with the declaration of the array. We can also set the values by asking the user to provide input for a function. We will see that method later. </li><li>There is no real need to declare the two arrays (i.e., quarterSales and quarterExpenses) as public. Their use is for computing the total sales and expenses. We will achieve nothing by making them public. We are able to achieve our purpose (i.e., computing the total sales and expenses) without having to make them public. </li><li>The function no longer has inputs or arguments. That is because it makes use of array elements that are defined in the state database by the current contract. We are not calling this function from another contract. Were we to call it from another contract, we would have had to include inputs or arguments to pass from the other contract. </li><li>Compile and deploy. Then interface with it via Remix. Click on determineProfits and see the results. </li><li>Delete the deployed contract before proceeding.</li></ul> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

#### Specification of array values within the function <a href="#specification-of-array-values-within-the-function" id="specification-of-array-values-within-the-function"></a>

There is another way in which one can specify values for the array. Since there is no use of the values of the elements of the array outside the function, you could specify the values within the function. Type the following and try to compile it.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

     //Integers  
      
     int public profits; //profits in wei; it is in int because it can be negative  
     
     bool public isProfitable; // boolean variable that is true when profits \> 0  
                               // and false otherwise  
     string public message; //message about performance  
     
     //in the following sales and expenses are in weis  

      function determineProfits() public {  
           
          int[4] quarterSales = [int(4),3,2,5];  
      
          int[4] quarterExpenses = [int(2),3,3,4];  
           
           
          int sales = quarterSales[0] + quarterSales[1] + quarterSales[2] + quarterSales[3];  
      
          int expenses = quarterExpenses[0] + quarterExpenses[1] +  
                         quarterExpenses[2] + quarterExpenses[3];  
           
          require(sales>=0 && expenses>=0);  
          profits = sales - expenses;  
           
          if (profits > 0) {  
              isProfitable = true;  
              message = "Well done\!";}  
              else {  
                  isProfitable = false;  
                  message = "Got to do better next time";}  
      }  
}
```

The compilation fails. Why?

One of the reasons has to do with the fact that Solidity is not clear about where quarterSales and quarterExpenses should be placed.

Note that the arrays ‘quarterSales’ and ‘quarterExpenses’ are local variables. The arrays are useful only within the function to calculate profits. We are not interested in saving them (let us assume that for the time being) over the long term. We have dealt with local variables before when we included sales and expenses within a function. We are doing the same here but Solidity is facing an issue. The issue arises because arrays are a complex variable type and whenever we are dealing with complex variable types as local variables, we have to make it clear to Solidity that we will store them in a special way. That special way is referred to as memory. We use the keyword ‘memory’ to specify that special way.

See the code below to understand where we include the keyword.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

//Integers  
 
int public profits; //profits in wei; it is in int because it can be negative  

bool public isProfitable; // boolean variable that is true when profits \> 0  
                          // and false otherwise  
string public message; //message about performance  

//in the following sales and expenses are in weis  

function determineProfits() public {  
     
    int[4] memory quarterSales = [int(4),3,2,5];  

    int[4] memory quarterExpenses = [int(2),3,3,4];  
     
     
    int sales = quarterSales[0] + quarterSales[1] + quarterSales[2] + quarterSales[3];  

    int expenses = quarterExpenses[0] + quarterExpenses[1] +
                   quarterExpenses[2] + quarterExpenses[3];  
     
    require(sales>=0 && expenses>=0);
        profits = sales - expenses;
       
        if (profits > 0) {
            isProfitable = true;
            message = "Well done!";}
            else {
                isProfitable = false;
                message = "Got to do better next time";}
    }
}
```

Try to compile it. The error goes away.

Deploy it and interact with it via the Remix interface. Observe the results.

Play around with the numbers for quarterSales and quarterExpenses. Use figures that will result in negative profits. Recompile every time. And deploy the newly compiled smart contract every time to be able to see the results of your changes.

You are sharp. You observe a disparity between what you see in the code and the explanation I gave about memory. Specifically, you observe that we don't really need 'sales' and 'expenses' outside the function. Yet, they do not have the 'memory' keyword in the lines where we declare them. Well, Solidity is fussy about using the memory keyword for only certain types of local variables. Specifically, it is fussy about using it only for variables that are considered as complex types. These include strings and arrays. There are additional types that are considered to be complex (e.g., structs). We have not dealt with them yet. For simpler or primitive types such as boolean and integer (and address, which we have not dealt with yet), it knows where to put them depending on whether we use them entirely within a function or outside it.

Delete the deployed contract before proceeding.

#### Passing an array via a function <a href="#passing-an-array-via-a-function" id="passing-an-array-via-a-function"></a>

We can also provide an array to a function from outside it by making it an input or an argument for the function. See below where we pass the arrays representing quarterSales and quarterExpenses via arguments of the function 'determineProfits'. You will notice that since we are passing arrays to a function and we are not referring to those arrays elsewhere within the contract (i.e., nowhere else except the single function within the contract), we store them in memory using the 'memory' keyword.

Type the following and compile it.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {
   
    //Integers
   
    int public profits; //profits in wei; it is in int because it can be negative
 
    bool public isProfitable; // boolean variable that is true when profits > 0
                              // and false otherwise
    string public message; //message about performance
 
    //in the following sales and expenses are in weis
 
    function determineProfits(int[4] memory quarterSales, int[4] memory quarterExpenses) public {
       
        int sales = quarterSales[0] + quarterSales[1] + quarterSales[2] +
                    quarterSales[3];
 
        int expenses = quarterExpenses[0] + quarterExpenses[1] +
                       quarterExpenses[2] + quarterExpenses[3];
       
        require(sales>=0 && expenses>=0);
        profits = sales - expenses;
       
        if (profits > 0) {
            isProfitable = true;
            message = "Well done!";}
            else {
                isProfitable = false;
                message = "Got to do better next time";}
    }
}
```

Deploy it after compilation.

To interact with it, click on the arrow to the left of the name of the contract under 'Deployed Contracts'. Then click on the down arrow to the right of the input space for determineProfits. You will see something like the following:

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

In the spaces that show up for quarterSales and quarterExpenses, type in \[4,3,2,5] as the input for quarterSales and \[2,3,3,4] as the input for quarterExpenses. Click on transact. Then click on isProfitable, message, and profits. Observe the results.

Change the values for quarterSales and quarterExpenses. After typing in your input, repeat the rest of the process and observe the results.

Delete the deployed contract before proceeding.

#### Processing array values in a more sophisticated way <a href="#processing-array-values-in-a-more-sophisticated-way" id="processing-array-values-in-a-more-sophisticated-way"></a>

Type the code in the following box.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {
   
    //Integers
   
    int public profits; //profits in wei; it is in int because it can be negative
 
    bool public isProfitable; // boolean variable that is true when profits > 0
                              // and false otherwise
    string public message; //message about performance
 
    //in the following sales and expenses are in weis
 
    function determineProfits(int[4] memory quarterSales, int[4]
        memory quarterExpenses) public {
       
        int sales; //this is the same as int sales = 0;
       
        for (uint i = 0; i < 4; i++)
        {
            sales += quarterSales[i]; // this is the same as sales =
                                      // sales + quarterSales[i];
        }
       
        int expenses; //this is the same as int expenses=0;
       
        for (uint i = 0; i < 4; i++)
        {
            expenses += quarterExpenses[i]; // this is the same as expenses =
                                            // expenses + quarterExpenses[i];
        }
       
        require(sales>=0 && expenses>=0);
        profits = sales - expenses;
       
        if (profits > 0) {
            isProfitable = true;
            message = "Well done!";}
            else {
                isProfitable = false;
                message = "Got to do better next time";}
    }
}
```

You will notice that we have done away with

int sales = quarterSales\[0] + quarterSales\[1] + quarterSales\[2] + quarterSales\[3];\
int expenses = quarterExpenses\[0] + quarterExpenses\[1] + quarterExpenses\[2] + quarterExpenses\[3];

Instead, we have two 'for' loops. Try to understand them before compiling your code. Try to formulate in your own words what those loops are trying to achieve.

Compile the contract. Deploy and carry out the same steps as for the previous contract (e.g., enter inputs for quarterSales and quarterExpenses). Observe the results.

Delete the deployed contract before proceeding.

We can make the above program more flexible by making changes in the for loop as shown below. Specifically, we use quarterSales.length instead of 4 when specifying i < 4 in the first for loop. Likewise, we use quarterExpenses.length instead of 4 when specifying i < 4 in the second for loop.. Adding .length at the end of quarterSales gives us the length of the array which is 4. Likewise quarterExpenses.length gives us 4.

```
// SPDX-License-Identifier: UNLICENSED
// Practicing types of variables

pragma solidity >=0.8.2 <0.9.0;

contract Types {

//Integers  
 
int public profits; //profits in wei; it is in int because it can be negative  

bool public isProfitable; // boolean variable that is true when profits \> 0  
                          // and false otherwise  
string public message; //message about performance  

//in the following sales and expenses are in weis  

function determineProfits(int[4] memory quarterSales, int[4]
        memory quarterExpenses) public {
       
        int sales; //this is the same as int sales = 0;
       
        for (uint i = 0; i < quarterSales.length; i++)
        {
            sales += quarterSales[i]; // this is the same as sales =
                                      // sales + quarterSales[i];
        }
       
        int expenses; //this is the same as int expenses=0;
       
        for (uint i = 0; i < quarterExpenses.length; i++)
        {
            expenses += quarterExpenses[i]; // this is the same as expenses =
                                            // expenses + quarterExpenses[i];
        }
       
        require(sales>=0 && expenses>=0);
        profits = sales - expenses;
       
        if (profits > 0) {
            isProfitable = true;
            message = "Well done!";}
            else {
                isProfitable = false;
                message = "Got to do better next time";}
    }
}
```

Compile the contract. Deploy and carry out the same steps as for the previous contract (e.g., enter inputs for quarterSales and quarterExpenses). Observe the results.

Note that in the line where we begin to define the function (i.e., function determineProfits(int\[4] memory quarterSales, int\[4] memory quarterExpenses)), both quarterSales and quarterExpenses are defined as int\[4]. That is still hardwiring. While the code will work if we have 4 integers for sales and 4 integers for expenses, it will not work if we have, say, 52 integers for sales (i.e., we may be considering weekly sales) or 52 integers for expenses (i.e., we may be considering weekly expenses). For our code to work then, we would need to change the initial part of the function to the following: function determineProfits(int\[] memory quarterSales, int\[] memory quarterExpenses). We have made both quarterSales and quarterExpenses as dynamic arrays. Now our code affords the flexibility to change the length of the arrays for quarterSales and quarterExpenses.

Delete the deployed contract before proceeding.

#### Making sense of the for loop <a href="#making-sense-of-the-for-loop" id="making-sense-of-the-for-loop"></a>

How do we make sense of the for loop? The following table takes us through the steps for the loop for sales. We start with the step where we define sales as an integer.

| Step                                           | Meaning                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| int sales                                      | This creates a new variable called sales. It is of the type 'int'. Its value is 0 (default value).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| for (uint i = 0; i < quarterSales.length; i++) | This begins a loop. The first time around, it set i (of the type uint) to 0. It checks if 0 is less than the length of the array quarterSales, which is 4. 0 is less than 4. It continues to execute the processes within the {} of the for loop.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| sales += quarterSales\[i]                      | The first thing within {} is this operation. It means that previous sales should be incremented by quarterSales\[0] (because i = 0]. Previous value of sales is equal to zero (first step above). To 0 it adds quarterSales\[0], which are first quarter sales.                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                                                | At this point, since the steps within {} have been executed, the program loops back to the statement within () following for. In that statement it looks at i++. That part is asking the program to increment i by 1. Previously it was 0. It is incremented to 1. The program compares the new i to the length of quarterSales and checks if it is less than the length. In other words 1 is compared to 4 to see if it is less. It is. The program then proceeds to the operation within {} of the for loop.                                                                                                                                                                       |
| sales += quarterSales\[i]                      | This is asking the program to increment sales by quarterSales\[1] (remember that i is 1 at this point). The previous sales is quarterSales\[0]. This operation ends up adding quarterSales\[0] and quarterSales\[1]. So far, so good.                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|                                                | Since the steps within {} have been executed, the program loops back to the statement within () following for. In that statement it looks at i++. That part is asking the program to increment i by 1. Previously it was 1. It is incremented to 2. The program compares the new i to the length of quarterSales and checks if it is less than the length. In other words 2 is compared to 4 to see if it is less. It is. The program then proceeds to the operation within {} of the for loop.                                                                                                                                                                                      |
| sales += quarterSales\[i]                      | This is asking the program to increment sales by quarterSales\[2] (remember that i is 2 at this point). The previous sales is quarterSales\[0] + quarterSales\[1]. This operation ends up adding quarterSales\[2] to quarterSales\[0] + quarterSales\[1]. Again, this is good up to now. 9                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                | Since the steps within {} have been executed, the program loops back to the statement within () following for. In that statement it looks at i++. That part is asking the program to increment i by 1. Previously it was 2. It is incremented to 3. The program compares the new i to the length of quarterSales and checks if it is less than the length. In other words 3 is compared to 4 to see if it is less. It is. The program then proceeds to the operation within {} of the for loop.                                                                                                                                                                                      |
| sales += quarterSales\[i]                      | This is asking the program to increment sales by quarterSales\[3] (remember that i is 3 at this point). The previous sales is quarterSales\[0] + quarterSales\[1] + quarterSales\[2]. This operation ends up adding quarterSales\[3] to quarterSales\[0] + quarterSales\[1] + quarterSales\[2].                                                                                                                                                                                                                                                                                                                                                                                      |
|                                                | Since the steps within {} have been executed, the program loops back to the statement within () following for. In that statement it looks at i++. That part is asking the program to increment i by 1. Previously it was 3. It is incremented to 4. The program compares the new i to the length of quarterSales and checks if it is less than the length. In other words 4 is compared to 4 to see if it is less. It is not! The program then exits the for loop and goes to the statement after {} of the loop. At this point we have sales equal to quarterSales\[0] + quarterSales\[1] + quarterSales\[2] + quarterSales\[3]. This is the total sales for the year. We are good. |

One can understand the 'for loop' for calculating total expenses in the same way.

#### Adding an element in an array <a href="#adding-an-element-in-an-array" id="adding-an-element-in-an-array"></a>

How does one add a new element to an array? See the following exercises which illustrate how to add an element in static and dynamic arrays. Try out the exercises on your own.

| <p>Exercise: Adding elements in static arrays </p><p>The following code helps you to fill the elements of a static array of length 4 and consisting of integers without having to hardwire it. You can also use this process of filling an element in a particular position to change the value at that position. We make the array public so that we can see values in it at any time. </p><p>// SPDX-License-Identifier: UNLICENSED </p><p>// Practicing a few things about arrays </p><p>pragma solidity >=0.8.2 &#x3C;0.9.0; </p><p>contract moreWithArrays { </p><p>        int[4] public aStaticArray; </p><p>        function addValues(uint index, int value) public { </p><p>                  aStaticArray[index] = value; </p><p>        } </p><p>} </p><p>Compile the contract and deploy it. Interact with the above code via Remix. </p><div><figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure></div><p>Type 3,5 to the right of addValues and click on addValues. Type 0 to the right of aStaticArray. Click on aStaticArray. What do you observe? Type 1 where you had typed 0 and follow the same process. What do you observe? Type 2 where you had typed 1 and follow the same process. What do you observe? Type 3 where you had typed 1 and follow the same process. What do you observe? Do you know how you will fill the other values in the array? </p><p></p><p>What if you wish to change the value in any index position? Let us say that we wish to change the value for index = 3 to 10. Do the following: </p><p></p><p>Type 3,10 to the right of addValues and click on addValues. Then type 3 to the right of aStaticArray and click on aStaticArray. You will see that the new value for index = 3 is 10. </p><p></p><p>Delete the deployed contract before proceeding.</p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

| <p>Exercise: Adding elements in a dynamic array </p><p>The following code helps you add a new book to the dynamic array allBooks (which may be the collection of your books).</p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED 
// Practicing a few things about arrays 
pragma solidity >=0.8.2 <0.9.0;
contract moreWithArrays {
     string[] public allBooks; 
     function addValues(string memory value) public { 
          allBooks.push(value); 
     }
}
```

| <p>Any idea why we had to use ‘memory’ in the function ‘addValues’ when we specified that our input is a string called value? </p><p>Compile the code. Deploy it. Interact with the contract via Remix. </p><div><figure><img src=".gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure></div><p>In the space to the right of addValues, enter your first book (e.g., Learn Solidity). Click on addValues. Then enter your second book (e.g., Learn Java). Click on addValues. </p><p>Then enter 0 to the right of allBooks. Click on allBooks. What do you observe? Enter 1 to the right of allBooks. Click on allBooks. What do you observe? </p><p>Add more books and see the results for yourself. Can you change the title of an existing book? How would you do it? </p><p>It is not possible to change the title of an existing book with the current code. Add a new function to your code as shown below to enable changing of a title.</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

```
// SPDX-License-Identifier: UNLICENSED 
// Practicing a few things about arrays 
pragma solidity >=0.8.2 <0.9.0; 
contract moreWithArrays { 
     string[] public allBooks; 
     function addValues(string memory value) public { 
          allBooks.push(value);
     }
     function changeValues(uint index, string memory newValue) public { 
          allBooks[index] = newValue; 
     } 
}
```

| Add a few books and then try to change the title of an existing book. Please note that when you change the value of an existing book, the index that you provide should be an existing one. In other words, if you have 2 books in the allBooks array, you should not try to change the value for index = 2, 3, or higher because those indexes do not exist yet. Delete the deployed contract before proceeding. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### Finding the length of an array in Solidity <a href="#finding-the-length-of-an-array-in-solidity" id="finding-the-length-of-an-array-in-solidity"></a>

If you are dealing with a static array, you know its length beforehand. There is little point in writing the code to find its length.

But when you have a dynamic array, its length changes with the addition of new elements. What if you wish to find the length of the array at any point?

| <p>Exercise: Modify the contract from the previous exercise to find number of books </p><p>Make the highlighted changes to the code from the previous exercise. It will help you find the number of books by finding the length of allBooks, which is a dynamic array.</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED
// Practicing a few things about arrays 
pragma solidity >=0.8.2 <0.9.0;
contract moreWithArrays {
    string[] public allBooks;
    uint public numBooks; 
    function addValues(string memory value) public { 
         allBooks.push(value); 
         numBooks= allBooks.length; 
    } 
}
```

| <p>Compile the code. Deploy it. Interact with the contract via Remix. </p><div><figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure></div><p>Click on numBooks. What do you observe? Why? </p><p>In the space to the right of addValues, enter your first book (e.g., learn solidity). </p><p>Click on addValues. Click on numBooks. What do you observe? Why? </p><p>Now enter your second book (e.g., learn java) in the space to the right of addValues. </p><p>Click on addValues. Click on numBooks. What do you observe? Why?</p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### More on arrays <a href="#more-on-arrays" id="more-on-arrays"></a>

For more on arrays, visit [https://www.geeksforgeeks.org/solidity-arrays/](https://www.geeksforgeeks.org/solidity-arrays/).
