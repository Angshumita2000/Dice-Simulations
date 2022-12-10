# Dice-Project
![Dice](Dice.png)

![R](https://img.shields.io/static/v1?label=Language%20Used&message=The%20R%20Programming%20Language&color=blue&logo=R)<br>
This project aims to find some answers to some experiments made by throwing one (or some) dice. The following questions were answered in this project, with all of them verified by simulating:<br>
1. On an average, how many times must a 6-sided die be rolled until a 6 turns up?
2. On an average, how many times must a 6-sided die be rolled until a 6 turns up twice a row?
3. On average, how many times must a 6-sided die be rolled until the sequence 65 appears (that is a 6 followed by a 5)?
4. On average, how many times must a 6-sided die be rolled until there are two rolls in a row that differ by 1(such as a 2 followed by a 1 or 3, or a 6 followed by a 5)? What if we roll until there are two rolls in a row that differ by no more than 1(so we stop at a repeated roll, too)?
5. We roll 6-sided die n times. What is the probability that all faces have appeared?
6. We roll a 6-sided die n times. What is the probability that all faces have appeared in order, in some six consecutive rolls (i.e., what is the probability that the sub-sequence 123456 appears among the rolls)?
7. Person A rolls n dice and person B rolls m dice. What is the probability that they have a common face showing (e.g., person A rolled a 2 and person B also rolled a 2, among all their dice)?
8. On average, how many times must a pair of 6-sided dice be rolled until all sides appear at least once?
9. Suppose we can roll a 6-sided die up to n times. At any point we can stop, and that roll becomes our “score”. Our goal is to get the highest possible score, on average. How should we decide when to stop?
10. Suppose we roll a fair dice 10 times. What is the probability that the sequence of rolls is non-decreasing?

This project was jointly done by **myself** and **my friend, Ahel Kundu**. To read the full mathematical treatment of the project, head to **[Project](Project.md)**. The blog post of this project is now available on *[R-bloggers](https://www.r-bloggers.com/2022/11/some-problems-related-to-dice/)*.<br>

----

Simulations were done in:
```
               _                                
platform       x86_64-w64-mingw32               
arch           x86_64                           
os             mingw32                          
crt            ucrt                             
system         x86_64, mingw32                  
status                                          
major          4                                
minor          2.1                              
year           2022                             
month          06                               
day            23                               
svn rev        82513                            
language       R                                
version.string R version 4.2.1 (2022-06-23 ucrt)
nickname       Funny-Looking Kid
```

###  This repository contains
- **Animations**: Contains the individual animation codes for each of the animations that were created
- **Simulation Codes**: Contains the individual simulation codes for each of the questions
- **GIFs.R**: Contains all the animation codes in a single file
- **Project-Dice.R**: Contains all the simulation codes in a single file
- **prerequisites.r**:  Contains the included package and codes required for reproducibility
- **Project.md**: Contains the final project with all the mathematical treatments included
- **Plots**: Contains the original plots generated inside the project

----
For any queries, reach us out at:<br>
![LinkedIn](https://img.shields.io/badge/LinkedIn-blue?style=flat&logo=Linkedin)<br>[Debartha](https://www.linkedin.com/in/debartha-paul-90a296a9/) and [Ahel](https://www.linkedin.com/in/ahel-kundu-509b4b1b7/)<br><br>
![Email](https://img.shields.io/badge/Email-white?style=flat&logo=gmail)<br>
*Debartha*: [pauldeep102@gmail.com](mailto:pauldeep102@gmail.com?subject=[GitHub]Dice%20Project%20Issue)<br>
*Ahel*: [ahelkundu2001@gmail.com](mailto:ahelkundu2001@gmail.com?subject=[GitHub]Dice%20Project%20Issue)
