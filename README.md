AI agent that joins a meeting and participates like a human. Useful for product demos, sales meetings, weekly meetings, etc.

Inspired by: https://github.com/recallai/voice-agent-demo

Here are the instructions on how to run the agent.

1. Activate the virtual environment and download the required libraries:

source .venv/bin/activate
pip install -r requirements.txt

2. Run the server (terminal 1):

cd python-server
python server.py

3. Run ngrok in a different terminal (terminal 2):

ngrok http 3000

4. Create a bot by sending a curl request. Ensure to:
      - replace YOUR_RECALL_TOKEN (and server url)
      - replace YOUR_NGROK_URL (do not include https://)
      - replace YOUR_BOT_NAME
      - replace meeting_url with your meeting url

CURL request template:

curl --request POST \
  --url https://us-east-1.recall.ai/api/v1/bot/ \
  --header 'Authorization: YOUR_RECALL_TOKEN' \
  --header 'accept: application/json' \
  --header 'content-type: application/json' \
  --data '{
    "meeting_url": "YOUR_MEETING_URL",
    "bot_name": "Recall.ai Notetaker",
    "output_media": {
      "camera": {
        "kind": "webpage",
        "config": {
          "url": "https://recallai-demo.netlify.app?wss=wss://YOUR_NGROK_URL"
        }
      }
    },
    "variant": {
      "zoom": "web_4_core",
      "google_meet": "web_4_core",
      "microsoft_teams": "web_4_core"
    }
  }'

CURL request with a video:

curl --request POST \
  --url https://us-west-2.recall.ai/api/v1/bot/ \
  --header 'Authorization: Recall API KEY' \
  --header 'accept: application/json' \
  --header 'content-type: application/json' \
  --data '{
    "meeting_url": "https://meet.google.com/nep-gmxq-tav",
    "bot_name": "v1",
    "output_media": {
      "camera": {
        "kind": "webpage",
        "config": {
          "url": "https://ai-orb-video.vercel.app?wss=wss://NGROK_URL"
        }
      },
      "microphone": {
        "kind": "audio"
      }
    },
    "variant": {
      "zoom": "web_4_core",
      "google_meet": "web_4_core",
      "microsoft_teams": "web_4_core"
    }
  }'
