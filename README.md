# NarrativeForge

AI-powered narrative and media generation platform with a stunning Tron/Minority Report-inspired UI.

## Features

- **Text Generation**: Create stories, screenplays, poems, songs, rap lyrics, and speeches
- **Image Generation**: Generate stunning images from text prompts using Replicate's FLUX model
- **Image-to-Video**: Convert images to videos with AI-powered motion
- **PWA Support**: Install as a Progressive Web App on desktop and mobile
- **Dark/Light Theme**: Toggle between dark and light modes
- **Save & Organize**: Save your creations and access them later
- **Dashboard**: Track your generation statistics

## Tech Stack

### Frontend
- **React 19** + **Vite** - Modern, fast development
- **Tailwind CSS** - Utility-first styling
- **shadcn/ui** - Beautiful, accessible components
- **Framer Motion** - Smooth animations
- **Lucide Icons** - Crisp, modern icons
- **React Router** - Client-side routing

### Backend
- **Node.js** + **Express** - Fast, lightweight server
- **OpenAI API** - Text generation (GPT-4o-mini)
- **Replicate API** - Image and video generation (FLUX, Stable Video Diffusion)

## Quick Start

### Prerequisites

- Node.js 18+ and npm/pnpm
- OpenAI API key ([Get one here](https://platform.openai.com/api-keys))
- Replicate API token ([Get one here](https://replicate.com/account/api-tokens))

### Installation

1. **Clone or extract the repository**

```bash
cd narrativeforge
```

2. **Install dependencies**

```bash
npm install
```

This will install dependencies for both the root, client, and server.

3. **Set up environment variables**

Create a `.env` file in the `server` directory:

```bash
cd server
cp .env.example .env
```

Edit `server/.env` and add your API keys:

```env
OPENAI_API_KEY=sk-your-openai-key-here
REPLICATE_API_TOKEN=r8_your-replicate-token-here
PORT=8080
CLIENT_URL=http://localhost:5173
```

### Running the Application

**Option 1: Run both client and server together (recommended)**

```bash
npm run dev
```

This will start:
- Client on `http://localhost:5173`
- Server on `http://localhost:8080`

**Option 2: Run client and server separately**

Terminal 1 (Client):
```bash
npm run dev:client
```

Terminal 2 (Server):
```bash
npm run dev:server
```

### Building for Production

```bash
cd client
pnpm build
```

The production build will be in `client/dist`.

## API Endpoints

### POST /api/gen/text
Generate text content (stories, poems, etc.)

**Request:**
```json
{
  "mode": "story",
  "prompt": "A tale of a forgotten city",
  "length": "medium",
  "tone": "dramatic",
  "style": "modern"
}
```

**Response:**
```json
{
  "id": "1234567890",
  "status": "completed",
  "text": "Generated text content...",
  "meta": { "mode": "story", "length": "medium", "tone": "dramatic", "style": "modern" }
}
```

### POST /api/gen/image
Generate images from text prompts

**Request:**
```json
{
  "prompt": "A futuristic cityscape at sunset",
  "aspect": "16:9",
  "steps": 30,
  "guidance": 7.5
}
```

**Response:**
```json
{
  "id": "1234567890",
  "status": "completed",
  "url": "https://replicate.delivery/...",
  "meta": { "prompt": "...", "aspect": "16:9" }
}
```

### POST /api/gen/image-to-video
Convert images to videos

**Request:**
```json
{
  "prompt": "Add gentle camera movement",
  "imageUrl": "https://example.com/image.png",
  "motionStyle": "default"
}
```

**Response:**
```json
{
  "id": "1234567890",
  "status": "completed",
  "url": "https://replicate.delivery/...",
  "meta": { "prompt": "...", "imageUrl": "..." }
}
```

## Project Structure

```
narrativeforge/
├── client/                 # React frontend
│   ├── public/
│   │   ├── manifest.webmanifest
│   │   ├── sw.js          # Service worker for PWA
│   │   └── icons/
│   ├── src/
│   │   ├── components/
│   │   │   ├── IntroScreen.jsx
│   │   │   ├── TextMediaGenerator.jsx
│   │   │   └── ui/        # shadcn/ui components
│   │   ├── routes/
│   │   │   ├── Home.jsx
│   │   │   ├── Images.jsx
│   │   │   ├── Videos.jsx
│   │   │   ├── Clips.jsx
│   │   │   ├── Characters.jsx
│   │   │   ├── Plots.jsx
│   │   │   ├── Saved.jsx
│   │   │   ├── Dashboard.jsx
│   │   │   └── Download.jsx
│   │   ├── App.jsx
│   │   ├── App.css
│   │   └── main.jsx
│   ├── package.json
│   └── vite.config.js
├── server/                # Node.js/Express backend
│   ├── index.js          # Main server file
│   ├── package.json
│   └── .env.example
├── package.json          # Root package.json
└── README.md
```

## Features in Detail

### Text Generation Modes
- **Story**: Creative narratives
- **Screenplay**: Movie/TV scripts
- **Poem**: Poetic compositions
- **Song**: Song lyrics
- **Rap**: Rap verses
- **Speech**: Formal speeches

### Image Generation
- Aspect ratios: 1:1 (Square), 16:9 (Landscape), 9:16 (Portrait)
- Powered by Replicate's FLUX Schnell model
- High-quality PNG output

### Image-to-Video
- Convert static images to animated videos
- Powered by Stable Video Diffusion
- Customizable motion styles

### PWA Features
- Install on desktop and mobile
- Offline support with service worker
- Native-like experience

## API Keys & Free Tiers

### OpenAI
- Free tier: $5 credit for new accounts
- Model used: `gpt-4o-mini` (very affordable)
- [Pricing](https://openai.com/pricing)

### Replicate
- Pay-as-you-go pricing
- FLUX Schnell: ~$0.003 per image
- Stable Video Diffusion: ~$0.05 per video
- [Pricing](https://replicate.com/pricing)

## Switching Providers/Models

### To use a different OpenAI model:
Edit `server/index.js`, line ~45:
```javascript
model: 'gpt-4o',  // or 'gpt-4', 'gpt-3.5-turbo', etc.
```

### To use a different image model:
Edit `server/index.js`, line ~87:
```javascript
const output = await replicate.run(
  "stability-ai/sdxl",  // or another model
  { /* ... */ }
);
```

## File Storage

Generated files are served directly from Replicate's CDN. No local storage is required for images/videos.

Text content can be saved to local storage (browser) or extended to use a database.

## Troubleshooting

### Server won't start
- Check that port 8080 is not in use
- Verify your `.env` file has valid API keys

### Client won't connect to server
- Ensure server is running on port 8080
- Check CORS settings in `server/index.js`

### API errors
- Verify your API keys are correct and active
- Check your Replicate/OpenAI account balance
- Review server logs for detailed error messages

## Contributing

Feel free to submit issues and pull requests!

## License

ISC

---

**Built with ❤️ using AI-powered tools**

