# Career Conversation Agent

A chatbot that answers questions about my career, as if you were talking to me. It reads my resume and a short summary, answers in my voice, and uses tool calling to record follow-ups.

**Live demo:** [huggingface.co/spaces/dollyjain/career_conversation](https://huggingface.co/spaces/dollyjain/career_conversation)

## What it does

- Answers questions about my background, skills, experience and certifications
- Stays in character and keeps answers grounded in the resume and summary it is given
- Uses two tools the model can call:
  - `record_user_details` records a visitor's email when they want to get in touch
  - `record_unknown_question` records any question it couldn't answer, so the gaps can be filled
- Sends those records as push notifications through Pushover

## How it works

1. On start-up, the app reads `me/linkedin.pdf` (resume text, via pypdf) and `me/summary.txt`.
2. Both go into a system prompt that tells the model who it is representing and how to behave.
3. Each message is sent to the model with the conversation history and the tool definitions.
4. If the model asks to call a tool, the app runs it, adds the result to the conversation and calls the model again, looping until it returns a normal answer.
5. Gradio's `ChatInterface` provides the chat UI, and the app is hosted as a Hugging Face Space.

## Tech stack

Python · OpenAI API (gpt-4o-mini) · tool calling · Gradio · pypdf · Hugging Face Spaces

## Run it locally

```bash
pip install -r requirements.txt
cp .env.example .env      # add your OpenAI and Pushover keys
# add me/linkedin.pdf and me/summary.txt (see me/README.md)
python app.py
```

## Credit

Built from the career conversation lab in Ed Donner's *Complete Agentic AI Engineering Course* (Udemy), adapted with my own profile and deployed to Hugging Face Spaces.
