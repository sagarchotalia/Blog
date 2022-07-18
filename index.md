# Chapter 0
### Pre-GSoC Phase
#### ??? - 20th May, 2022
I first started searching for organisations back in January. After extensive research, I found OpenAstronomy to be quite interesting and joined the Slack channel. I was looking at the sub-organisations in OpenAstronomy, and joined their individual Slack channels as well.
It was around this time that I started looking at the issues of the sub-orgs. I was very new to open-source, hence even basic stuff like issuing PR's and tackling simple `good-first-issues` was challenging.

After looking at the codebase and the issues a bit, and engaging with the community on Slack, I found *RADIS* to be a fitting place for me.

I started solving some of the good first issues; during the pre-GSoC phase, I added some links to the RADIS Flowchart. This was quite simple, and I solved it easily, thus earning myself my *first contribution*!
I also tried to solve another good issue, which involved adding the feature of a "cutoff error" parameter to the code. I committed the first simple changes to the codebase, but my approach was wrong. Dr. Erwan suggested a much more elegant approach, and so I worked on that a bit. However, I wrote the code in a very basic and simple way, making use of lists everywhere. I have yet to implement those changes in the form of Numpy Arrays, which will make the code faster and improve readability.

# Chapter 1
### Community Bonding Period
#### 20th May - 12th June, 2022
During the Community Bonding Period, I talked with my fellow RADIS GSoC participants and got to know their projects better. I also read the RADIS research paper and got to know about the physics behind the code. 

It was around this time(27th May) that my exams got over, and naturally my family suggested that we go on a short vacation. Hence making time for GSoC was a bit difficult.

I steadily continued my progress in understanding the codebase, and also began tackling a challenge that Dr. Erwan mentioned to me: adding of a `chunksize` parameter in the [_broaden_lines()](https://github.com/radis/radis/blob/b853a26b34a0b9b53670062a2214da4d134ec391/radis/lbl/broadening.py#L2115)function, present in the [broadening.py](https://github.com/radis/radis/blob/develop/radis/lbl/broadening.py) file.

I took some time understanding how the code was written and structured initially, and was quite impressed at the technique used to divide the database into chunks and process these chunks instead of individual lines. I thought it necessary to change a bit of the code structure, shifting the focus to the chunksize in terms of readability.

All in all, the Community Bonding Period was quite fun! I got to enjoy a bit of my post-exam "summer" break, and also spent some time coding.

# Let the Coding Begin!

# Chapter 2: Weeks 1 and 2

Dr. Erwan let us know about the community's plan to conduct our projects in teams of two, based on our projects' similarities. 

Thus a team between [Arunava Basu](https://github.com/arunavabasu-03) and I, and a team between [Tran Huu Nhat Huy](https://github.com/TranHuuNhatHuy) and [Supriya Kumari](https://github.com/Supriya1702) was formed.

Unfortunately, I fell sick midway through week 1. I tried to tackle smaller issues, but couldn't focus at all. 
So, I cut myself some slack and took rest. Week 2 was similar, I couldn't get much stuff done. However, I put all my energy into getting better and also tried deepening my understanding of the RADIS code. Small challenges like resolving database path errors in ~/radis.json felt like huge wins!

Slowly but steadily, I began to solve the chunksize issue that was assigned to me. I looked at the various functions in broadening.py, and how they interact with each other. It was super interesting to see how all the functions were so useful, and how the computation of one parameter given certain constraints, utilized many of the functions.

# Chapter 3: Weeks 3 and 4

In week 3, I began testing my implementation of the chunksize feature. I found that there was an error being raised in the plotting of graphs, due to a library called *publib* being used. Upon searching for this library, I was amazed to see that it was built by Dr. Erwan! You can have a look at it [here](https://github.com/erwanp/publib)

I initially thought nothing of the error, and was convinced that my implementation was correct. Dr Erwan then guided me to [an example](https://radis.readthedocs.io/en/latest/auto_examples/plot_styles.html#sphx-glr-auto-examples-plot-styles-py) in the RADIS Example Gallery, in which you can change the library being used. Hence, I dropped publib and just used the default config used in the example, which used Seaborn. I found it worked for me, hence I continued with it.

I ran the chunksize code again, and found out that I was getting some errors regarding array sizes not being equal, during the initialization of a DataFrame in the code. Since Pandas DataFrames require all rows to be equal in size, this was an unavoidable error. I began debugging the error.

It turned out that, when the chunksize loop was running in the code, and optimization was set as a parameter, certain values were being calculated incorrectly. Let me walk you through the broadening calculations of RADIS:

- When we want to calculate the broadening without chunksize, i.e. over the entire DataFrame, we set parameters like `line_profile`, `wavenumber`, `abscoeff`, and certain other parameters such as `line_profile_LDM, wL, wG, wL_dat, wG_dat` which are important to the internal computations of RADIS.
- The wL, wG, wG_dat and wL_dat parameters then set a few more values that are used in the function `_apply_lineshape_LDM()`, which is the final step in the broadening process.
- Usually, when we calculate all these constants over the entire DataFrame, they can be arrays with large lengths. Hence while computing them over chunks of the DataFrame, these individually calculated arrays need to be appended to the initialised constants. This was the step I was doing wrong, which I then fixed.

I found that after this correction, the errors I had encountered while plotting the graphs were gone. However, just as soon as one error was resolved, another one occurred :')
The example that I was testing my code in wasn't even entering the Chunksize loop. I took a long look at the code, and added chunksize as parameters in two very important functions: [calc_spectrum()](https://github.com/radis/radis/blob/b853a26b34a0b9b53670062a2214da4d134ec391/radis/lbl/calc.py#L38) and [calc_spectrum_one_molecule()](https://github.com/radis/radis/blob/b853a26b34a0b9b53670062a2214da4d134ec391/radis/lbl/calc.py#L568). These are the two main functions invoked whenever we want to calculate a spectrum with RADIS, given the input parameters such as the temperature, pressure, type of molecule, database to refer etc. I then improved the code a bit, fixed the mistakes I had made during my initial implementation, and voila! The example was atleast entering the right part of the code. This didn't solve all my issues though.

![image](/Users/sagarchotalia/Blog/Assets/image.png)

This was the output when I ran the code with the exact same conditions, apart from the chunksize parameter, which you can observe was set to 300 for the black coloured lines and `None` for the red one. The output should've been the exact same, but it wasn't. And so, I got to debugging the error.