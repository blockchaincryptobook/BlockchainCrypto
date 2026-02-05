# Solidity variables and functions, Part 2

## **Additional types of variables** <a href="#additional-types-of-variables" id="additional-types-of-variables"></a>

We are continuing our discussion of types of variables allowed by Solidity and what you can do with them.

### **Structs** <a href="#structs" id="structs"></a>

In plain english, structs allow you to create your own variable type.

In technical terms, structs are a way by which you define a data structure for storing records.

Example of usage

* Let us say that you wish to store student records consisting of student name, age, and gender.
* There is no variable type in Solidity that will let you store such a record.
* So, you create your own variable type.
* The following struct will enable you to create a variable type (or a structure) to store those records.

```
  struct studentRecord {

    string name;

    uint age;

    string gender;

  }
```

* The following figure depicts the structure of data enabled by the struct studentRecord.

<figure><img src=".gitbook/assets/image (11) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* With an additional step (described later), it will allow you to store a record with the following three fields: the student name, the student age, and student gender.
* Take another example. You may wish to store records of the books that you have ([source](https://www.tutorialspoint.com/solidity/solidity_structs.htm)).
* There is no variable type in Solidity to let you store such records.
* Therefore, you create your own variable type called bookRecord as shown below.

```
  struct bookRecord { 

     string title;

     string author;

     uint bookID;

  } 
```

* The following figure depicts the structure of data enabled by the struct bookRecord .

<figure><img src=".gitbook/assets/image (12) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* With an additional step (described later), it will allow you to store a record with the following three fields: the title of the book, the author, and the bookID.

At this point, note a few things about structs:

* The struct you create is just a type of variable. You can also see it as a blueprint, structure, or framework for storing information.
* In more specific terms, it specifies fields -- their names and nature -- for a record which we may want to create and use.
* A struct (e.g., studentRecord) does not hold values. We have to take an additional step to create variables. The following clarifies this by drawing out the similarity of a struct to a variable type that we are familiar with by now, such as the ‘string’ type.
  * Just like string is a variable type, the struct you define is a variable type.
    * studentRecord is a variable type. It is different from integer, string, boolean, or arrays that we have used so far.
    * bookRecord is another variable type. It is different from integer, string, boolean, or arrays that we have used so far. It is also different from studentRecord.
  * Just like you use the string type to create a new variable (e.g., string studentName;), we use the struct that you define to create a new variable.
    * We can use the studentRecord struct to create a new variable called aStudent as shown below:
      * studentRecord aStudent;
    * We can use the bookRecord struct to create a new variable aBook as shown below:
      * bookRecord aBook;
  * Just like the variable studentName can store a student name (e.g., Alexandra Tucci), aStudent can store a student record. Likewise, aBook can store a book record. See examples below:
    * studentRecord aStudent = studentRecord (“Alexandra Tucci”, 21, “F”);
    * bookRecord aBook = bookRecord(“Learn Java”, “TP”, 1);

The following Solidity exercise, which is adapted from [https://www.tutorialspoint.com/solidity/solidity\_structs.htm](https://www.tutorialspoint.com/solidity/solidity_structs.htm), illustrates how to use a struct.

| <p>Exercise 1</p><ul><li>Create a contract called name to create a string variable called studentName that stores a student name “Anthony Morello”. Make it a state variable with ‘public’ visibility. It will likely look like the following.</li></ul> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED 
pragma solidity \>=0.8.2 \<0.9.0;
contract name {    
          string public studentName \= 'Anthony Morello'; 
}
```

* Now type in the following contract to create a struct and use it to store a book record (you can type it into the same file as the above contract).

```
contract test {    
        struct bookRecord {       
                  string title;       
                  string author;       
                  uint bookID;    
        }     
        bookRecord public aBook \= bookRecord('Learn Java', 'TP', 1);        
} 
```

| <ul><li>What is the difference between the two contracts? How are they similar?</li><li>We see that in the second contract, we define a new variable type. It is called bookRecord. However, we do not create a new variable type in the first contract. We use a variable type that is already provided by Solidity. In both the contracts we use the relevant variable types to create new variables.</li><li>In the first contract, we use the variable type string to create a new variable called studentName. In the second contract, we use the variable type bookRecord to create a new variable called aBook.</li><li>In both the contracts, we store values in the variables at the time of their creation.</li><li>When we create studentName in the first contract, we store “Anthony Morello” in that variable.</li><li>When we create the variable aBook in the second contract, we give the following values to its three fields: 'Learn Java', 'TP', 1. Note that we have to precede these values with the name of the struct, i.e., bookRecord. That serves to provide structure to the values.<br>Had we not assigned any values for the fields in aBook, the default values would have been the following: ””,””,0 (i.e., blank, blank, and 0).</li><li>Compile the second contract and deploy it.</li><li>Click on the aBook variable to see values for its fields. What do you see? Why? (answer available here)</li><li>Make sense of your experience and then proceed to the following exercises.</li></ul> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| <p>Exercise 2</p><p>In the following contract, we write the code to view the value in a particular field -- bookID. We assume that aBook is no longer public.</p><p>Type the following contract:</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED 
pragma solidity \>=0.8.2 \<0.9.0;
contract test {
        struct bookRecord {
                string title;       
                string author;       
                uint bookID;    
        }    
        bookRecord aBook \= bookRecord('Learn Java', 'TP', 1);     
        function getBookInfo() public view returns (uint) {         
                  uint infoWeNeed \= aBook.bookID;         
                  return infoWeNeed;        
        }
}
```

| <ul><li>To refer to any of the fields, we use the following: aBook.fieldName.<br>For instance, to refer to bookID, we say aBook.bookID.<br>To refer to the title, we say aBook.title.</li><li>Since aBook is no longer public, we write a function to access it and use information from it. A function within the contract is able to access it. Our EOA is unable to access it, unlike in the previous exercise. To be sure, it is more cumbersome to access aBook using a function instead of making the variable public but there is value in learning about this method.</li><li>When we declare the function, notice that we use the keyword – view. This is telling the Ethereum virtual machine that our function is one that is not making any changes to any state variable and it is only viewing information in it. By doing so, we are saving gas money because a transaction is not required for a view function.<br>The keywords ‘view’ and ‘pure’ indicate the nature of the function from the viewpoint of state mutability or the mutability of state variables. When any of these is used in the definition of a function, it means that no state variable is going to be mutated or changed. View means that one or more state variables are going to be viewed by the function (but not changed). Pure means that NO STATE VARIABLE IS INVOLVED ANYWHERE WITHIN THE FUNCTION.</li><li>You will also notice the keyword ‘returns’ in the function. This is saying that this function will return something as a result of execution. In the portion in parentheses () that follow ‘returns’, the function is specifying what it will return. It says that it will return a value of type uint.</li><li>Within the function, you see the process that will be followed by it. The process is to return the value of aBook.</li><li>Compile and deploy.</li><li>Run the getBookInfo function to see the result.</li><li>Note that creating the function is a cumbersome way to get information about the bookID. In Exercise 1 we saw that we can see the whole of aBook. But there is a reason for doing what we did. Now we know how to refer to a particular field in a struct type variable.</li><li>The above contract can also be substituted with the following:</li></ul> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED 
pragma solidity \>=0.8.2 \<0.9.0;
contract test {
        struct bookRecord {       
                string title;       
                string author;       
                uint bookID;    
        }    
        bookRecord aBook \= bookRecord('Learn Java', 'TP', 1);      
        function getBookInfo() public view returns (uint) {         
                return aBook.bookID;       
        }
}  
```

| <ul><li>Modify the contract to be able to view the value of two fields together -- bookID and title.</li></ul> |
| -------------------------------------------------------------------------------------------------------------- |

| <p>Exercise 2 (continued)</p><p>In the following contract, we write the code to view the value of two fields -- bookID and title.</p><p>Type the following contract:</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

```
// SPDX-License-Identifier: UNLICENSED  
pragma solidity \>=0.8.2 \<0.9.0;
contract test {
        struct bookRecord {       
                string title;       
                string author;       
                uint bookID;    
        }        
        bookRecord aBook \= bookRecord('Learn Java', 'TP', 1);        
        function getBookInfo() public view returns (uint, string memory)  {       
                return (aBook.bookID, aBook.title);    
        }    
}
```

| <ul><li>Notice that for returns, we specify two values, one of which is a uint and the other is a string. Since string is a complex variable in Solidity, we have to be clear about the location of the value of the string that will be returned. We will not keep it in the state database and let it remain as local. Hence, we use memory.<br>For instance, to refer to bookID, we say aBook.bookID.<br>To refer to the title, we say aBook.title.</li><li>Compile and deploy.</li><li>Run the getBookInfo function to see the result.</li><li>What if you want to get the values of ALL of the fields?</li></ul> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Getting the values of all of the fields was already covered in Exercise 1. But that assumed that aBook was public. What if it is not? How do we do it? The next exercise covers that.

| <p>Exercise 3 </p><p>In this exercise, we will write the code to be able to retrieve information about the book whose record we save. We are assuming that the variable aBook is not public. Since it is not public, then only the code within the contract can view it. We will write a function that is public in accessibility that is able to retrieve the book record. We will make this function public. </p><p>Type the following contract:</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

```
//SPDX-License-Identifier: UNLICENSED 
pragma solidity \>=0.8.2 \<0.9.0;   
contract test {    
        struct bookRecord {       
                string title;       
                string author;       
                uint bookID;    
        }        
        bookRecord aBook \= bookRecord('Learn Java', 'TP', 1);        
        function getBook() public view returns (bookRecord memory) {       
                return aBook;    
        }    
}
```



| <ul><li>Review the function getBook(). In the () portion of returns (), we specify the type of variable that will be returned and where it will be stored. Note that even though aBook is a state variable, we are returning a copy that was generated as a result of ‘return aBook’. This copy is not a local variable in the formal sense because it was not declared inside the function. However, it is treated in the same way as a local variable because it exists only during the function call and is stored in memory, not in storage. Since the value being returned is a struct and the returned copy lives in memory, the returns() portion of the function must specify memory.</li></ul> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| <p>Exercise 4 </p><ol><li>Modify the contract from Exercise 3 to store a new book: [“Learning Python”,”PP”,2]. </li><li>Compile and deploy. </li><li>Use the getBook function to make sure your contract works properly. </li><li>What has happened to the previous book record that you had stored? Can you get to it somehow? </li></ol><p>We find that when we store information about a new book, we lose information about the book we had stored previously. What if we want to store the old book and the new book? Or even more books after that? The next section handles that. But, before that, continue with Exercise 4. </p><ol start="5"><li>Modify your contract to store the book information within the function. That is, move the statement to store the book so that it is within the function. </li><li>Does your contract work? </li></ol><p>We find that our contract does not compile. See if you can get help from ChatGPT.</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### **Using an array with struct type variable to create a database for books** <a href="#using-an-array-with-struct-type-variable-to-create-a-database-for-books" id="using-an-array-with-struct-type-variable-to-create-a-database-for-books"></a>

Often, we are working with multiple records, such as a collection of multiple books. We may want to store records of all the books we have. We can use the struct bookRecord to create a database consisting of multiple records. This can be conceptualized as shown in the figure below (and in this [slide presentation](https://docs.google.com/presentation/d/1CqrB4Vv0MDFNuFDlLMj52LLFYbBQdJKb7_cf0IXcDh0/edit?usp=sharing)).

<figure><img src=".gitbook/assets/image (13) (1) (1).png" alt=""><figcaption></figcaption></figure>

In Solidity, we create an array type that is based on the bookRecord struct as follows:

bookRecord\[] bookDatabase; //we can add public to make it visible

The above is based on the following way to define a dynamic array:

typeOfVariable\[] variableName;

By default, the array bookDatabase will be empty. To store a new record into it, we will have to say:

bookDatabase.push(bookRecord('Learn Java', 'TP', 1));

The above is based on the following way to add a new element to a dynamic array:

variableName.push(newElement);

We will be able to circle through the database like for any array. To access the first element, we will refer to it as bookDatabase\[0]. The second element is bookDatabase\[1], and so on.

| <p>Exercise 5 </p><p>The following code creates the book database for us. Review it and continue on through the bullet points that follow.</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED

pragma solidity \>=0.8.2 \<0.9.0;  
   
contract Books {  
     
//This creates a struct \-- a struct allows us to create a new type of variable.  
//This new type of variable will allow the creation of a record with multiple  
//fields. In our case, the record we would like to create is a book record.  
   
   struct bookRecord {  
      string title; //this defines the first field in the record  
      string author; //this is going to be the second field  
      uint bookID; //this will be the third field  
   }  
     
   //This creates an array that consists of multiple book records.  
   //This array of multiple records creates a database.  
     
   bookRecord\[\] public bookDatabase;    
   
   //The following function receives input for a book record.  
   //After receiving it, it adds it to the array  
     
   function addBook(string memory inputTitle, string memory inputAuthor,  
       uint inputBookID) public  
       {    
           //We create a book record from the input provided by the user.  
           //For that, we use the previously defined struct. Remember  
           //that the struct we created creates a new type of variable.  
           //It is like int or uint. Both are types of variables. int or  
           //uint are not variables. But 'int i' is a variable as is 'uint i'.  
           //So to create a variable that is of the type we created using  
           //struct, we say 'structName variableName'. In the following, we  
           //also have to use memory because the variable we are creating  
           //aBook does not need to be in storage; memory is fine for us.  
           
           bookRecord memory aBook;  
             
           //Once we have a variable aBook, we can give value to it.  
           //Giving it a value means creating a record of a  
           //particular book. The following does that. It takes  
           //the input from the user and populates the fields of  
           //the record that goes by the name aBook  
             
           aBook \= bookRecord(inputTitle, inputAuthor, inputBookID);  
             
           //This adds a new element to the array bookDatabase.  
           //Any time you have to add a new element, you  
           //say nameOfArray.push(element). The nameOfArray in our  
           //case is bookDatabase. The element is a book record.  
           //The book record that we are adding is the book for  
           //which the user has provided us with title, author, and id.  
           //We have called that record as aBook.  
             
           bookDatabase.push(aBook);  
           
        }  
}
```

The above code after removing the comments:

```
// SPDX-License-Identifier: UNLICENSED

pragma solidity \>=0.8.2 \<0.9.0;  
   
contract Books {  
   
   struct bookRecord {  
      string title;  
      string author;  
      uint bookID;  
   }  
     
   bookRecord\[\] public bookDatabase;    
     
   function addBook(string memory inputTitle, string memory inputAuthor,  
       uint inputBookID) public  
       {    
           bookRecord memory aBook;  
     
           aBook \= bookRecord(inputTitle, inputAuthor, inputBookID);  
             
           bookDatabase.push(aBook);  
        }  
}
```

| <p>Exercise 5 (continued) </p><ul><li>Compile the contract and deploy it. </li><li>Add the following three books: <br>Learn Solidity by J. Anton, book id is 1 <br>Learn Java by A. Pressley, book id is 2 <br>Mastering Solidity by R. Modi, book id is 3. </li><li>Circle through the records to get a feel for how to view the entries that you have made. Note that each book is now an element of the bookRecord[] array. To see the first book, for example, type 0 as the index value in the space to the right of the blue button for bookDatabase in the deployed contract. </li><li>See below for a shorter version of the contract. Compare it to the longer version to understand how one can make the transition from the longer version to the shorter version.</li></ul> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED  pragma solidity \>=0.8.2 \<0.9.0;
contract Books {
        struct bookRecord {       
                string title;       
                string author;       
                uint bookID;    
        }        
        bookRecord\[\] public bookDatabase;          
        function addBook(string memory inputTitle, string memory inputAuthor, uint inputBookID) public {                
                bookDatabase.push(bookRecord(inputTitle, inputAuthor, inputBookID));        
        } 
}
```

| <p>Exercise 6 </p><p>Modify the contract you employed in the previous exercise so that you are able to display the following information about the books in the booksDatabase. </p><ul><li>the author of the third book </li><li>the title of the second book </li><li>the id of the first book </li></ul><p>You will have to create a function to retrieve values for each of these variables from the booksDatabase. </p><p>After you compile and deploy the contract successfully, add three books as directed in the previous exercise and test its working. </p><p>Hint: Use the figure at the start of this section to find the way to refer to the values you have been asked to retrieve.</p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### **Using struct to create a database for store profits** <a href="#using-struct-to-create-a-database-for-store-profits" id="using-struct-to-create-a-database-for-store-profits"></a>

We are going to use the notion of structs to store records consisting of store name and profits. We will enhance our smart contract so that anyone calling it (e.g., store manager) can get the annual profits computed and stored along with the store name in a data structure we create using the idea of structs.

But before we use a struct to create a database for store profits, we will do a clean up exercise.

| <p>Exercise 7 </p><p>Take the following contract and streamline it. Specifically, remove the isProfitable and message variables. Also, the profits variable can now be made a local variable -- we will be having a record of profits in the profitsDatabase. There is no need to refer to that variable separately.</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

```
// SPDX-License-Identifier: UNLICENSED  
//Practicing types of variables   
pragma solidity \>=0.8.2 \<0.9.0;   
contract Types {
        //Unsigned or positive integers         
        int public profits; //profits in wei; it is in int because it can be negative       
        bool public isProfitable; // boolean variable that is true when profits \> 0 and false otherwise     
        string public message; //message about performance       
        //in the following sales and expenses are in weis       
        function determineProfits(int\[4\] memory quarterSales, int\[4\]         
        memory quarterExpenses) public {                 
                int sales; //this is the same as int sales \= 0;                 
                for (uint i \= 0; i \< quarterSales.length; i\++) {             
                        sales \+= quarterSales\[i\]; // this is the same as sales \= sales \+ quarterSales\[i\];         
                }                 
                int expenses; //this is the same as int expenses=0;                 
                for (uint i \= 0; i \< quarterExpenses.length; i\++) {             
                          expenses \+= quarterExpenses\[i\]; // this is the same as expenses \= expenses \+ quarterExpenses\[i\];
                }                 
                require(sales\>=0 && expenses\>=0);         
                profits \= sales \- expenses;                 
                if (profits \> 0) {             
                        isProfitable \= true;             
                        message \= "Well done\!";
                }             
                else {                 
                        isProfitable \= false;                
                        message \= "Got to do better next time";
                }     
        }
} 
```

After the above is cleaned up, you should have the following.

```
// SPDX-License-Identifier: UNLICENSED

//Practicing types of variables  
   
pragma solidity \>=0.8.2 \<0.9.0;  
   
contract Types {  
     
    //Unsigned or positive integers  
     
    //in the following sales and expenses are in weis  
   
    function determineProfits(int\[4\] memory quarterSales, int\[4\]  
        memory quarterExpenses) public {  
         
        int sales; //this is the same as int sales \= 0;  
         
        for (uint i \= 0; i \< quarterSales.length; i\++)  
        {  
            sales \+= quarterSales\[i\]; // this is the same as sales \=  
                                      // sales \+ quarterSales\[i\];  
        }  
         
        int expenses; //this is the same as int expenses=0;  
         
        for (uint i \= 0; i \< quarterExpenses.length; i\++)  
        {  
            expenses \+= quarterExpenses\[i\]; // this is the same as expenses \=  
                                            // expenses \+ quarterExpenses\[i\];  
        }  
         
        require(sales\>=0 && expenses\>=0);  
        int profits \= sales \- expenses;

    }  
}
```

In the above contract, look at the line near the end of the contract which reads as follows:

&#x20;     int profits = sales - expenses;

Previously, it was

&#x20;     profits = sales - expenses;

We had to add int because we removed the line where we had defined profits as a state and public variable of the int type.

The contract will give you a few warnings when you compile it. But let us not worry about that.

Now let us proceed with using a struct to create a database for store profits.

At this point, our smart contract accepts quarterly sales and expense figures. We want to enhance it and make it accept the store name and the reporting year as well. It is as if the manager of a store calls our smart contract to submit the name of the store, the reporting year, the quarterly sales figures, and the quarterly expense figures and the smart contract computes the annual profit and stores the store name, the reporting year, and the annual profit in a database consisting of similar records for other stores and years as well.

Essentially, the database that we are trying to create will look something like that in the table below.

| Store1 | 2018 | 5  |
| ------ | ---- | -- |
| Store2 | 2018 | -3 |
| Store3 | 2018 | 1  |
| Store1 | 2019 | 2  |
| Store2 | 2019 | -3 |
| Store3 | 2019 | 4  |

The following contract creates the database we just described.

```
// SPDX-License-Identifier: UNLICENSED

//Practicing types of variables  
   
pragma solidity \>=0.8.2 \<0.9.0;  
   
contract Types {  
         
    //what we are saying next is that we are creating a new record  
    //type called profitRecord  
   
    struct profitRecord{  
            string storeName;  
            string reportingYear;  
            int profitForYear;  
    }  
     
    //We are using the new structure that we created to create a new database.  
    //How can we make a database? Isn't profitsRecord a description for a record?  
    //Yes, it is but we are now going to use profitsRecord\[\]. This is an array of  
    //records that follow the profitsRecord structure. This array is now  
    //describing a collection of records that are shown in Figure 1\.  
   
    profitRecord\[\] public profitsDatabase;  
     
    //in the following sales and expenses are in weis  
     
    function determineProfits(string memory inputStore, string memory inputYear,  
          int\[4\] memory quarterSales, int\[4\] memory quarterExpenses) public {  
         
        int sales; //this is the same as int sales \= 0;  
         
        for (uint i \= 0; i \< quarterSales.length; i\++)  
        {  
            sales \+= quarterSales\[i\]; // this is the same as sales \= sales \+  
                                      // quarterSales\[i\];  
        }  
         
        int expenses; // this is the same as int expenses=0;  
         
        for (uint i \= 0; i \< quarterExpenses.length; i\++)  
        {  
            expenses \+= quarterExpenses\[i\]; // this is the same as expenses \=  
                                            // expenses \+ quarterExpenses\[i\];  
        }  
         
        require(sales\>=0 && expenses\>=0);  
        int profits \= sales \- expenses;  
             
         // The following defines a variable to store the profit along with store  
         // name and year. It then creates a profit record and then adds it to  
         // the profit database.  
   
         profitRecord memory aProfitRecord;  
         aProfitRecord \= profitRecord(inputStore, inputYear, profits);  
         profitsDatabase.push(aProfitRecord);  
         
    }  
}
```

Compile the contract and deploy it. Enter information about the three stores for years 2018 and 2019. Make up figures for quarterly sales and expenses -- just make sure you use different figures for different stores and different years.

Circle through the profitsDatabase variable to see what the values look like.

#### **Searching through a struct based profits database to locate a record** <a href="#searching-through-a-struct-based-profits-database-to-locate-a-record" id="searching-through-a-struct-based-profits-database-to-locate-a-record"></a>

| <p>Exercise 9 </p><p>Consider the contract you completed in Exercise 8 above. What if a manager wants to search through the database that we have created to locate a particular store and find its profits for a particular year? </p><p>The following contract accomplishes that by creating a separate function called ‘toSearch’ for that. See <a href="https://docs.google.com/document/d/1X7I7Xx0Mgd3iF4HOlbGvBxPQl5qIidHy2G1q4jZNvK0/edit?usp=sharing">this document</a> that shows our class attempt with the “do while” loop after corrections to the syntax.</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED

//Practicing types of variables  
   
pragma solidity \>=0.8.2 \<0.9.0;  
   
contract Types {  
     
    //what we are saying next is that we are creating a new record type  
    //called profitsRecord  
   
    struct profitsRecord{  
            string storeName;  
            string reportingYear;  
            int profitForYear;  
           }  
             
    //We are using the new structure that we created to create a new database.  
    //How can we make a database? Isn't profitsRecord a description for a record?  
    //Yes, it is but we are now going to use profitsRecord\[\]. This is an array of  
    //records that follow the profitsRecord structure. This array is now  
    //describing a collection of records that are shown in Figure 1\.  
   
   
    profitsRecord\[\] public profitsDatabase;  
     
    //in the following sales and expenses are in weis  
   
    function determineProfits(string memory store, string memory year, int\[4\] memory quarterSales, int\[4\] memory quarterExpenses) public {  
         
        int sales; //this is the same as int sales \= 0;  
         
        for (uint i \= 0; i \< quarterSales.length; i\++)  
        {  
            sales \+= quarterSales\[i\]; // this is the same as sales \= sales \+ quarterSales\[i\];  
        }  
         
        int expenses; //this is the same as int expenses=0;  
         
        for (uint i \= 0; i \< quarterExpenses.length; i\++)  
        {  
            expenses \+= quarterExpenses\[i\]; // this is the same as expenses \= expenses \+ quarterExpenses\[i\];  
        }  
         
        require(sales\>=0 && expenses\>=0);  
        int profits \= sales \- expenses;  
   
         profitsDatabase.push(profitsRecord(store, year, profits));  
         
    }  
     
      //The following function makes use of the keyword 'view' because there is no state variable that is being altered  
      //by the function. The variables that are being altered are memory variables.  
       
      function toSearch(string memory storeToFind, string memory yearToFind) public view returns (string memory whetherFound, int profitsFound) {  
         
        uint i;           //default is 0  
        bool storeFound;  //default is false  
        bool yearFound;   //default is false  
        bool recordFound; //default is false

         
        do {  
             
            // we are comparing the store name in the profit record under  
            // consideration to the store name provided as a function  
            // argument. The result of comparison will be true or false.   
             
            storeFound \= (keccak256(abi.encodePacked((profitsDatabase\[i\].storeName))) \== keccak256(abi.encodePacked((storeToFind))));  
   
   
            // we are comparing the year in the profit record under  
            // consideration to the year provided as a function  
            // argument. The result of comparison will be true or false.  
   
            yearFound \= (keccak256(abi.encodePacked((profitsDatabase\[i\].reportingYear))) \== keccak256(abi.encodePacked((yearToFind))));

            //recordFound is the combination of storeFound and yearFound. It is   
            //true only when both storeFound and yearFound are true. It is false   
            //otherwise. && (or AND) is like multiplication, true is like 1   
            //and false is like 0\. So, recordFound can be seen as storeFound x   
            // yearFound. Only when both are 1, is recordFound 1 or true.   
            recordFound \= storeFound && yearFound;  
             
            if (recordFound)  
            {whetherFound \= "Found profits for given store and year\!";  
   
            // the following sets the profitsFound to the value in the profit  
            // field in the profit record under consideration  
   
            profitsFound \= profitsDatabase\[i\].profitForYear;}  
            else  
            {whetherFound \= "Failed to find profits for given store and year";}  
             
            i\++; //increment i  
         
        }  
        while (\!recordFound && i \< profitsDatabase.length); //The looping continues as long as recordFound is false AND i, which has just been incremented, is less than length of the profitsDatabase array  
         
        return (whetherFound, profitsFound);  
         
    }  
}
```

The above contract after removing comments is provided below.

```
// SPDX-License-Identifier: UNLICENSED

pragma solidity \>=0.8.2 \<0.9.0;

contract Types {

    struct profitsRecord{  
            string storeName;  
            string reportingYear;  
            int profitForYear;  
           }  
         
    profitsRecord\[\] public profitsDatabase;  
     
    function determineProfits(string memory store, string memory year, int\[4\] memory quarterSales, int\[4\] memory quarterExpenses) public {  
         
        int sales;  
        for (uint i \= 0; i \< quarterSales.length; i\++)  
        {  
            sales \+= quarterSales\[i\];  
        }

        int expenses;  
        for (uint i \= 0; i \< quarterExpenses.length; i\++)  
        {  
            expenses \+= quarterExpenses\[i\];  
        }  
         
        require(sales\>=0 && expenses\>=0);  
        int profits \= sales \- expenses;  
   
         profitsDatabase.push(profitsRecord(store, year, profits));  
    }  
     
      function toSearch(string memory storeToFind, string memory yearToFind) public view returns (string memory whetherFound, int profitsFound) {  
         
        uint i;            
        bool storeFound;  
        bool yearFound;  
        bool recordFound;

         
        do {  
             
            storeFound \= (keccak256(abi.encodePacked((profitsDatabase\[i\].storeName))) \== keccak256(abi.encodePacked((storeToFind))));  
            yearFound \= (keccak256(abi.encodePacked((profitsDatabase\[i\].reportingYear))) \== keccak256(abi.encodePacked((yearToFind))));  
             
            recordFound \= storeFound && yearFound;

            if (recordFound)  
            {whetherFound \= "Found profits for given store and year\!";  
   
            profitsFound \= profitsDatabase\[i\].profitForYear;}  
            else  
            {whetherFound \= "Failed to find profits for given store and year";}  
             
            i\++;  
        }  
        while (\!recordFound && i \< profitsDatabase.length);  
        return (whetherFound, profitsFound);  
    }  
}
```

Let us go through the do-while loop. Assume that the length of the profitDatabase array is 6.

* i starts with the default value which is 0.
* We make use of a do while loop that starts with the first element of the profitsDatabase. It checks whether (a) the storeName for that element matches what the user has provided as input for the function AND (b) the reportingYear for that element matches what the user has provided as input for the function.
* Let us say that either the storeName or the reportingYear of the element does not match what the user has provided. Or both don’t match.
* Therefore, either storeFound or yearFound is going to be FALSE or both are going to be FALSE.
* Since at least one of them is FALSE, recordFound, which is the combination of both, is also going to be FALSE.
* The if (recordFound) part of the code will go to the else part because recordFound is FALSE and whetherFound is going to be computed as “Failed to find profits for given store and year”.
* i is incremented by 1. It goes to 1.
*   The loop checks whether the combination of (a) !recordFound, which is the opposite of recordFound and (b) the result of checking whether i < length of the profitsDatabase array is TRUE. Since,

    * recordFound is FALSE, !recordFound is TRUE, and
    * the result of checking whether i < length of the profitsDatabase array is TRUE

    their combination is TRUE. The loop is supposed to continue as long as whatever follows while is TRUE. Since that is TRUE, the loop continues.
* We again check whether (a) the storeName for that element matches what the user has provided as input for the function AND (b) the reportingYear for that element matches what the user has provided as input for the function
* Let us say that either one of them or both of them don’t match. Then recordFound is again going to be FALSE.
* The if part of the code makes whetherFound = "Failed to find profits for given store and year".
* i is incremented to 2
*   The loop checks whether the combination of (a) !recordFound, which is the opposite of recordFound and (b) the result of checking whether i < length of the profitsDatabase array is TRUE. Since,

    * recordFound is FALSE, !recordFound is TRUE, and
    * the result of checking whether i < length of the profitsDatabase array is TRUE

    their combination is TRUE. The loop is supposed to continue as long as whatever follows while is TRUE. Since that is TRUE, the loop continues.
* Now we will compare the store name and year provided by the user to those of the third element in profitsDatabase. Let us assume that there is a match for both the inputs. In that case recordFound becomes TRUE.
* When recordFound is TRUE, the if part of the code makes whetherFound = "Found profits for given store and year!" and also makes profitsFound as equal to the profits found for the third element of the profitsDatabase array.
* i is incremented to 3.
*   The loop checks whether the combination of (a) !recordFound, which is the opposite of recordFound and (b) the result of checking whether i < length of the profitsDatabase array is TRUE. Since,

    * recordFound is TRUE, !recordFound is FALSE, and
    * the result of checking whether i < length of the profitsDatabase array is TRUE

    their combination is FALSE. The loop is supposed to continue as long as whatever follows while is TRUE. Since that is FALSE, the loop exits.
* After we exit the loop, we go to the next statement in our code, which is to return the values of whetherFound the profitsFound.
* Note that the manner in which two strings are compared is not straightforward.
  * Solidity cannot do a simple comparison of strings.
  * What we do is that we end up hashing the two strings before we compare them.
  * We use the keccak256 function to hash.
    * But keccak256 does not accept strings as they are. We have to encode them using the abi.encodePacked() function.
  * Thus, to compare two strings represented by a and b, we do the following:
    * whetherSame = keccak256(abi.encodePacked(a)) == keccak256(abi.encodePacked(a))
  * whetherSame is a boolean that gives us the result of comparison. In other words, if the a and b are the same then whetherSame is TRUE. Else it is FALSE.

### **Mapping** <a href="#mapping" id="mapping"></a>

Mapping is another way to store information of interest in the form of key-value pairs. The following slide illustrates the basic idea behind mapping.

<figure><img src=".gitbook/assets/image (14) (1) (1).png" alt=""><figcaption></figcaption></figure>

For instance, we may want to store the gender of different individuals so that when we ask for the gender of a specific person, we can get to it quickly.

* We can create a mapping between the name of the person and the gender and call it genderOf.
* We store genderOf\[Alice] as Female, genderOf\[Bob] as Male, and so on.
* In this example, the name is the key and the gender is the value. A particular key and gender constitute a key-value pair.
* A mapping that maps the names of different individuals with their genders can be considered as a database in which we store new mappings and from which we are also able to retrieve the value for any particular key.
* When the time comes to retrieve the gender of anyone, such as Bob, we say that we want genderOf\[Bob].

We can extend this to other possibilities for keys and values. For instance, we could map a person to that person’s address. The following figure illustrates mapping of a person to the address of that person.

<figure><img src=".gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure>

In Solidity, a mapping is created in the following way:

mapping (variable type for key => variable type for value) nameForMapping;

For mapping the gender of a person to that person’s name, we would create the mapping in the following way:

mapping (string => string) genderDatabase;

The first string refers to the name of an individual and the second string refers to that individual's gender.

A mapping is typically stored as a state variable. ‘Typically’ does not mean ‘always’. There is nothing about mappings that prevents you from using them as local variables. But because of how mappings tend to be used, we are likely to find them as state variables.

#### **Example use of mapping: Mapping countries to their capitals** <a href="#example-use-of-mapping-mapping-countries-to-their-capitals" id="example-use-of-mapping-mapping-countries-to-their-capitals"></a>

The following figure maps countries to their capitals. The country is the key and the capital is the value.

<figure><img src=".gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

\
This can be implemented using Solidity code as in the following exercise.

| <p>Exercise 10 </p><ol><li>Type the following code into Remix.</li></ol> |
| ------------------------------------------------------------------------ |

```
// SPDX-License-Identifier: UNLICENSED  
pragma solidity \>=0.8.2 \<0.9.0;   
contract Types {         
        mapping(string\=\>string) public capitalOf;         
        function enterkeyValue (string memory inputCountry, string memory inputCapital) public     {         
        capitalOf\[inputCountry\] \= inputCapital;     
        }     
}
```

| <ol start="2"><li>Compile and deploy the contract. </li><li>Use the enterKeyValue function to enter the following country-capital pairs: <br>USA     Washington DC <br>India    New Delhi <br>UK        London </li><li>Use the capitalOf variable to find the capital of the USA, India, UK, and France. What do you see? What do you see, and how do you explain each of the outputs based on how mappings work in Solidity? </li></ol><p></p><p>Key takeaway: When we enter a country that has not mapped, the mapping variable still returns something. It does not give us an error. The value that it returns is the default for the variable type ‘string’. That is because we are asking it for the capital of France. We have entered the country and we are asking for its capital. If you review the mapping definition, you will see that it is </p><p>mapping(string=>string) </p><p></p><p>The part within parentheses corresponds to COUNTRY => CAPITAL. The variable type for COUNTRY is string. The variable type for CAPITAL is string. We asked for a capital that does not exist in the mapping. It gives us the default for the variable type for CAPITAL, which is “” (or blank).</p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

We can see the use of mapping in Exercise 10 as helping us create a database – a database that allows us to search for the capital of a country. What is the advantage of using a database created using mapping?

* We are able to search it very quickly. Essentially, if we know the key, we can get to the value very quickly.
* Mapping is like the index at the back of a book. If we know the topic that we are interested in, the index tells us the page number and we can directly go to that page and, hence, the topic, without having to mess with other pages and topics. We would not have to start with the first page and see if it has the topic we are looking for and continue our search sequentially until we find the topic that we are looking for.
* We could have also stored the association between a country and its capital using struct-based records as shown below.

<figure><img src=".gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure>

To search for the capital of any country -- say, the UK, we would have to start with the first country and check if it is the UK. If not, we go to the next record. We check that. If it is not the UK, we go to the next one and check that. We would continue that process until we found the UK. At that point, we would extract the capital from that record.

But with mapping, we simply provide the key and we find the value immediately. In our example, we would simply provide the UK as our key and the mapping would immediately give us back its capital. It will not mess with other countries in the database.

<figure><img src=".gitbook/assets/image (20) (1).png" alt=""><figcaption></figcaption></figure>

#### **Using mapping and struct to create a books database** <a href="#using-mapping-and-struct-to-create-a-books-database" id="using-mapping-and-struct-to-create-a-books-database"></a>

One can use the notions of mapping and structs to create a books database.

<figure><img src=".gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>

A question that arises is: what should the key be?

A key is usually something that is unique for any value in the key-value pair. For instance, mapping of a country to its capital will not work if India has two capitals. India or any other country should map to only one capital because if it maps to more than one capital, we will confuse whoever is trying to find the capital corresponding to India.

We cannot use either the title or the book author as the key because there can be two or more books with the same title or two or more books by the same author.

Is there a way for us to create a key that will be unique for each book? Yes, we could concatenate the title of the book and its author. The chances for that combination to repeat itself would be rare. It is not impossible because you could have the second or more advanced versions of a book by the same author. But let us assume that that does not happen for the time being.

<figure><img src=".gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Let us see how we would implement this in Solidity.

| <p>Exercise 11 </p><ol><li>Type the following code into Remix.</li></ol> |
| ------------------------------------------------------------------------ |

```
// SPDX-License-Identifier: UNLICENSED  
pragma solidity \>=0.8.2 \<0.9.0;  
contract BooksMapping {   
        struct bookRecord {       
                string title;       
                string author;       
                uint bookID;
        }   
        mapping(string\=\>bookRecord) public mappedBookDatabase;      
        function mapBook(string memory key, string memory inputTitle, string memory inputAuthor, uint inputBookID) public {
        mappedBookDatabase\[key\] \= bookRecord(inputTitle, inputAuthor, inputBookID);    
        }
}
```

| <ol start="2"><li>Compile and deploy the contract. </li><li>Use the mapBook function to enter the first three key-value pairs shown below. The key for any book is a concatenation of the name of the book and the author.</li></ol><div><figure><img src=".gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure></div><ol start="4"><li> Input the following in the input area for the mappedBookDatabase variable and click on mappedBookDatabase to see the result. What do you observe? Why? <br>Learn SoliditySP <br>Learn PythonPP <br>Learn JavaJP </li><li>Now make sense of the contract. Explain in a few sentences the working of the contract. </li><li>Type ‘Learn RRP’ (without quotes) in the input area for the mappedBookDatabase and click on mappedBookDatabase. What do you observe? Why? </li><li>Let us say that the author of Learn Python comes out with a second edition of the same book and we have books and their key-value pairs as shown below. Using the contract deployed in the previous exercise, go ahead and enter the new book.</li></ol><div><figure><img src=".gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure></div><ol start="8"><li>Input the following in the input area for the mappedBookDatabase variable and click on mappedBookDatabase to see the result. What do you observe? Why? <br>Learn PythonPP</li></ol> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| <p>Exercise 12</p><p>We will now try to automate the key creation. </p><ol><li>Type the following code into Remix.</li></ol> |
| ---------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED  
pragma solidity \>=0.8.2 \<0.9.0;   
contract BooksMapping {   
        struct bookRecord {       
                string title;       
                string author;       
                uint bookID;    
        }   
        mapping(string\=\>bookRecord) public mappedBookDatabase;      
        function mapBook(string memory inputTitle, string memory inputAuthor, uint inputBookID) public {
                string memory concatenatedTitleAuthor \= string(abi.encodePacked(inputTitle,inputAuthor));
                mappedBookDatabase\[concatenatedTitleAuthor\] \= bookRecord(inputTitle, inputAuthor, inputBookID);    
        } 
}
```

| <ol start="2"><li>Compile and deploy the contract. </li><li>Use the mapBook function to enter the following information for three books: <br>Learn Solidity by JS, book id is 1 <br>Learn Java by JJ, book id is 2 <br>Learn Python by JP, book id is 3 </li><li>Input the following in the input area for the mappedBookDatabase variable and click on mappedBookDatabase to see the result. <br>Learn SoliditySP <br>Learn PythonPP <br>Learn JavaJP </li><li>You must have noticed that this contract works just like the previous contract. However, you did not have to enter the key when entering book information. Why? To understand, look at the difference in the code between this and the previous contract. One of the new lines that you will find in the latest contract is the following: string memory<br>concatenatedTitleAuthor = string(abi.encodePacked(inputTitle,inputAuthor)); <br><br>In this new line, the part after the equal sign achieves concatenation (or joining) of two strings given by inputTitle and inputAuthor. In general, whenever you have to concatenate two strings a and b, you use the following: string(abi.encodePacked(a,b)). </li><li>Explain the working (i.e., the logic part within {}) of the mapBook function in a few sentences (e.g., 4-5 sentences at the most).</li></ol> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

The following gives the code in Exercise 12 with relevant comments.

```
// SPDX-License-Identifier: UNLICENSED

//Smart contract that allows one to add a book to the bookDatabase.  
//This smart contract makes use of mapping  
   
pragma solidity \>=0.8.2 \<0.9.0;  
   
contract BooksMapping {  
//This creates a bookRecord with particular fields  
   
struct bookRecord {  
      string title;  
      string author;  
      uint bookID;  
   }  
     
//This creates the mapping that we will use.  
//The key will be a string that is a concatenation of book title and  
//book author. Why concatenate? To avoid collision with another  
//book of the same title. It is less likely (though not impossible)  
//for two books to have the same title and authors. But we will assume  
//that the concatenation will produce a unique key and, hence,  
//a unique mapping.  
   
   
mapping(string\=\>bookRecord) public mappedBookDatabase;  
   
   
//This function will map a book's record (defined by the above struct)  
//to the concatenated key.  
   
   
   function mapBook(string memory inputTitle, string memory inputAuthor, uint inputBookID) public {  
             
           //Concatenate title & author to create the key  
           string memory concatenatedTitleAuthor \= string(abi.encodePacked(inputTitle,inputAuthor));  
             
           //Now map aBook to concatenatedStoreYear  
           mappedBookDatabase\[concatenatedTitleAuthor\] \= bookRecord(inputTitle, inputAuthor, inputBookID);  
   }  
     
}
```

####

| <p>Note regarding concatenation in the previous code We use abi.encodePacked in Solidity to concatenate multiple string or data inputs into a single sequence of bytes. It efficiently combines values without adding extra padding, which makes it ideal for tasks like forming keys or creating identifiers. However, the result of this operation is of type bytes, not string. To convert these bytes back into a string that can be stored, displayed, or used as a key in a mapping, we wrap the result with the string() function. </p><p></p><p>In short, abi.encodePacked joins values together as bytes, and string() converts those bytes into a readable string representation.</p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### **Searching through a mapping** <a href="#searching-through-a-mapping" id="searching-through-a-mapping"></a>

We will do two exercises to help us search through a mapping. The first exercise shows us how. The second exercise makes use of learning from the first exercise.

| <p>Exercise 13 </p><ol><li>Type in the following contract. The contract is based on the contract in Exercise 10. Review it to answer the questions that follow.</li></ol> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED  
pragma solidity \>=0.8.2 \<0.9.0;   
contract Types {         
        mapping(string\=\>string) capitalOf;         
        function enterkeyValue (string memory inputCountry, string memory inputCapital) public {         
                capitalOf\[inputCountry\] \= inputCapital;
        }      
        function findCapital(string memory inputCountry) public view returns (string memory) {         
                return capitalOf\[inputCountry\];     
        }
}
```

| <ol start="2"><li>What is the purpose of the findCapital function? In other words, what does it try to do? To answer this, remove the findCapital function and compile and deploy the contract. Can you find the capital somehow? </li><li>Try out the contract with a few inputs to understand it better. </li><li>What makes it reasonable to use ‘view’ in the findCapital function?</li></ol> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| <p>Exercise 14 </p><ol><li>Type in the following contract. The contract is the same as the contract in Exercise 12 except that the findBookInfo function is new. Also, mappedBookDatabase is no longer “public”. We, therefore have a function to retrieve information from mappedBookDatabase. A part of the function is blank. The steps that follow indicate the purpose of the function to let you fill the blank appropriately.</li></ol> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

```
//SPDX-License-Identifier: UNLICENSED  
pragma solidity ^0.8.0;
contract BooksMapping {
        struct bookRecord {       
                string title;       
                string author;       
                uint bookID;
        }   
        mapping(string\=\>bookRecord) mappedBookDatabase;      
        function mapBook(string memory inputTitle, string memory inputAuthor, uint inputBookID) public {
                string memory concatenatedTitleAuthor \= string(abi.encodePacked(inputTitle,inputAuthor));
                mappedBookDatabase\[concatenatedTitleAuthor\] \= bookRecord(inputTitle, inputAuthor, inputBookID);
        }     
        function findBookInfo(string memory inputTitle, string memory inputAuthor)            
        public view returns (bookRecord memory) {           
                return \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_;
        }
}
```

| <ol start="2"><li>The blank that you see in the code needs to be filled in so that when a user calls the findBookInfo function, the user is able to see the whole book record that corresponds to the title and author provided by the user. Go ahead and fill the blank. </li><li>Modify the findBookInfo function so that the function returns only the ID of the book whose title and author are provided by the user.</li></ol> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## **Allowing only certain addresses to search** <a href="#allowing-only-certain-addresses-to-search" id="allowing-only-certain-addresses-to-search"></a>

### **Restricting search for the books database** <a href="#restricting-search-for-the-books-database" id="restricting-search-for-the-books-database"></a>

What if we want only the creator of the books database contract to be able to store the books? The following exercise helps us understand how we can do that.

| <p>Exercise 14 </p><ol><li>Type in the following contract.</li></ol> |
| -------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED  
pragma solidity \>=0.8.2 \<0.9.0;   
contract BooksMapping {   
        struct bookRecord {       
                string title;       
                string author;       
                uint bookID;
        }
        address public creator;   
        constructor() {     
                creator \= msg.sender; 
        }  
        mapping(string\=\>bookRecord) public mappedBookDatabase;      
        function mapBook(string memory inputTitle, string memory inputAuthor, uint inputBookID) public {
                string memory concatenatedTitleAuthor \= string(abi.encodePacked(inputTitle,inputAuthor));
                mappedBookDatabase\[concatenatedTitleAuthor\] \= bookRecord(inputTitle, inputAuthor, inputBookID);             }     
        function findBookInfo(string memory inputTitle, string memory inputAuthor)            
        public view returns (uint) {          
                require (msg.sender \== creator, "You are not the creator of the contract.");           
                return  mappedBookDatabase\[string(abi.encodePacked(inputTitle,inputAuthor))\].bookID;            
        }
}
```

| <ol start="2"><li>Compile and deploy the contract. </li><li>Click on the variable ‘creator’ to find its value. Look at the address of the EOA that you used to deploy the contract (look under the label ACCOUNT). How does the value of the variable ‘creator’ compare to the address of your EOA? </li><li>Change your EOA to the second address in the drop down under ACCOUNT. </li><li>Using the mapBook function, try to enter the following as your first book: <br>Title: Learn Java <br>Author: JP <br>ID: 1 </li><li>What do you observe? Can you explain the reason behind whatever that you observe? </li><li>Now change your EOA back to the first one. </li><li>Try to enter the first book again. Are you able to? Why? </li><li>Using the mapBook function, enter the following as your second book: <br>Title: Learn Solidity <br>Author: SP <br>ID: 2 </li><li>Switch to the second EOA account like before. </li><li>Use the findBookInfo function to find the ID of the book whose title is ‘Learn Java’ and author is ‘JP’. Are you able to find the ID? Can you explain why the second EOA worked for this function? </li><li>Be ready to discuss your observations.</li></ol> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

One can make sense of your observations in the previous exercise by understanding the use of the constructor function.

* The constructor function is a special function in Solidity. It is always called 'constructor'. It may or may not have arguments (input parameters). The statements in it are executed only once at the time of the deployment of the contract. They are ignored after that.
* The constructor within our contract does the following:
  * It makes use of a global variable 'msg.sender'. A global variable is something that does not need to be defined. It is provided by the Ethereum environment. The variable ‘msg.sender’ refers to the address of the sender of a message. Remember that the constructor runs at the time of deployment. The deployment happens when the deployer sends a message to the network seeking deployment of the contract. In other words, at the time of deployment, the sender is the deployer.
  * It takes the address of the deployer's address (msg.sender) and stores it as ‘creator’.
* In the mapBook function, we add a require statement that checks whether the entity invoking the function has the same address as that of the creator.
  * The require statement has two parameters. The first one is the condition that needs to be met. The second is the feedback message that is provided when the condition is not met. This message is "You are not the creator of the contract."
* The require statement allows the rest of the function to execute only if the entity invoking the function has the same address as that of the creator. In the event the address of the entity invoking the function is not the same as that of the creator, the function exits. In the feedback area of Remix, we see the message "You are not the creator of the contract." being provided as feedback when the condition in the require statement is not met.

### **Restricting more efficiently by using function modifier** <a href="#restricting-more-efficiently-by-using-function-modifier" id="restricting-more-efficiently-by-using-function-modifier"></a>

The previous contract allowed anyone to add books but allowed only the creator of the contract to view the books. What if we want only the creator to both add and view books. We will need the require statement in two functions.

Is there a more efficient way than that? There may be situations where we have several functions that need to be restricted. A more efficient way would be helpful.

The contract in the following exercise illustrates a more efficient way to restrict who can use the functions in the contract.

| <p>Exercise 15 </p><ol><li>Type in the following contract.</li></ol> |
| -------------------------------------------------------------------- |

```
// SPDX-License-Identifier: UNLICENSED  
pragma solidity \>=0.8.2 \<0.9.0;   
contract BooksMapping {   
        struct bookRecord {       
                string title;       
                string author;       
                uint bookID;    
        }   
        address public creator;   
        constructor() {     
                creator \= msg.sender; 
        }  
        modifier onlyCreator {     
                require(msg.sender\==creator, 'You are not the creator.');     \_; 
        }  
        mapping(string\=\>bookRecord) public mappedBookDatabase;      
        function mapBook(string memory inputTitle, string memory inputAuthor, uint inputBookID) onlyCreator public {
                string memory concatenatedTitleAuthor \= string(abi.encodePacked(inputTitle,inputAuthor));
                mappedBookDatabase\[concatenatedTitleAuthor\] \= bookRecord(inputTitle, inputAuthor, inputBookID);
        }     
        function findBookInfo(string memory inputTitle, string memory inputAuthor) onlyCreator public view returns (uint) {           
                return  mappedBookDatabase\[string(abi.encodePacked(inputTitle,inputAuthor))\].bookID;            
        }
}
```

| <ol start="2"><li>Compile and deploy the contract. </li><li>Click on the variable ‘creator’ to find its value. Look at the address of the EOA that you used to deploy the contract (look under the label ACCOUNT). How does the value of the variable ‘creator’ compare to the address of your EOA? </li><li>Change your EOA to the second address in the drop down under ACCOUNT. </li><li>Using the mapBook function, try to enter the following as your first book: <br>Title: Learn Java <br>Author: JP <br>ID: 1 </li><li>What do you observe? Can you account for whatever that you observed? </li><li>Now change your EOA back to the first one. </li><li>Try to enter the first book again. Are you able to? </li><li>Using the mapBook function, enter the following as your second book: <br>Title: Learn Solidity <br>Author: SP <br>ID: 2 </li><li>Switch to the second EOA account like before. </li><li>Use the findBookInfo function to find the ID of the book whose title is ‘Learn Java’ and author is ‘JP’. Are you able to find the ID? Can you explain why the second EOA did not work for this function? Try your luck with the first EOA account. What do you observe? </li><li>Be ready to discuss your observations.</li></ol> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

The following helps us make sense of the contract in the previous exercise.

* We moved the ‘require’ statement into a function modifier.
* After defining the function modifier we used it in the functions where we want the same restriction to apply by using its name ‘onlyCreator’ in the first line of the function along with other keywords such as public, etc.
* We use it in both the functions in our contract – i.e., mapBook and findBookInfo.

This method of restricting who can invoke a function using a modifier is more efficient than incorporating the requirement statement in the function itself if there is more than one function where we need to apply the same restriction.
