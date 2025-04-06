# TinyTroupe-Test

##  Step 1: Install Packages

Open a terminal from Codespace on Github. In the terminal, run the following command to clone the repository:

```bash
git clone https://github.com/microsoft/tinytroupe
```
Change directory into the  `tinytroupe` folder:

```bash 
cd tinytroupe
```

```bash 
pip install .
```
##  Step 2: Setup API Key

In the terminal that you just installed packages, use the following command to setup API Key:

```bash
export OPENAI_API_KEY="xxxx"
```

##  Step 3: Experiments (Simulation)

### Talk to an existing persona

```bash 
from tinytroupe.examples import create_lisa_the_data_scientist
lisa_ds = create_lisa_the_data_scientist() # instantiate a Lisa from the example builder
lisa_ds.listen_and_act("Tell me about your life.")
```

###  Talk to a customized persona

This implies you need to define a new persona using `tinytroupe` package.

```Python
from tinytroupe.agent import TinyPerson
# Create agents with richer backgrounds and personalities
faria = TinyPerson("Faria")
faria.define("age", 25)
faria.define("nationality", "American")
faria.define("occupation", "She is a passionate middle school teacher and a part-time student majoring in Data Science at a university in New York City.")
faria.define("hobbies", "She enjoys mentoring students, exploring new technologies, and working on hands-on data science projects during weekends.")
faria.define("teaching_style", "She is known for her patient, friendly, and hands-on approach to teaching. She often uses real-world examples and visual aids to make complex ideas easier.")
faria.define("goals", "Faria aspires to transition into educational data science, where she can use data to improve learning outcomes and school systems.")
faria.define("personality", "She is empathetic, approachable, and always curious to learn new things.")
```
```Python
john = TinyPerson("John")
john.define("age", 27)
john.define("nationality", "British")
john.define("occupation", "He is an ambitious university student currently exploring different areas of Data Science as part of his degree.")
john.define("interests", "John is especially interested in data visualization, basic statistics, and learning to program using tools like Python, R, and SQL.")
john.define("study_goals", "He wants to eventually become a data analyst, working with business or educational data to make informed decisions.")
john.define("learning_style", "He learns best through clear visualizations, practical examples, and step-by-step guidance.")
john.define("personality", "John is inquisitive, friendly, and sometimes a bit shy when asking questions, but he's very eager to learn.")
```
# Create a shared environment, To instantiate a conversation between two personas above, we will need `TinyWorld` function.
```python
world = TinyWorld("Classroom", [faria, john])
world.make_everyone_accessible()
```

# Seed the conversation with a natural student-teacher question. Use the method `.listen_and_act` to have a conversation with the persona defined above
```python
faria.listen("Hey Faria, I wanted to get help for my data science homework so I can understand it better. I'm especially struggling with choosing the right type of chart for my dataset.")
```
# Run the simulation for 3 steps to observe a more thoughtful exchange
```python
world.run(3)
```

###  Questions need to be answered:
# 1. How to install tinytroupe packages?

# Answer: To install the TinyTroupe package, one must first clone the repository from GitHub using the command git clone https://github.com/microsoft/tinytroupe. After cloning the repository, the user should navigate into the project directory by executing cd tinytroupe. Inside this directory, there is a requirements.txt file which lists the dependencies required by the package. These can be installed using the command pip install -r requirements.txt. Additionally, if the project includes a setup.py or a pyproject.toml file, it is recommended that the user installs the package itself by running pip install .. This will ensure that TinyTroupe is fully integrated into the user’s Python environment. These steps reflect a typical installation process for Python-based projects hosted on GitHub.



# 2. What is Turing Test? In today's world with Large Language Models (LLMs), what is the definition of Turing Test?

# Answer: The Turing Test, originally proposed by Alan Turing in 1950, serves as a benchmark for assessing a machine’s ability to exhibit human-like intelligence. In its classical form, the test involves a human evaluator interacting with both a machine and another human, without knowing which is which. If the evaluator cannot reliably distinguish the machine from the human based solely on their responses, the machine is considered to have passed the Turing Test.

# In today’s context—especially with the development and widespread use of Large Language Models (LLMs) such as GPT-4 and beyond—the definition of the Turing Test has evolved. While LLMs are now capable of producing text that is often indistinguishable from that of a human, the modern interpretation of the Turing Test involves more than linguistic mimicry. It encompasses the model’s ability to maintain coherent dialogue, reason logically, retain contextual information, and exhibit adaptive responses. Therefore, while many LLMs might pass the traditional version of the test, contemporary applications demand a more nuanced evaluation of machine intelligence—one that includes depth, consistency, and contextual awareness.




# 3. Create a simulation of your own topic and show me the transcript. This implies define at least two personas of your own choice with conflict built in and observe their conversation. You can simply copy/paste the conversation in a .md file. Please comment on the transcript whether you think the Turing Test is passed.

The following is my conversation:

USER --> Faria: [CONVERSATION] 
          > Hey Faria, I wanted to get help for my data science homework so I can understand it
          > better. I'm especially struggling with choosing the right type of chart for my dataset.
TinyPerson(name='Faria')
>>> 
>>> # Run the simulation for 3 steps to observe a more thoughtful exchange
>>> world.run(3)
──────────────────────────────────────────────────────────────── Classroom step 1 of 3 ────────────────────────────────────────────────────────────────
Faria acts: [THINK] 
           > I need to help with the data science homework. Choosing the right type of chart is
           > crucial for understanding the data. I should ask about the dataset and what kind of
           > information they want to convey with the chart.
Faria acts: [TALK] 
           > Sure! I'd be happy to help you with your data science homework. Can you tell me more
           > about your dataset and what kind of information you're trying to convey with the chart?
Faria acts: [DONE] 

Faria --> John: [CONVERSATION] 
           > Sure! I'd be happy to help you with your data science homework. Can you tell me more
           > about your dataset and what kind of information you're trying to convey with the chart?
John acts: [THINK] 
          > Faria is offering to help me with my data science homework. I need to provide details
          > about my dataset and what I want to convey with the chart. I should think about the
          > specific aspects of the dataset that are important for the chart.
John acts: [TALK] 
          > Thank you, Faria! I really appreciate your help. The dataset I'm working with contains
          > information about student performance in various subjects. I'm trying to create a chart
          > that shows the correlation between study hours and exam scores. Do you have any
          > suggestions on how to visualize this effectively?
John acts: [DONE] 

John --> Faria: [CONVERSATION] 
          > Thank you, Faria! I really appreciate your help. The dataset I'm working with contains
          > information about student performance in various subjects. I'm trying to create a chart
          > that shows the correlation between study hours and exam scores. Do you have any
          > suggestions on how to visualize this effectively?
──────────────────────────────────────────────────────────────── Classroom step 2 of 3 ────────────────────────────────────────────────────────────────
Faria acts: [THINK] 
           > John's dataset is about student performance, and he wants to visualize the correlation
           > between study hours and exam scores. A scatter plot would be a good choice for this, as
           > it can effectively show the relationship between two continuous variables. I should
           > explain this to him and suggest he also consider adding a trend line to highlight the
           > correlation.
Faria acts: [TALK] 
           > For your dataset, I recommend using a scatter plot to visualize the correlation between
           > study hours and exam scores. This type of chart will allow you to see how the two
           > variables relate to each other. You might also consider adding a trend line to
           > highlight the correlation more clearly. Would you like to know how to create that in
           > your data visualization tool?
Faria acts: [DONE] 

Faria --> John: [CONVERSATION] 
           > For your dataset, I recommend using a scatter plot to visualize the correlation between
           > study hours and exam scores. This type of chart will allow you to see how the two
           > variables relate to each other. You might also consider adding a trend line to
           > highlight the correlation more clearly. Would you like to know how to create that in
           > your data visualization tool?
John acts: [THINK] 
          > Faria suggested using a scatter plot to visualize the correlation between study hours
          > and exam scores, which sounds like a great idea. I should ask for guidance on how to
          > create that trend line in my data visualization tool.
John acts: [TALK] 
          > Yes, I would love to know how to create that scatter plot with a trend line in my data
          > visualization tool! What steps should I follow?
John acts: [DONE] 

John --> Faria: [CONVERSATION] 
          > Yes, I would love to know how to create that scatter plot with a trend line in my data
          > visualization tool! What steps should I follow?
──────────────────────────────────────────────────────────────── Classroom step 3 of 3 ────────────────────────────────────────────────────────────────
2025-04-06 00:57:11,811 - tinytroupe - ERROR - [2] Error: 'stream'
2025-04-06 00:57:16,814 - tinytroupe - ERROR - [3] Error: 'stream'
2025-04-06 00:57:21,816 - tinytroupe - ERROR - [4] Error: 'stream'
2025-04-06 00:57:26,819 - tinytroupe - ERROR - [5] Error: 'stream'
2025-04-06 00:57:26,819 - tinytroupe - ERROR - Failed to get response after 5.0 attempts.
2025-04-06 00:57:54,454 - tinytroupe - ERROR - [2] Error: 'stream'
2025-04-06 00:57:59,457 - tinytroupe - ERROR - [3] Error: 'stream'
2025-04-06 00:58:04,460 - tinytroupe - ERROR - [4] Error: 'stream'
2025-04-06 00:58:09,463 - tinytroupe - ERROR - [5] Error: 'stream'
2025-04-06 00:58:09,463 - tinytroupe - ERROR - Failed to get response after 5.0 attempts.
2025-04-06 00:58:37,152 - tinytroupe - ERROR - [2] Error: 'stream'
2025-04-06 00:58:42,155 - tinytroupe - ERROR - [3] Error: 'stream'
2025-04-06 00:58:47,158 - tinytroupe - ERROR - [4] Error: 'stream'
2025-04-06 00:58:52,161 - tinytroupe - ERROR - [5] Error: 'stream'
2025-04-06 00:58:52,161 - tinytroupe - ERROR - Failed to get response after 5.0 attempts.
2025-04-06 00:59:19,811 - tinytroupe - ERROR - [2] Error: 'stream'
2025-04-06 00:59:24,814 - tinytroupe - ERROR - [3] Error: 'stream'
2025-04-06 00:59:29,817 - tinytroupe - ERROR - [4] Error: 'stream'
2025-04-06 00:59:34,820 - tinytroupe - ERROR - [5] Error: 'stream'
2025-04-06 00:59:34,820 - tinytroupe - ERROR - Failed to get response after 5.0 attempts.
2025-04-06 01:00:02,370 - tinytroupe - ERROR - [2] Error: 'stream'
2025-04-06 01:00:07,373 - tinytroupe - ERROR - [3] Error: 'stream'
2025-04-06 01:00:12,376 - tinytroupe - ERROR - [4] Error: 'stream'
2025-04-06 01:00:17,379 - tinytroupe - ERROR - [5] Error: 'stream'
2025-04-06 01:00:17,379 - tinytroupe - ERROR - Failed to get response after 5.0 attempts.

# Answer: In the simulation conducted, two personas were defined: Faria and John. John, a student, seeks assistance with a data science assignment, particularly in selecting an appropriate chart to visualize the relationship between study hours and exam scores. Faria, the helpful agent in the simulation, responds thoughtfully by first requesting additional context about the dataset. Upon learning more, she suggests that a scatter plot would be the most appropriate method to visualize the correlation. She also recommends including a trend line to enhance the clarity of the relationship between variables. The conversation continues for several turns, with John acknowledging the suggestion and asking for guidance on how to implement the recommended visualization.

# Despite encountering technical errors toward the end of the simulation—related to streaming and not the dialogue itself—the interaction between the personas remained coherent, relevant, and logically structured. Faria’s responses demonstrated an understanding of the user’s needs and provided targeted, practical advice. The dialogue felt natural and free of robotic or repetitive behavior. As such, it is reasonable to conclude that this simulation does pass the Turing Test, at least within the scope of this academic interaction. The personas communicated in a manner that would be difficult to distinguish from a real conversation between two human individuals.



