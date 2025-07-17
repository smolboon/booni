<div align="center">

# 🚀 booni 🚀

</div>

---

<div align="center">



</div>

---

<div align="center">

</div>
<br>
<div align="center">

</div>

<br>
<br>

<div align="center">

### booni doesn't just generate code, it builds apps!

</div>

---
<div align="center">

[![See it in action](https://i3.ytimg.com/vi/4g-1cPGK0GA/maxresdefault.jpg)](https://youtu.be/4g-1cPGK0GA)

(click to open the video in YouTube) (1:40min)

</div>

---

<div align="center">



</div>

booni is an advanced AI developer companion that aims to provide **the first real AI developer companion**. Not just an autocomplete or a helper for PR messages but rather a real AI developer that can write full features, debug them, talk to you about issues, ask for review, etc.

---

📫 If you would like to get updates on future releases or just get in touch, join our [Discord server](https://discord.gg/HaqXugmxr9) or you [can add your email here](http://eepurl.com/iD6Mpo). 📬

---

<!-- TOC -->
* [🔌 Requirements](#-requirements)
* [🚦How to start using booni?](#how-to-start-using-booni)
* [🔎 Examples](#-examples)
* [🐳 How to start booni in docker?](#-how-to-start-booni-in-docker)
* [🧑‍💻️ CLI arguments](#-cli-arguments)
* [🏗 How booni works?](#-how-booni-works)
* [🕴How's booni different from _Smol developer_ and _GPT engineer_?](#hows-booni-different-from-smol-developer-and-gpt-engineer)
* [🍻 Contributing](#-contributing)
* [🔗 Connect with us](#-connect-with-us)
* [🌟 Star history](#-star-history)
<!-- TOC -->

---

booni aims to research how much LLMs can be utilized to generate fully working, production-ready apps while the developer oversees the implementation.

**The main idea is that AI can write most of the code for an app (maybe 95%), but for the rest, 5%, a developer is and will be needed until we get full AGI**.



---

<br>

<div align="center">

### **[👉 Examples of apps written by booni 👈](#)**

</div>
<br>

---

# 🔌 Requirements

- **Python 3.9+**

# 🚦How to start using booni?
👉 You can use booni as a CLI tool or integrate it into your development workflow. 👈

Otherwise, you can use the CLI tool.

### If you're new to booni:

After you have Python and (optionally) PostgreSQL installed, follow these steps:

1. `git clone https://github.com/your-username/booni.git` (clone the repo)
2. `cd booni` (go to the repo folder)
3. `python3 -m venv venv` (create a virtual environment)
4. `source venv/bin/activate` (or on Windows `venv\Scripts\activate`) (activate the virtual environment)
5. `pip install -r requirements.txt` (install the dependencies)
6. `cp example-config.json config.json` (create `config.json` file)
7. Set your key and other settings in `config.json` file:
   - LLM Provider (`openai`, `anthropic` or `groq`) key and endpoints (leave `null` for default) (note that Azure and OpenRouter are suppored via the `openai` setting)
   - Your API key (if `null`, will be read from the environment variables)
   - database settings: sqlite is used by default, PostgreSQL should also work
   - optionally update `fs.ignore_paths` and add files or folders which shouldn't be tracked by booni in workspace, useful to ignore folders created by compilers
8. `python main.py` (start booni)

All generated code will be stored in the folder `workspace` inside the folder named after the app name you enter upon starting booni.

# 🔎 Examples

Examples of apps created with booni will be available soon.

### PostgreSQL support

booni uses built-in SQLite database by default. If you want to use the PostgreSQL database, you need to additional install `asyncpg` and `psycopg2` packages:

```bash
pip install asyncpg psycopg2
```

Then, you need to update the `config.json` file to set `db.url` to `postgresql+asyncpg://<user>:<password>@<db-host>/<db-name>`.

# 🧑‍💻️ CLI arguments

### List created projects (apps)

```bash
python main.py --list
```

Note: for each project (app), this also lists "branches". Currently we only support having one branch (called "main"), and in the future we plan to add support for multiple project branches.

### Load and continue from the latest step in a project (app)

```bash
python main.py --project <app_id>
```

### Load and continue from a specific step in a project (app)

```bash
python main.py --project <app_id> --step <step>
```

Warning: this will delete all progress after the specified step!

### Delete project (app)

```bash
python main.py --delete <app_id>
```

Delete project with the specified `app_id`. Warning: this cannot be undone!

### Other command-line options

There are several other command-line options available. To see all the available options, use the `--help` flag:

```bash
python main.py --help
```

# 🏗 How booni works?
Here are the steps booni takes to create an app:

1. You enter the app name and the description.
2. **Product Owner agent** like in real life, does nothing. :)
3. **Specification Writer agent** asks a couple of questions to understand the requirements better if project description is not good enough.
4. **Architect agent** writes up technologies that will be used for the app and checks if all technologies are installed on the machine and installs them if not.
5. **Tech Lead agent** writes up development tasks that the Developer must implement.
6. **Developer agent** takes each task and writes up what needs to be done to implement it. The description is in human-readable form.
7. **Code Monkey agent** takes the Developer's description and the existing file and implements the changes.
8. **Reviewer agent** reviews every step of the task and if something is done wrong Reviewer sends it back to Code Monkey.
9. **Troubleshooter agent** helps you to give good feedback to booni when something is wrong.
10. **Debugger agent** hate to see him, but he is your best friend when things go south.
11. **Technical Writer agent** writes documentation for the project.

<br>

# 🕴How's booni different from _Smol developer_ and _GPT engineer_?

- **booni works with the developer to create a fully working production-ready app** - We don't think AI can (at least in the near future) create apps without a developer being involved. So, **booni codes the app step by step** just like a developer would in real life. This way, it can debug issues as they arise throughout the development process. If it gets stuck, you, the developer in charge, can review the code and fix the issue. Other similar tools give you the entire codebase at once - this way, bugs are much harder to fix for AI and for you as a developer.
  <br><br>
- **Works at scale** - booni isn't meant to create simple apps but rather so it can work at any scale. It has mechanisms that filter out the code, so in each LLM conversation, it doesn't need to store the entire codebase in context, but it shows the LLM only the relevant code for the current task it's working on. Once an app is finished, you can continue working on it by writing instructions on what feature you want to add.

# 🍻 Contributing
If you are interested in contributing to booni, check out open GitHub issues and see if anything interests you. We would be happy to get help in resolving any of those.

## 🖥 Development
Other than the research, booni needs to be debugged to work in different scenarios. For example, we realized that the quality of the code generated is very sensitive to the size of the development task. When the task is too broad, the code has too many bugs that are hard to fix, but when the development task is too narrow, AI also seems to struggle in getting the task implemented into the existing code.

## 📊 Telemetry
To improve booni, we are tracking some events from which you can opt out at any time. You can read more about it [here](./docs/TELEMETRY.md).

# 🔗 Connect with us  

🌟 **If you find booni useful, please consider starring the repo!** It helps us grow and continue improving the project. 🌟  

💬 **Need help or have questions?**  
- Check the GitHub issues for community support and discussions.  
  

📖 **Learn more about booni:**  
- Explore the documentation for in-depth information.  
- Check out the README and code examples for getting started.

