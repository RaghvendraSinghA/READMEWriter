#### Q1 - Which command is used to list files in sorted order?
      Ans --> ls -S

#### Q2 - What is encapsulation in OOP?
      Ans -->Encapsulation in OOP (Object-Oriented Programming) means bundling data and        
             the methods that operate on that data together inside a class, while controlling direct     
             access to the data So, that other software application code doesn't access
             unwanted data accidentally.

#### Q3 - How can you move a file from one location to another?
      Ans --> mv command, it can also rename the file/folder


#### Q4 - What is the lspci command used for?
      Ans --> lspci stands for list Peripheral Component Interconnect.
              It shows all the external devices connected to motherboard
              through pci-bus.
              e.g. -->
              Graphics cards (GPU)
              Network adapters
              USB controllers
              Audio devices
              Storage controllers

#### Q5 - What is the kill command, and what are its commonly used flags?
      Ans --> kill command is used to kill a process by signaling it with flags. 
      
              Some commonly used flags are -:
              kill -9 process_id   -   Kill process forcefully,Like kill instantly.  
              kill 15 process_id   -   Kill process gracefully,Like gives time to        
                                        process to save its work progress and      
                                        then leave cpu, ram etc.


#### Q6 - What is a transaction in SQL?
      Ans --> A transaction in SQL is a group of one or more database operations      
              treated as a single unit of work.
              So, set of operations but, they work as unit,Either all will execute
              or none will execute.


#### Q7 - What is the xargs command used for?

      Ans --> xargs are used to pass arguments to a command,
              It is used mostly with pipes for chaining output of
              one command to another.
              e.g. pgrep firefox | xargs kill -9
                  This command finds all running processes ids named with firefox 
                  and then using pipe(|) and xargs it pass them to kill.

#### Q8 - What is the difference between a list and a dictionary?
      Ans --> list is data-structure which stores values and have indexes as numbers only.        
              Dictionary data-structure stores values in key-value pairs,      
              keys are indexes and can be of any data-type and because of that       
              they are more descriptive.     
  
              list have O(n) search time complexity while searching a value,
              while dictionary have O(1) time complexity while searching a value     
              if u know key of value.


#### Q9 - How can you find the number of words in a file?
      Ans --> grep -iow pattern filename | wc -l   
      
          This command searches for the word pattern in filename.

          Flags
          -i -> Ignore case
              Matches pattern, Pattern, PATTERN, etc.
          -o -> Only print the matched part
          -w -> Match the whole word only
          |(pipe)  -> pass output to next
          wc -l -> counts number of lines.

#### Q10 - What is the difference between a parameter and an argument?
    Ans --> parameters are written in function definition while      
            arguments are written while calling the function.


#### Q11 - What is the difference between WHERE and HAVING?
    Ans --> WHERE is used to filter rows and HAVING is used   
            to filter groups after GROUP BY.


#### Q12 - What is the difference between a list and an array?
    Ans --> list is dynamic in size and array is of fixed size.     
            Array can have values only of same data-type and list     
            can have values of any data-type.     
            list are slower than array because of internal implementation.    

#### Q13 - What is the difference between an application and a service?
    Ans --> An application is a program designed to perform tasks for a user.
            Usually, an application is something the user directly opens and interacts with,    
            It have graphical user Interface(GUI).
            Examples: Web browser, VS Code, Calculator, Photoshop

            A service is a program or process that usually runs in the background and provides    
            functionality to other applications or the operating system.     
            It doesn't have graphical user Interface(GUI).    
            Examples: Database service (postgresql), Web server (nginx)
            


              
