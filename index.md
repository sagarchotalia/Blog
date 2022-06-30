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

Unfortunately, I fell sick midway through week 1. :( I tried to tackle smaller issues, but couldn't focus at all. So, I cut myself some slack and took rest. Week 2 was similar, I couldn't get much stuff done. However, I put all my energy into getting better and also tried deepening my understanding of the RADIS code. Small challenges like resolving database path errors in ~/radis.json felt like huge wins!