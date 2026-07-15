# ADK Codelab (Gemini API Key)

https://codelabs.developers.google.com/adkcourse/instructions

## 1. Clone the Repository
```bash
git clone https://github.com/cuppibla/adk_tutorial.git
cd adk_tutorial
```

## 2. Create Gemini API Key 
- https://aistudio.google.com/app/api-keys
- copy and keep it handy.

## 3. Configure Environment
```bash
cloudshell edit .env
```

```text
GOOGLE_GENAI_USE_VERTEXAI=FALSE
GOOGLE_API_KEY=AIza...
```

> **Note:** The free Gemini API key may occasionally return **429 (quota exceeded)** or **404 (model unavailable)** depending on account quota or model availability. If this happens, either use a Gemini API key with available quota or use the Vertex AI version of the codelab.

## 4. Start ADK
```bash
adk web
```

## 5. Change the port to 8000

## Agent Selection and Prompts
1. <strong>a_single_agent</strong>
   Plan a trip from Sunnyvale to San Francisco this weekend, I love food and art.
2. <strong>b2_parallel_agent</strong>
   Plan my trip to San Francisco, I want to find some good concert, restaurant and museum.
3. <strong>b1_sequential_agent</strong>
   Find a good sushi near Stanford and tell me how to get there.
4. <strong>b3_loop_agent</strong>
   Plan a trip from Sunnyvale to San Francisco today.
5. <strong>c_custom_agent</strong>
   Plan a trip from Sunnyvale to San Francisco this weekend, I love food and art. Make sure within budget of 100 dollars.
6. <strong>d_routing_agent</strong>
   Plan a trip from Sunnyvale to San Francisco this weekend, I love concert, restaurant and museum.
7. <strong>e_agent_as_tool</strong>
   Plan a trip from Sunnyvale to San Francisco this weekend, I love concert, restaurant and museum.

## Session 6
Follow Step 8 of the codelab.

## Session 7 (MCP)
If you have issues with the toolbox, follow the workaround below. 

### Toolbox Workaround
```bash
cd ~/adk_tutorial/mcp_tool_box

rm -f toolbox

export VERSION=0.16.0
export OS=linux/amd64

curl -L -o toolbox https://storage.googleapis.com/genai-toolbox/v$VERSION/$OS/toolbox

chmod +x toolbox
```

### Terminal 1
```bash
cd ~/adk_tutorial/mcp_tool_box
./toolbox --tools-file "trip_tools.yaml" --port 7001
```

### Terminal 2
```bash
cd ~/adk_tutorial
set -a
source .env
set +a
source .adk_env/bin/activate
cd g_agents_mcp
python -u main.py
```
Sometimes, killing the terminal and restarting the server works too!

### MCP Prompts
- What are the top-rated things to do in Tokyo?
- Show me the museums in Rome.
- What can I do in New York for under 25 dollars?

