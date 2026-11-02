# 🎓 AI Learning Buddy

A small Streamlit app that turns any topic into a beginner-friendly explanation, a real-life example, or a practice quiz, powered by Google's Gemini API.

## Why

Learning a new topic usually means jumping between several places: one for a simple explanation, another for real-world examples, and another for practice questions. AI Learning Buddy puts all of these in one place. You type a topic and pick what you need.

## Features

Enter a topic and choose an activity:

| Activity | What you get |
|---|---|
| **Explain Concept** | A simple explanation aimed at beginners |
| **Real-Life Example** | One easy-to-relate example of the topic |
| **Generate Quiz** | 5 multiple-choice questions with answers |
| **Ask Anything** | Your text sent to Gemini as-is, for free-form questions |

If the topic box is empty, the app shows a warning instead of calling the API.

## Tech stack

- **Python** + **[Streamlit](https://streamlit.io/)** for the web UI
- **Google Gemini API** (`gemini-2.5-flash`) via the `google-generativeai` SDK
- **Streamlit secrets** for API key handling (the key is never hard-coded)

## Getting started

### Prerequisites

- Python 3.9+
- A Gemini API key. Get one free from [Google AI Studio](https://aistudio.google.com/app/apikey).

### 1. Clone the repo

```bash
git clone https://github.com/ShaistaSultana1011/ai-learning-buddy.git
cd ai-learning-buddy
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Add your API key

Create a file at `.streamlit/secrets.toml` in the project folder:

```toml
GEMINI_API_KEY = "your-api-key-here"
```

> ⚠️ Don't commit this file. Add `.streamlit/secrets.toml` to your `.gitignore`.

### 4. Run the app

```bash
streamlit run ai_learning_buddy.py
```

Open the URL Streamlit prints (usually http://localhost:8501), enter a topic, choose an activity, and click **Generate**.

### Deploying on Streamlit Community Cloud

1. Push the repo to GitHub and create a new app on [share.streamlit.io](https://share.streamlit.io/) pointing at `ai_learning_buddy.py`.
2. In the app's **Settings → Secrets**, paste:
   ```toml
   GEMINI_API_KEY = "your-api-key-here"
   ```

The repo also includes a `.devcontainer` config, so it can be opened directly in GitHub Codespaces. You'll still need to add the secrets file there.

## How it works

1. The app configures Gemini with the key from `st.secrets["GEMINI_API_KEY"]`.
2. Based on the selected activity, it builds a targeted prompt (for example, *"Explain {topic} in simple language for a beginner."*).
3. The prompt goes to `gemini-2.5-flash`, and the response is rendered on the page.

## Lessons learned

- **Prompt design matters.** Short, specific instructions ("for a beginner", "5 MCQs with answers") give far more consistent output than vague prompts.
- **The model is the easy part.** Wiring up an LLM API takes only a few lines. Most of the value comes from how the product frames the request.
- **Keep secrets out of code.** Streamlit secrets keep the API key out of the source and out of GitHub.
- **Streamlit is great for prototyping.** It gives you a usable UI without writing any HTML, CSS, or JavaScript.

## Roadmap

- [ ] Interactive quiz mode with scoring
- [ ] Save session / chat history
- [ ] Difficulty levels (beginner / intermediate / advanced)
- [ ] Migrate to Google's newer [`google-genai`](https://pypi.org/project/google-genai/) SDK (`google-generativeai` is being phased out)
- [ ] Add a `.gitignore` for `.streamlit/secrets.toml`
