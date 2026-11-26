# From 2,100 Messy Orders to a Live AI-Built System in 2 Hours

Nov 25, 2026&#32;

## What you will build today

In two hours you will turn 2,100 messy food-delivery orders into a cleaned, tested, working dashboard, using AI agents inside Google Antigravity while you stay in charge as the engineer.

The agent does a lot of the typing. You do the thinking: you decide the rules, you read what the agent wrote, and you prove that it is right. That split is the real skill of this session, and it is the way professional teams are starting to work.

**By the end of the session you will have:**

- A project folder on your laptop with its own Python virtual environment
- Python code that you typed yourself, and code an agent wrote that you reviewed line by line
- A cleaning pipeline driven by a written list of rules (a "contract")
- A test suite that guards those rules
- A live dashboard in your browser that an agent opened, clicked through and checked on its own
- A system that survived a surprise file thrown at it halfway through the session

**Four moments to watch for.** You will see one sentence turn into a working app. You will see three agents work at the same time. You will catch the agent quietly deleting real data. And you will watch your finished system break on new data, then fix it in minutes.

## Pre-requisites: install before the session

Do everything in this section before the session begins, because class assumes it is already done. Follow the install guides below, then tick every box. If a step fails, tell your instructor early; most install problems take two minutes to fix when caught early and twenty when caught late.

- [ ] Laptop charged, charger in your bag, internet working
- [ ] Python 3.10 or newer installed (3.11 or 3.12 is best)
- [ ] VS Code with the Antigravity extension installed, and signed in with a personal Gmail account
- [ ] A second Gmail account ready as a backup, with its password at hand
- [ ] Pre-flight test done: the agent replied inside Antigravity (last step of the install guide below)
- [ ] A folder named `food-lab` created in Documents (or anywhere you can find it)

### Check your Python version

Open a terminal (Terminal on Mac, PowerShell on Windows), type the command for your system and press Enter.

```bash
# Mac
python3 --version

# Windows (PowerShell)
py --version
```

You should see something like `Python 3.12.4`. If you see a number below 3.10, or an error such as "command not found", install Python from python.org. On Windows, tick the box that says **Add python.exe to PATH** on the first installer screen; forgetting it is the most common reason `python` is not recognised later.

### Install Python (only if the check above failed)

**On Windows:**

1. Go to **python.org/downloads** and download the latest stable Python 3 installer (3.11 or newer).
2. Run it. On the very first screen, tick **Add python.exe to PATH**, then click **Install Now**.
3. When it finishes, close PowerShell, open a new one and run `py --version` again.

**On Mac:**

1. Go to **python.org/downloads** and download the latest stable Python 3 installer for macOS (3.11 or newer).
2. Open the downloaded file and click through the installer.
3. Close Terminal, open a new one and run `python3 --version` again.

Always open a **new** terminal window after installing. An old window does not know that Python now exists.

### Install VS Code and the Antigravity extension

1. Install **Visual Studio Code** from **code.visualstudio.com** if you do not have it already. The extension needs VS Code 1.90 or later, and it works on Windows and Mac.
2. Open VS Code and click the **Extensions** icon in the left sidebar (or press Ctrl+Shift+X on Windows, Cmd+Shift+X on Mac). Search for **Google Antigravity**, choose the one published by **Google**, and click **Install**. Other extensions with similar names are not the real one.
3. Click the **Antigravity icon** in the Activity Bar (the narrow strip of icons on the far left) and choose **Sign In**. Finish signing in in your browser with your personal Google account. Your college account may be blocked, so use a personal one. On the first launch the extension installs a small background helper called `agy` by itself, so wait for it to finish.
4. Open your folder: choose **File**, then **Open Folder**, and select your `food-lab` folder.
5. The Antigravity chat opens in a side panel. Press Ctrl+L (Cmd+L on Mac) to open or focus it, and Ctrl+Shift+L (Cmd+Shift+L) to start a new conversation. When the agent proposes a change, Alt+Enter (Option+Enter) accepts it and Alt+Shift+Enter (Option+Shift+Enter) rejects it. Press Esc to stop an agent that is running.

**Pre-flight test (2 minutes).** With `food-lab` open, send this to the agent: `Create a file called hello.py that prints "Antigravity is ready" and run it.` If it replies and you see that sentence in the output, your sign-in, quota and setup all work. Then sign out and sign in once with your backup Gmail account too, so you know the backup works before you need it.

You may also see an **Open in Agents** button at the top of VS Code (shortcut Ctrl+Shift+A). It opens the agents in a separate, larger window, and you will use it in Block 4. Chrome is optional. The browser agent can use Google Chrome, and recent versions on personal accounts use a built-in browser instead.

Menu names change as Antigravity updates, so your screen may differ slightly from what is described here. If something does not match, ask the agent "where do I find X?" or raise your hand.

### Why you need a second Gmail account

The free plan limits how much each account can use. With a whole class prompting at once, someone will hit the limit. Your work lives in the `food-lab` folder on your own laptop, not inside your Google account, so if you run out you can sign out, sign in with your backup account and carry on without losing anything.

## Your two hours at a glance

&#91;embedded content: session map · 7 blocks, 120 minutes\]

Four blocks are highlighted because each one holds a surprise: the demo, the data traps, three agents working at once and the curveball. Block 6 is the quiet one, and it is where the learning settles. Every block ends with a checkpoint, so you always know whether you are on track.

## Block 0: The hook (minutes 0 to 10)

Hands off the keyboard for this one. Your instructor types a single sentence into Antigravity, and you watch an agent build a small app, launch it, open a browser, click through it and show screenshots as proof that it works.

**Write down a prediction before the demo ends.** Take out a notebook and finish this sentence: "Out of 10 decisions the agent makes while cleaning messy data, about \_\_\_ will be wrong." You will come back to this number in Block 6.

### Three layers worth knowing

- **Model.** A very large pattern predictor. Give it text, it predicts what text should come next. On its own it cannot open a file, run a command or check its own answer.
- **Agent.** A model plus tools, running in a loop of plan, act, check. It can read your files, edit them, run commands in a terminal, look at the result, notice an error and try again.
- **System.** The agent plus everything that makes the result trustworthy: your rules, your tests, your data and the people who verify the output. A system is what still works next month.

Today you move through all three layers. You start by watching an agent, you end by owning a system.

### What to notice during the demo

1. Before writing any code, the agent produces a plan and a task list. Where does it ask for your approval?
2. When it finishes, how does it know the app works? What evidence does it show you?
3. Which parts of the work did the agent do alone, and which parts needed a human decision?

**Checkpoint:** you can explain, in one sentence to the person next to you, the difference between a model and an agent.

## Block 1: Set up your workspace (minutes 10 to 25)

Every project needs a clean place to live. In Python that place is a **virtual environment**: a private toolbox for this one project. Packages you install into it stay in it, so a version clash in one project can never break another, and deleting the folder removes everything without touching the rest of your laptop.

### Step 1: Open your project

1. In VS Code, choose **File**, then **Open Folder**, and select your `food-lab` folder.
2. Open the Antigravity chat by clicking the Antigravity icon in the Activity Bar, or by pressing Ctrl+L (Cmd+L on Mac).
3. If you are asked how much freedom to give the agent, pick the option where you review commands before they run. You will see exactly what it does to your laptop, and that habit matters more than the speed you would gain.

### Step 2: Give the agent its first job

Copy this prompt into the agent panel and send it.

```text
Create a Python virtual environment named .venv inside this folder.
Install pandas and pytest into it.
Then write a file called env_check.py that prints my operating system,
the Python version and the pandas version, followed by the line ENV OK.
Run it using the virtual environment's Python and show me the output.
Before you run any command, tell me in one sentence what it does.
```

Watch what happens. The agent should explain its commands, ask permission, run them, and report back. Read each command before you approve it. You are the engineer on call, so nothing runs on your machine without you knowing why.

### Step 3: Verify it yourself

Do not take the agent's word for it. Open a terminal inside Antigravity (or your own terminal, in the `food-lab` folder) and run the check with your own hands.

```bash
# Mac
.venv/bin/python env_check.py

# Windows (PowerShell)
.venv\Scripts\python env_check.py
```

**What this command does.** `.venv/bin/python` (on Windows, `.venv\Scripts\python`) is the copy of Python that lives inside your project's virtual environment. `env_check.py` is the small script the agent wrote. Together they run that script, which prints your operating system, your Python version and your pandas version. Using the environment's own Python proves that pandas was installed in the right place. The command only reads information and changes nothing.

You should see three facts about your machine and then `ENV OK`.

**Checkpoint:** `ENV OK` is on your screen, and you ran the command yourself, not just the agent.

### If it does not work

- **"python is not recognized" on Windows.** Use `py` instead of `python`, or ask the agent to find the correct Python command for your machine.
- **PowerShell says running scripts is disabled.** You do not need to "activate" the environment at all. Call the environment's Python directly, exactly as shown in Step 3.
- **Mac asks for permission to install developer tools.** Say yes and wait a few minutes.

### Fast finishers

Ask the agent: "Explain every command you just ran in one line each, and tell me what would have gone wrong if we had skipped the virtual environment." Compare its answer with the explanation at the top of this block.

## Block 2: Python, first by hand and then with the agent (minutes 25 to 50)

The agent can write Python faster than you can. That is exactly why you must be able to read Python well enough to catch its mistakes. In this block you write a little code with your own hands first, so that the agent's code later is something you can judge, not just trust.

### Part A: Create today's dataset

The data is a made-up but realistic export of food-delivery orders from Indian cities, built to be messy in the ways real data is messy. Everyone gets exactly the same file, so everyone's numbers can be compared.

1. In Antigravity, create a new file called `gen_messy_orders.py` in your `food-lab` folder.
2. Copy the script from **Appendix: the data generator** at the bottom of this page, paste it in and save.
3. Run it in the terminal:

```bash
# Mac
.venv/bin/python gen_messy_orders.py --batch 1

# Windows (PowerShell)
.venv\Scripts\python gen_messy_orders.py --batch 1
```

**What this command does.** `.venv/bin/python` (on Windows, `.venv\Scripts\python`) is the Python inside your virtual environment. `gen_messy_orders.py` is the script you just saved. `--batch 1` is an option that tells the script to build the first file. Together they run the script, which invents 2,100 food-delivery orders, with a little mess built in, and saves them as a new file called `orders_raw.csv` in your folder. It does not use the internet and it does not touch any other file.

You should see `Wrote 2100 rows to orders_raw.csv`, and a new file with that name appears in your folder. Open it and scroll for a minute. Look at the city names and the empty cells. Already something looks off, and that is on purpose.

### Part B: Write your first program by hand

Create `explore.py` and **type these lines yourself, without copy and paste**. Typing slows you down just enough to notice what each line does.

```python
import pandas as pd

df = pd.read_csv("orders_raw.csv")

print("Rows and columns:", df.shape)
print()
print(df.head(5).to_string())
print()
print("Missing values per column:")
print(df.isna().sum())
print()
print("Exact duplicate rows:", df.duplicated().sum())
print("Different spellings in the city column:", df["city"].nunique())
print()
print(df["city"].value_counts().head(10))
```

What the new ideas mean:

- `pd.read_csv` reads a spreadsheet-style file into a **DataFrame**, a table with named columns that you can ask questions about.
- `df.shape` is the table's size as (rows, columns).
- `df.isna().sum()` counts empty cells in each column.
- `df["city"].value_counts()` counts how often each distinct value appears.

Run it with `.venv/bin/python explore.py` (Mac) or `.venv\Scripts\python explore.py` (Windows).

**What this does.** Running `explore.py` reads `orders_raw.csv` into a DataFrame, then prints the size of the table, its first five rows, how many cells are empty in each column, how many rows are exact duplicates, and how many different spellings the `city` column has. It only looks at the data. It does not change `orders_raw.csv`.

**The program, line by line.** Match each line of your code with what it printed.

| Your code | What it does | What you see in the output |
| --- | --- | --- |
| `import pandas as pd` | Loads the pandas library and gives it the short nickname `pd`. | Nothing is printed. |
| `df = pd.read_csv("orders_raw.csv")` | Reads the file into a table and names that table `df`. If the file name is wrong, Python stops here with a FileNotFoundError. | Nothing is printed. |
| `print("Rows and columns:", df.shape)` | `df.shape` is the size of the table as (rows, columns). | `Rows and columns: (2100, 10)` |
| `print(df.head(5).to_string())` | `head(5)` takes the first five rows. `to_string()` prints every column on one wide line instead of hiding some. | The five-row table. `NaN` means an empty cell. |
| `print("Missing values per column:")` | Prints a label so the numbers below make sense. | The label itself. |
| `print(df.isna().sum())` | `isna()` marks every empty cell as True. `sum()` counts the Trues in each column. | `delivery_minutes 106, rating 159`, and 0 for the rest. `dtype: int64` only says the counts are whole numbers. |
| `print("Exact duplicate rows:", df.duplicated().sum())` | `duplicated()` marks a row True if an identical row appeared earlier. `sum()` counts them. | `Exact duplicate rows: 100` |
| `print("Different spellings in the city column:", df["city"].nunique())` | `df["city"]` picks out one column. `nunique()` counts how many different values it holds. | `Different spellings in the city column: 24` |
| `print(df["city"].value_counts().head(10))` | `value_counts()` counts how often each spelling appears, most common first. `head(10)` keeps the top ten. | `Bengaluru` `343 down to mumbai 68`. The last line, `Name: count, dtype: int64`, is pandas describing the column. |

The blank `print()` lines in your file only add empty lines between the sections.

**Three things your own output already shows.** Look at the five rows again. The same city appears in different forms, such as `hyderabad` and `Mumbai`. Some `rating` and `delivery_minutes` cells are empty (NaN), which is also why those columns show `4.0` instead of `4`: empty cells force pandas to store the column with decimals. And the output counts 100 exact duplicate rows. You have just spotted the defects you will fix in Block 3.

**Checkpoint:** your output matches these facts. If a number differs, find out why before moving on, because every later block depends on it.

| What you should see | Value |
| --- | --- |
| Rows and columns | 2100 rows, 10 columns |
| Exact duplicate rows | 100 |
| Empty cells in delivery\_minutes and rating | 106 and 159 |
| Different spellings in the city column | 24 |

Twenty-four spellings for what should be six cities. That single number is the whole reason data preprocessing exists.

### Part C: Break it on purpose

Real programmers spend more time reading errors than writing code, so practise on an error you caused yourself.

1. In `explore.py`, change `orders_raw.csv` to `orders.csv` and run it again. It fails with a long red message.
2. Read the **last line** of the message first, because that is where Python states the actual problem. Then read upward to see which line of your code triggered it.
3. Copy the whole error into the agent with this prompt:

```text
Here is an error from my program. Explain in plain English what went wrong
and why. Do not fix it yet. Then tell me which single line I should change.

<paste the error here>
```

4. Fix it yourself by changing the name back, and run the program again.

Notice what just happened: the agent explained, and you fixed. That pattern will repeat all session.

### Part D: Review the agent's code

Now let the agent change your program, and practise being the reviewer.

```text
In explore.py, add code that prints how many different restaurants there are
and the share of orders (as a percentage) for each payment_method.
Change nothing else in the file. Show me the changes before you apply them.
```

Before you accept the change, ask yourself three review questions:

1. Did it touch any line I did not ask about?
2. Did it add an import or a function I do not understand?
3. If I deleted the explanation and only had the code, could I still tell what it does?

**Checkpoint:** `explore.py` runs without errors and prints the new information. You can point to the exact lines the agent added.

## Block 3: Clean the data and prove it (minutes 50 to 75)

Data preprocessing means turning raw data into data you can trust. Analysts spend most of their time here, and it is also where AI agents make their quietest and most expensive mistakes. This block teaches you to give the agent clear rules and then audit what it did.

### Step 1: Hunt for defects

Open `orders_raw.csv` and run more questions through pandas, or ask the agent to help you look. There are four kinds of defect hidden in the file. Tick each one when you have seen it with your own eyes.

- [ ] Exact duplicate rows
- [ ] The same city written in different ways (Delhi, DELHI, delhi, and "Delhi " with a trailing space)
- [ ] Empty cells in rating and delivery\_minutes
- [ ] Impossible quantities: zero or negative

### Step 2: Write the cleaning contract before any code

This is the most important habit of the session. Before you let an agent touch the data, you write the rules in plain English. A written contract gives you something to test the agent against. Without it you are only hoping.

Here is the contract for today. Read every line and make sure you understand why it exists.

1. Remove exact duplicate rows and keep the first copy.
2. Drop any row where quantity is zero or negative, because the order cannot be trusted.
3. Make every city name consistent: remove extra spaces and capitalise it, so delhi, DELHI and "Delhi " all become Delhi.
4. Convert order\_date to a real date.
5. Leave an empty rating or delivery\_minutes empty. Never fill it with a made-up number, and never drop a row only because of it.
6. Never delete a row for any reason that is not in the rules above.

### Step 3: Give the agent the contract

Copy this prompt, then paste the six rules from Step 2 where indicated.

```text
Write clean.py with a function clean(df) that cleans the raw orders data in
orders_raw.csv. Follow this contract exactly:

<paste the six rules here>

Running clean.py should save clean_orders.csv and print how many rows each
rule removed.
Use the .venv in this folder for all Python and installs.
```

Let the agent work. When it shows you its plan, **read it**, and check that every rule in your contract appears in the plan. Approve it only when you are satisfied.

### Step 4: Audit the agent

Run `clean.py` yourself. Then check your results against the numbers below. These come from following the contract exactly, so a difference means something is wrong, in the agent's code or in your reading of the contract.

| Checkpoint number | Correct value |
| --- | --- |
| Rows at the start | 2,100 |
| Rows after removing duplicates | 2,000 |
| Rows after dropping bad quantities | 1,980 |
| Order dates | 1 January 2025 to 31 March 2025 |
| Different cities | 6 |
| Rows with an empty rating | 150 |
| Rows with an empty delivery\_minutes | 99 |
| Total order value | 1,043,160.92 rupees |
| Average delivery time | 33.45 minutes |
| Average rating | 4.01 |

**One trap to look for.** AI agents love to "tidy up" data in ways that look smart. If your row count is below 1,980, the agent probably deleted real orders. The usual cause is dropping every row that has an empty rating or delivery time. Those are real orders, and rule 5 says to keep them.

The dates give you a second check. Every date must fall between 1 January and 31 March 2025. If your range is different, the agent has parsed or filtered the dates wrongly.

If a number is wrong, do not fix it by hand. Tell the agent which number is wrong and what you expected, and ask it to find the cause:

```text
The cleaned data has <your number> rows but the contract says it should have
1,980. Find which step removed the extra rows and explain why before changing
anything.
```

**Checkpoint:** every number in the table matches. Write down the one thing the agent got wrong on its first try, if anything. It is useful evidence for Block 6.

## Block 4: Design the system, then build it with three agents at once (minutes 75 to 100)

A cleaning script is not yet a system. A system has parts with clear jobs, agreed ways for those parts to talk, and checks that tell you when something breaks. In this block you act as the architect: you design first, then you hand different parts to different agents and let them work in parallel.

### Part A: Draw the architecture before building anything

An **architecture** is three things written down before any code: the parts of your system, the one job each part does, and how the parts pass information to each other. Teams draw it first because changing a drawing takes seconds, while changing finished code takes hours.

Your goal in this block is a dashboard in your browser that shows numbers from your cleaned orders. Work through three short steps, in order.

**Step 1 (2 minutes, no laptop).** On paper or in a notes app, draw a box for each part you think you need to get from `orders_raw.csv` to a dashboard in the browser. Write one job under each box, such as "cleans the data". Do not look at the map below yet. Your drawing does not need to match it.

**Step 2 (1 minute).** Now compare your drawing with the map below. Read it as a story. The raw files go into `pipeline.py`. The pipeline calls `clean.py`, which holds the rules you wrote in Block 3. The pipeline then writes one file, `data.json`. The dashboard reads only that file. The tests guard `clean.py`, and a browser agent opens the dashboard and checks it.

**Step 3 (2 minutes, with your neighbour).** Decide which parts two people could build at the same time, and what they would have to agree on before starting. Write your answer down, then read the explanation under the map.

&#91;embedded content: system architecture · 7 parts, 3 built in parallel\]

Only the shape of `data.json` ties the dashboard to the rest, which is why the dashboard agent can start before the pipeline agent has finished.

**Check your answer to Step 3.** The pipeline, the tests and the dashboard can all be built at the same time. The only thing their builders must agree on first is the exact shape of `data.json`, because the pipeline writes it and the dashboard reads it. You will write that agreement down in Part B.

### Part B: Agree on the contract between the parts

The dashboard does not need to know how the data was cleaned. It only needs to know the **shape** of `data.json`. If the pipeline and the dashboard both promise to follow the same shape, two agents can build them at the same time without waiting for each other. Engineers call this an interface or a data contract. The numbers below are examples of the shape, not real results.

```json
{
  "total_orders": 1980,
  "total_revenue": 1043160.92,
  "avg_delivery_minutes": 33.45,
  "avg_rating": 4.01,
  "by_city": [
    {"city": "Bengaluru", "orders": 539, "revenue": 282819.48},
    {"city": "Mumbai", "orders": 443, "revenue": 236568.32}
  ],
  "by_cuisine": [
    {"cuisine": "North Indian", "orders": 384, "revenue": 197801.66}
  ],
  "daily_orders": [
    {"date": "2025-01-01", "orders": 26}
  ],
  "payment_split": [
    {"method": "Cash", "orders": 509}
  ]
}
```

### Part C: Launch three agents in parallel

Each agent **owns exactly one file** and may not edit any other. This rule is how real teams avoid stepping on each other, and here it stops three agents from overwriting one another's work. Open a new conversation for each agent in the same project, paste the prompt, and keep all three running.

**Agent A: the pipeline.** It owns `pipeline.py`.

```text
You own pipeline.py only. Do not edit any other file.
First read clean.py and check the real column names of the cleaned data.
Use only those names. Revenue is the sum of the amount column.
Write pipeline.py. It reads one or more CSV files given on the command line
(default orders_raw.csv), cleans them with clean() from clean.py, saves
clean_orders.csv, and writes dashboard/data.json in exactly this shape:

<paste the JSON example here>

The example shows only one or two entries per list. Your file must contain
every city, cuisine, date and payment method, and the real totals.
Use the .venv in this folder for all Python and installs.
```

**Agent B: the tests.** It owns `tests/test_clean.py`.

```text
You own tests/test_clean.py only. Do not edit any other file.
First read clean.py and use only the column names it really uses.
Write pytest tests for clean() in clean.py, one test per rule of this contract:

<paste the six rules here>

If a test fails, do not edit clean.py. Tell me what failed and why.
Use the .venv in this folder for all Python and installs.
```

**Agent C: the dashboard.** It owns `dashboard/index.html`.

```text
You own dashboard/index.html only. Do not edit any other file.
Build a dashboard titled "Food Orders Dashboard" that loads data.json from the
same folder. Show four headline numbers (orders, revenue in rupees, average
delivery minutes, average rating), a bar chart of orders by city, a line chart
of daily orders, and a chart of the payment split. Use every entry in
data.json, and make all charts fully visible on a laptop screen.
Until the real data.json exists, create a sample dashboard/data.json in this
shape to test with:

<paste the JSON example here>
```

Now watch all three work at once in the Antigravity panel. Notice which agents are busy, which are waiting for your approval and which have finished. Approve plans only after reading them.

### Part D: Run it and look at it

When all three agents are done, run each part yourself, in this order.

```bash
# Mac
# 1. Build the data
.venv/bin/python pipeline.py orders_raw.csv
# 2. Run the tests
.venv/bin/python -m pytest
# 3. Serve the dashboard, then open http://localhost:8000
cd dashboard
../.venv/bin/python -m http.server 8000

# Windows (PowerShell)
# 1. Build the data
.venv\Scripts\python pipeline.py orders_raw.csv
# 2. Run the tests
.venv\Scripts\python -m pytest
# 3. Serve the dashboard, then open http://localhost:8000
.venv\Scripts\python -m http.server 8000
```

**What each command does.**

1. `pipeline.py orders_raw.csv` runs the pipeline on the raw file. It loads the orders, cleans them with the rules in `clean.py`, saves the cleaned table as `clean_orders.csv`, writes the summary numbers to `dashboard/data.json`, and prints a short report.
2. `-m pytest` asks Python to run pytest, the testing tool installed in your environment. It runs every test in the `tests` folder and tells you which passed and which failed. It does not change your data.
3. `cd dashboard` moves the terminal into the dashboard folder. `-m http.server 8000` then starts a tiny web server on your laptop that shares that folder at `http://localhost:8000`. Leave it running while you look at the page, and press Ctrl+C to stop it. The `../` in the Mac command means "one folder up", because the virtual environment sits outside the dashboard folder.

On Windows, use `.venv\Scripts\python` in place of `.venv/bin/python`, and `..\.venv\Scripts\python` for step 3. The dashboard needs a small local web server because a browser will not let a page read files from your disk by itself.

**If your numbers do not match.** After the pipeline runs, check the summary it prints. With `orders_raw.csv` you should see **1,980 orders** and a revenue of **1,043,160.92**. If your order count is lower, the pipeline ran but the cleaning step quietly lost rows, most often rows with an empty rating or delivery time. Warnings about deprecated pandas options are harmless, but a lower order count is not. Treat it as a clue and ask the agent to find where the rows were lost.

To fix it, send this to the agent that owns `clean.py`:

```text
My pipeline gives <your number> orders but it should give 1,980. Find where
the rows are being lost and fix it.
```

Then run the pipeline again and compare the totals. The lesson: a program that runs without crashing is not proof that it is right. Always check the numbers.

### Part E: Let the browser agent check the work

You can look at the dashboard yourself, but an agent can check every number in seconds and keep evidence. Send this to a new conversation. The first time, Antigravity may ask your permission to control a browser, which is expected.

```plain
Serve the dashboard folder on port 8000 and open it in the browser. Check that
the numbers on the page match dashboard/data.json and that the browser console
shows no errors. Take screenshots and tell me anything that looks wrong. Use Playwright for browser automation.
```

**Checkpoint:** all your tests pass, the dashboard shows 1,980 orders, and you can open a screenshot taken by the agent as proof. If the agent finds a problem, you have just seen verification work as designed.

## Block 5: The curveball (minutes 100 to 115)

Your system works on today's file. Real systems have to survive tomorrow's file. In this block your instructor hands you a second batch of orders that was exported by a different system, and you find out whether what you built is robust or only lucky.

### Step 1: Receive the new file

```bash
# Mac
.venv/bin/python gen_messy_orders.py --batch 2

# Windows (PowerShell)
.venv\Scripts\python gen_messy_orders.py --batch 2
```

**What this command does.** It is the same generator script as before, but `--batch 2` tells it to build the second file. It writes 600 new orders to `orders_batch2.csv`, imitating an export from a different system, with defects you have not seen yet. Your first file is not touched.

You should see `Wrote 600 rows to orders_batch2.csv`.

### Step 2: Inspect it without the agent

Spend two minutes comparing `orders_batch2.csv` with `orders_raw.csv` by eye or with pandas. Write down every difference you can find. There are three, and none of them were in the first file. Hint: look at the column names, the dates and the cities.

### Step 3: Watch it break

Run the pipeline on both files together.

```bash
# Mac
.venv/bin/python pipeline.py orders_raw.csv orders_batch2.csv

# Windows (PowerShell)
.venv\Scripts\python pipeline.py orders_raw.csv orders_batch2.csv
```

**What this command does.** It runs your pipeline on two files at once. `pipeline.py` loads `orders_raw.csv` and `orders_batch2.csv`, combines them into one table, cleans it, and rebuilds `clean_orders.csv` and `dashboard/data.json`. Nothing in the raw files changes. Expect it to fail at first, because the second file is laid out differently.

It will most likely crash, or worse, run and produce wrong numbers without any warning. Read the last line of the error. Does it match one of the differences on your list?

### Step 4: Update the contract, then fix with discipline

First, extend your written contract with three new rules. The contract grows whenever the world teaches you something new.

7. A column named `amt` means `amount`.
8. `order_date` now includes a time of day. Keep only the date.
9. A city we have never seen before (like Mysuru) is kept and reported. It is never dropped, and it never crashes the pipeline.

Then use this sequence, which is the one professional engineers use. **Write the failing test first, then fix the code, then prove that everything still passes.**

```text
orders_batch2.csv is a new file from another branch. Run the pipeline on both
files and tell me what breaks. Then add tests for these new rules and show that
they fail:

<paste rules 7 to 9 here>

Then update clean.py until all tests pass, old and new. Do not weaken or delete
any existing test. Finally run the pipeline on both files and show me the totals.
Use the .venv in this folder for all Python and installs.
```

The instruction "do not weaken or delete any existing test" matters. When an agent is stuck, one easy way out is to change the test instead of fixing the code. Watching for that is part of your job.

### Step 5: Verify again

Re-run the browser agent prompt from Block 4, Part E. Then compare your numbers with these.

| Checkpoint number | Correct value |
| --- | --- |
| Total orders in the dashboard | 2,580 |
| Total revenue | 1,465,241.58 rupees |
| Different cities | 7 (the original 6, plus Mysuru) |
| Order dates | 1 January 2025 to 30 April 2025 |

**Checkpoint:** all old tests and all new tests pass, and the dashboard shows 2,580 orders.

### What just happened

Your tests were the system's memory. When the new file arrived, they told you immediately what still worked and what did not, and they made sure the fix did not undo yesterday's rules. A system with tests can change safely. A system without them can only change bravely.

## Block 6: Show, reflect, and keep what you learned (minutes 115 to 120)

**Show your dashboard.** Turn to the person next to you and give a 60-second demo of your dashboard. Tell them one thing the agent did well and one thing it got wrong.

**Revisit your prediction.** Back in Block 0 you guessed how many of the agent's decisions would be wrong. Look at your guess again. Then fill in the table below with every mistake, near-miss or surprise you actually caught today. Click into a cell to type.

| What the agent did | How I noticed | Which block |
| --- | --- | --- |
|  |  |  |
|  |  |  |
|  |  |  |

**Three questions to answer in your notebook:**

1. Where did you add the most value as the human in the loop?
2. What would you let an agent do alone next time, and what would you always check yourself?
3. If your instructor had skipped the written contract and the tests, what would have gone wrong first?

## Windows and Mac cheat sheet

The code is identical on both systems. Only the commands around it differ, and almost all the differences are in how you call Python. Keep this table nearby; you will use it in every block.

| Task | Mac | Windows (PowerShell) |
| --- | --- | --- |
| Open a terminal | Terminal | PowerShell |
| Check your Python version | `python3 --version` | `py --version` |
| Create a virtual environment | `python3 -m venv .venv` | `py -m venv .venv` |
| Run a script with the environment's Python | `.venv/bin/python script.py` | `.venv\Scripts\python script.py` |
| Install a package | `.venv/bin/python -m pip install pandas` | `.venv\Scripts\python -m pip install pandas` |
| Run the tests | `.venv/bin/python -m pytest` | `.venv\Scripts\python -m pytest` |
| Folder separator in paths | `/` | `\` |
| Start a new Antigravity conversation | Cmd+Shift+L | Ctrl+Shift+L |
| Jump to the agent panel | Cmd+L | Ctrl+L |
| Find a file by name | Cmd+P | Ctrl+P |
| Stop a program running in the terminal | Ctrl+C | Ctrl+C |

The habit behind the table: always call the Python that lives inside `.venv`, by its full path. That way you never need to "activate" anything, you never run the wrong Python by accident, and you avoid the PowerShell message about scripts being disabled.

## If something goes wrong

Every problem below happens in every class. None of them is a sign that you did something wrong.

| What you see | What to do |
| --- | --- |
| The agent says you have reached your usage limit | Switch to your backup Gmail account (steps below). Your files stay in `food-lab`, so you lose nothing. |
| The agent keeps repeating the same attempt | Stop it. Rewrite your prompt with the exact error pasted in and one clear instruction, then send it again. |
| Your number does not match a checkpoint | Do not fix it by hand. Ask the agent: "Explain why this number is X when I expected Y. Do not change anything yet." |
| The agent wants to delete or overwrite a file you do not recognise | Say no and ask what the file is for. |
| The dashboard is blank | Check that the server is running and that you opened `http://localhost:8000`, not the file itself. Check that `data.json` exists in the `dashboard` folder. |
| You are more than five minutes behind | Ask your neighbour, then raise your hand. Do not stay stuck silently, because later blocks build on earlier ones. |

### Switching to your backup Gmail account

1. Save all your files and note which block you are in.
2. In Antigravity, open the Antigravity panel menu (the three dots), choose Settings, and sign out. The exact menu name may differ on your version.
3. Sign in again through your browser with your backup Gmail account.
4. Reopen your `food-lab` folder with File, then Open Folder. Everything you built is still there.
5. Tell the new agent where you are: "I am in Block 3 and clean.py already exists. Read the files in this folder and continue from there."

### How to make your usage last

- One clear prompt with all the context beats five vague ones.
- Paste the full error once instead of describing it.
- Ask for a plan first. It is cheaper to correct a plan than to undo finished work.
- Name the one file the agent should touch, as the Block 4 prompts do.
- Do the small things yourself. Renaming a file or changing a number takes you seconds and costs no quota.

## What you now know, and what to try next

You started the session watching an agent and finished it owning a system. Here is what you practised, in the language of your course.

| Course topic | What you can now do |
| --- | --- |
| Understanding AI and its applications | Explain the difference between a model, an agent and a system, and say where a human must stay in the loop |
| Setting up the Python environment | Create a virtual environment, install packages into it and prove that it works |
| Programming with Python | Read a traceback, write a short pandas program by hand and review code an agent wrote |
| Data preprocessing | Write a cleaning contract, apply it, and audit the result against known numbers |
| AI architecture and system design | Split a system into parts, define the contract between them and assign each part to its own agent |
| Intelligent Systems Engineering | Protect a system with tests, and change it safely when new data arrives |

### Take-home challenges

Pick the level that suits you. Each one uses only what you built today.

**Bronze: extend the dashboard.** Ask an agent to add a chart of revenue by cuisine. Before you start, write down what the new `data.json` shape must look like, then give that shape to the pipeline agent and the dashboard agent separately, exactly as in Block 4.

**Silver: bring your own mess.** Make a small dirty dataset from your own life (hostel mess feedback, match scores, shared expenses with friends). Plant at least five defects in it on purpose. Write the contract first, then run your pipeline on it, and keep a log of what the agent got wrong.

**Gold: publish it like an engineer.** Put your project in a GitHub repository with a README that explains the architecture, the contract, how to run the tests and a screenshot of the dashboard. A repository like this is a portfolio piece that shows how you work with AI, not only that you can use it.

### Three rules to carry into every project

1. **Write the contract before the code.** If you cannot say what "correct" means in plain English, you cannot tell whether the agent got it right.
2. **Give each agent one job and one file.** Clear ownership is what lets several agents work at once without breaking each other.
3. **Never accept a result without evidence.** Numbers you can check, tests that pass and screenshots from a browser are evidence. "It looks fine" is not.

## Appendix: the data generator

Copy everything in the box below into a new file named `gen_messy_orders.py`, exactly as it is. It uses only Python's built-in libraries, so nothing needs installing. Running it with the same options always produces the same file, which is why everyone's numbers match.

```python
"""Generates the food-delivery orders used in the lab. Standard library only."""
import argparse
import csv
import random
from datetime import date, datetime, timedelta

CITIES = ["Bengaluru", "Mumbai", "Delhi", "Hyderabad", "Chennai", "Pune"]
CITY_WEIGHTS = [28, 24, 20, 12, 9, 7]
RESTAURANTS = ["Biryani Blues", "Dosa Plaza", "Pizza Hub", "Tandoor Tales", "Wok This Way",
               "Burger Barn", "Sweet Tooth", "Chaat Corner", "Momo Magic", "Thali House"]
CUISINES = {"Biryani Blues": "Mughlai", "Dosa Plaza": "South Indian", "Pizza Hub": "Italian",
            "Tandoor Tales": "North Indian", "Wok This Way": "Chinese", "Burger Barn": "Fast Food",
            "Sweet Tooth": "Desserts", "Chaat Corner": "Street Food", "Momo Magic": "Tibetan",
            "Thali House": "North Indian"}
PAYMENTS = ["UPI", "Card", "Cash", "Wallet"]


def batch1(path, n=2000, seed=42):
    rnd = random.Random(seed)
    start = date(2025, 1, 1)
    rows = []
    for i in range(1, n + 1):
        city = rnd.choices(CITIES, weights=CITY_WEIGHTS)[0]
        rest = rnd.choice(RESTAURANTS)
        qty = rnd.choices([1, 2, 3, 4], weights=[40, 30, 20, 10])[0]
        d = start + timedelta(days=rnd.randint(0, 89))
        style = rnd.random()
        if style < 0.15:
            city = city.upper()
        elif style < 0.30:
            city = city.lower()
        elif style < 0.40:
            city = city + " "
        rows.append({
            "order_id": f"ORD{i:04d}",
            "order_date": d.strftime("%Y-%m-%d"),
            "city": city,
            "restaurant": rest,
            "cuisine": CUISINES[rest],
            "quantity": qty,
            "amount": f"{qty * rnd.uniform(120, 420):.2f}",
            "payment_method": rnd.choice(PAYMENTS),
            "delivery_minutes": max(10, int(rnd.gauss(34, 8))),
            "rating": rnd.choices([2, 3, 4, 5], weights=[8, 17, 40, 35])[0],
        })

    for r in rnd.sample(rows, 150):
        r["rating"] = ""
    for r in rnd.sample(rows, 100):
        r["delivery_minutes"] = ""
    for r in rnd.sample(rows, 20):
        r["quantity"] = rnd.choice([0, -1, -2])

    rows.extend(dict(r) for r in rnd.sample(rows, 100))
    rnd.shuffle(rows)

    with open(path, "w", newline="", encoding="utf-8") as f:
        w = csv.DictWriter(f, fieldnames=list(rows[0].keys()))
        w.writeheader()
        w.writerows(rows)
    print(f"Wrote {len(rows)} rows to {path}")


def batch2(path, n=600, seed=7):
    rnd = random.Random(seed)
    start = datetime(2025, 4, 1, 9, 0)
    cities = CITIES + ["Mysuru"]
    rows = []
    for i in range(1, n + 1):
        rest = rnd.choice(RESTAURANTS)
        qty = rnd.randint(1, 4)
        ts = start + timedelta(minutes=rnd.randint(0, 60 * 24 * 29))
        rows.append({
            "order_id": f"ORD{5000 + i}",
            "order_date": ts.strftime("%Y-%m-%d %H:%M"),
            "city": rnd.choice(cities),
            "restaurant": rest,
            "cuisine": CUISINES[rest],
            "quantity": qty,
            "amt": f"{qty * rnd.uniform(130, 450):.2f}",
            "payment_method": rnd.choice(PAYMENTS),
            "delivery_minutes": max(10, int(rnd.gauss(36, 9))),
            "rating": rnd.choice([2, 3, 4, 4, 5, 5]),
        })
    with open(path, "w", newline="", encoding="utf-8") as f:
        w = csv.DictWriter(f, fieldnames=list(rows[0].keys()))
        w.writeheader()
        w.writerows(rows)
    print(f"Wrote {len(rows)} rows to {path}")


if __name__ == "__main__":
    ap = argparse.ArgumentParser()
    ap.add_argument("--batch", type=int, choices=[1, 2], default=1)
    a = ap.parse_args()
    if a.batch == 1:
        batch1("orders_raw.csv")
    else:
        batch2("orders_batch2.csv")
```
