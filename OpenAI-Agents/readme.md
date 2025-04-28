* https://pypi.org/project/openai-agents/
    * https://github.com/openai/openai-agents-python
    * https://github.com/JAlcocerT/openai-agents-python


> You can also do MCP with openai agents

```sh
#git clone https://github.com/openai/openai-agents-python
git clone https://github.com/JAlcocerT/openai-agents-python
cd examples/basic
```

---

## Env Setup


```sh
#python -m venv solvingerror_venv #create the venv
python3 -m venv oaiagent_venv #create the venv

#solvingerror_venv\Scripts\activate #activate venv (windows)
source oaiagent_venv/bin/activate #(linux)
```

**Install dependencies** with:

```sh
pip install openai-agents==0.0.10
#pip install beautifulsoup4 openpyxl pandas numpy==2.0.0
pip install -r requirements.txt #all at once
#pip freeze | grep langchain

#pip show beautifulsoup4
pip list
#pip freeze > requirements-output.txt #generate a txt with the ones you have!
```

```sh
source .env

#export OPENAI_API_KEY="your-api-key-here"
#set OPENAI_API_KEY=your-api-key-here
#$env:OPENAI_API_KEY="your-api-key-here"
echo $OPENAI_API_KEY
```