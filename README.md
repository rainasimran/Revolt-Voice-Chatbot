Revolt Motors Voice Chat Clone  

A complete implementation of a **real-time voice assistant for Revolt Motors**, built using **Google's Gemini Live API**, replicating the functionality of their production chatbot with a modern, responsive UI.  

---

## 🌟 Features  
- 🎙️ Real-time voice conversations with AI assistant  
- ✋ User interruption support (barge-in functionality)  
- ⚡ Low latency responses (1–2 seconds target)  
- 🖥️ Clean, responsive, and updated user interface  
- 🔒 Server-to-server architecture for secure communication  
- 🌐 Domain-specific chatbot focused exclusively on **Revolt Motors topics**  

---

## 🛠️ Prerequisites  
Before you begin, ensure you have installed:  
- Node.js **v18 or higher**  
- npm **v9 or higher**  
- Google Cloud account with **Gemini API enabled**  
- Microphone-enabled device  
- Modern browser (**Chrome recommended**)  

---

## 🚀 Quick Start  

### 1. Clone the repository  
```bash
git clone https://github.com/rainasimran/Revolt-Voice-Chatbot.git
cd Revolt-Voice-Chatbot
```
2. Install dependencies
npm install

3. Set up environment variables

Create a .env file:

cp .env.example .env


Edit .env with your credentials:

GEMINI_API_KEY=your_actual_api_key_here
PORT=3000
NODE_ENV=development

4. Run the application
npm start

5. Access the app

Open 👉 http://localhost:5173 in your browser.

🏗️ Project Structure

Revolt-Voice-Chatbot/
├── public/              # Client-facing assets
│   ├── css/             # Stylesheets
│   ├── js/              # Client-side JavaScript
│   ├── audio/           # Temporary audio storage
│   └── index.html       # Main interface (updated UI)
├── routes/              # API endpoints
│   └── api.js           # Voice chat API routes
├── services/            # Core services
│   ├── gemini.js        # Gemini API wrapper
│   └── audio.js         # Audio processing
├── app.js               # Express application
├── package.json         # Dependencies
└── README.md            # Project documentation

🔧 Configuration
Gemini Models

Edit services/gemini.js to switch models:

// For production
const model = 'gemini-2.5-flash-preview-native-audio-dialog';

// For development (higher rate limits)
// const model = 'gemini-2.0-flash-live-001';

System Instructions

The AI behavior is controlled by this prompt in services/gemini.js:

const systemInstructions = `
You are "Rev", the official AI assistant for Revolt Motors.
Your knowledge is strictly limited to:

- Revolt Motors electric vehicles (RV300, RV400, etc.)
- Charging infrastructure and battery technology
- Company history and leadership
- Dealer network and test drives
- Pricing and financing options

For any off-topic questions, respond with:
"I'm specialized in Revolt Motors products. How can I help you with our electric vehicles?"
`;

🎯 Key Implementation Details
Voice Processing Flow

Browser captures microphone input via Web Audio API

Audio stream sent to backend in chunks

Server processes via Gemini Live API

Text response converted to speech via Web Speech API

Audio streamed back to client in real-time

Interruption Handling
// In services/gemini.js
const handleInterruption = () => {
  audioProcessor.stopCurrentPlayback();
  startNewSession(); // Gemini API handles interruption
};

🧪 Testing

Manual Tests:

Ask about Revolt Motors products → verify AI response

Speak during AI reply → check interruption handling

Measure latency (~1–2s)

Ask off-topic questions → verify redirection

Automated Tests:

npm test

🚨 Troubleshooting
Issue	Solution
API quota exceeded	Use development model or request quota increase
Microphone access blocked	Check browser permissions + HTTPS
High latency	Reduce audio chunk size / check network
Audio distortion	Adjust sample rate in services/audio.js

🌍 Deployment
Heroku Example
heroku create revolt-voice-chatbot
heroku config:set GEMINI_API_KEY=your_key
heroku config:set NODE_ENV=production
git push heroku main


Production Notes:

HTTPS required for microphone

Env variables set properly

PM2 or similar process manager recommended

📚 Resources

Demo Video --> https://drive.google.com/file/d/1b44pEYLuEP_vI1-Fz883Q7aeYL9YLQCX/view?usp=drive_link

📄 License

MIT License - See LICENSE file for details

📧 Contact

For support, contact: simranraina30@gmail.com

