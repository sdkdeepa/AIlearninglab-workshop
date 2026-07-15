# ADK Codelab (Vertex AI + Google Cloud)

## Pre Setup 
Follow the slides for steps: [Slides](https://docs.google.com/presentation/d/19GNvPupJEnrbXKrsydzpp5Jhqb3e3ZfjXd6zg8_M2KU/edit?usp=sharing)

1. Create a brand new Gmail account ad activate free cloud trial (worth $300)
2. go to https://console.cloud.google.com/
3. Click create "Create a project"
4. Enter project name
5. Select "No Orginization" under Parent resource
6. Click "Activate Cloud Shell" on the top right 
7. Make sure you the terminal shows the project id correctly
8. You may be asked to 
8. Click "Open editor" 

# Workshop 
## 1. Clone the Repository
```bash
git clone https://github.com/cuppibla/adk_tutorial.git
cd adk_tutorial
```

## 2. Google Cloud Setup
- Create a Google Cloud Project (Free Trial with $300 credits)
- Authenticate:
```bash
gcloud auth login
gcloud auth application-default login
```
- Enable APIs:
```bash
gcloud services enable aiplatform.googleapis.com
```
<em><strong>Optional services </em></strong>(For Deployment only - won't be covered during the workshop)

```bash
gcloud services enable \
  run.googleapis.com \
  cloudbuild.googleapis.com

```

## 3. Configure Environment
```bash
cloudshell edit .env
```

```text
GOOGLE_GENAI_USE_VERTEXAI=TRUE
GOOGLE_CLOUD_PROJECT=<PROJECT_ID>
GOOGLE_CLOUD_LOCATION=global
```
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
```bash
What are the top-rated things to do in Tokyo?
Show me the museums in Rome.
What can I do in New York for under 25 dollars?
```
------
# Restarting the Vertex AI Environment

If you close Cloud Shell or return later, follow these steps.

## 1. Open Google Cloud Console
- https://console.cloud.google.com
- Launch **Cloud Shell**.

## 2. Go to the project and activate the virtual environment

```bash
cd ~/adk_tutorial
source .adk_env/bin/activate
```

## 3. Verify authentication and project

```bash
gcloud auth list
```

If required:

```bash
gcloud auth login
```

Verify the project:

```bash
gcloud config get-value project
```

<strong> If needed:</strong>

```bash
gcloud config set project YOUR_PROJECT_ID
```

## 4. Authenticate Application Default Credentials (ADC)

```bash
gcloud auth application-default login
```

(Optional)

```bash
gcloud auth application-default print-access-token
```

## 5. Verify Vertex AI API is Enabled 
```bash
gcloud services list --enabled | grep aiplatform
```

## 6. Verify the environment and start ADK

```bash
cloudshell edit .env
```

```text
GOOGLE_GENAI_USE_VERTEXAI=TRUE
GOOGLE_CLOUD_PROJECT=YOUR_PROJECT_ID
GOOGLE_CLOUD_LOCATION=global
```
Make sure to set it to global location.

### Start ADK:

```bash
adk web
```

Open the forwarded URL on port **8000**.

### Troubleshooting

If you receive **403 PERMISSION_DENIED** or **Application Default Credentials not found**, run:

```bash
gcloud auth application-default login
```

`gcloud auth application-default login` is different from `gcloud auth login`. Both may be required when using Vertex AI.