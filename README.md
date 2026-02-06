# PrepWise - Smart Meal Planner

A beautiful meal planning app powered by Claude AI that helps you plan weekly meals, generate grocery lists, and reduce food waste.

## Features

- 🍽️ Personalized meal plans based on dietary preferences
- 💰 Budget-conscious grocery planning
- 🛒 Interactive grocery list with cost breakdown
- 💡 Meal prep tips and storage advice
- ✅ Checkable grocery items
- 📱 Mobile-responsive design

## Tech Stack

- **Frontend**: Pure HTML/CSS/JavaScript
- **Backend**: Netlify Serverless Functions
- **AI**: Claude API (Sonnet 4)
- **Deployment**: Netlify

## Local Development

### Prerequisites

- Node.js (v14 or higher)
- An Anthropic API key ([get one here](https://console.anthropic.com/))

### Setup

1. **Clone or download this repository**

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Create a `.env` file** (copy from `.env.example`)
   ```bash
   cp .env.example .env
   ```

4. **Add your Anthropic API key to `.env`**
   ```
   ANTHROPIC_API_KEY=sk-ant-xxxxx
   ```

5. **Start the development server**
   ```bash
   npm run dev
   ```

6. **Open your browser** to `http://localhost:8888`

## Deploy to Netlify

### Option 1: Deploy via Netlify UI (Recommended)

1. **Push your code to GitHub** (create a new repository)

2. **Go to [Netlify](https://app.netlify.com/)** and sign in

3. **Click "Add new site" → "Import an existing project"**

4. **Connect to your GitHub repository**

5. **Configure build settings** (Netlify will auto-detect from `netlify.toml`)
   - Build command: (leave empty)
   - Publish directory: `.`
   - Functions directory: `netlify/functions`

6. **Add environment variable**
   - Go to Site settings → Environment variables
   - Add `ANTHROPIC_API_KEY` with your API key value

7. **Deploy!** Netlify will build and deploy your site

### Option 2: Deploy via Netlify CLI

1. **Install Netlify CLI globally**
   ```bash
   npm install -g netlify-cli
   ```

2. **Login to Netlify**
   ```bash
   netlify login
   ```

3. **Initialize your site**
   ```bash
   netlify init
   ```

4. **Set your environment variable**
   ```bash
   netlify env:set ANTHROPIC_API_KEY "your-api-key-here"
   ```

5. **Deploy**
   ```bash
   netlify deploy --prod
   ```

## Environment Variables

Set the following environment variable in Netlify:

- `ANTHROPIC_API_KEY` - Your Anthropic API key from https://console.anthropic.com/

⚠️ **Important**: Never commit your `.env` file or expose your API key in client-side code.

## Project Structure

```
prepwise-netlify/
├── index.html                          # Main HTML file
├── netlify.toml                        # Netlify configuration
├── package.json                        # Node dependencies
├── .env.example                        # Environment variables template
├── .gitignore                          # Git ignore rules
├── netlify/
│   └── functions/
│       └── generate-meal-plan.js       # Serverless function for Claude API
└── README.md                           # This file
```

## How It Works

1. User fills out preferences (dietary restrictions, budget, household size, food dislikes)
2. Frontend sends a request to the Netlify serverless function
3. Serverless function securely calls Claude API with the user's prompt
4. Claude generates a structured meal plan with grocery list and tips
5. Frontend displays the results in an interactive UI

## Customization

### Modify Dietary Options

Edit the `DIETARY_OPTIONS` array in `index.html`:

```javascript
const DIETARY_OPTIONS = [
  { id: "none", label: "No Restrictions", icon: "🍽️" },
  // Add your own options here
];
```

### Adjust Budget Range

Modify the budget slider in `index.html`:

```html
<input type="range" min="30" max="300" step="5" value="100" id="budgetSlider">
```

### Change AI Model

Edit the serverless function in `netlify/functions/generate-meal-plan.js`:

```javascript
model: 'claude-sonnet-4-20250514',  // Change to another Claude model
```

## API Costs

This app uses the Claude API. Check [Anthropic's pricing](https://www.anthropic.com/pricing) for current rates. Typical meal plan generation uses ~1,000-2,000 tokens.

## Troubleshooting

**Issue**: "Server configuration error" when generating meal plans
- **Solution**: Make sure `ANTHROPIC_API_KEY` is set in Netlify environment variables

**Issue**: CORS errors in browser console
- **Solution**: The serverless function includes CORS headers; make sure you're accessing via the Netlify domain

**Issue**: Function timeout
- **Solution**: Claude API calls should complete in <10 seconds. Check your API key and network connection

## License

MIT License - feel free to use this for personal or commercial projects!

## Credits

Built with ❤️ using Claude AI
