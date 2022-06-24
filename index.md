# Chapter 0
### Pre-GSoC Phase
#### ??? - 20th May, 2022
I first started searching for organisations back in January. After extensive research, I found OpenAstronomy to be quite interesting and joined the Slack channel. I was looking at the sub-organisations in OpenAstronomy, and joined their individual Slack channels as well.
It was around this time that I started looking at the good first issues of the sub-orgs. I was very new to open-source, hence even basic stuff like issuing PR's and tackling simple `good-first-issues` was challenging to me.

After looking at the codebase and the issues a bit and talking on Slack, I found *RADIS* to be a fitting place for me. 

I started solving some of the good first issues; during the pre-GSoC phase, I added some links to the RADIS Flowchart and tried to solve another good issue, which involved adding the feature of a "cutoff error" parameter to the code. I committed the first simple changes, but my approach was wrong. Dr. Erwan suggested a much more elegant approach, and so I worked on that a bit. I have yet to implement those changes in the form of Numpy Arrays, which will make the code faster and improve readability.

# Chapter 1
### Community Bonding Period
#### 20th May - 12th June, 2022
During the Community Bonding Period, I talked with my fellow RADIS GSoC participants and got to know their projects better. I read the RADIS research paper and got to know about the physics behind the code. I steadily continued my progress understanding the codebase, and also began tackling a challenge that Dr. Erwan mentioned to me: adding of a `chunksize` parameter in the [_broaden_lines()](https://github.com/radis/radis/blob/b853a26b34a0b9b53670062a2214da4d134ec391/radis/lbl/broadening.py#L2115)function, present in the [broadening.py](https://github.com/radis/radis/blob/develop/radis/lbl/broadening.py) file.

I took some time understanding how the code was written and structured initially, and was quite impressed at the technique used to divide the database into chunks and process these chunks instead of individual lines. I thought it necessary to change a bit of the code structure, shifting the focus to the chunksize in terms of readability.

# Chapter 2
### Coding Begins!

Dr. Erwan let us know about the community's plan to conduct our projects in teams of two, based on our projects' similarities. 

Thus a team between [Arunava Basu](https://github.com/arunavabasu-03) and I, and a team between [Tran Huu Nhat Huy](https://github.com/TranHuuNhatHuy) and [Supriya Kumari](https://github.com/Supriya1702) was formed.