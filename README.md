# SINTEF Weather Widget

A real-time weather display application for Trondheim, Norway, featuring animated weather effects and SINTEF research information.

## 🌦️ Live Demo

**View the live application:** [www.dovenpels.no/sintef-weather-widget/trondheim-weather.html](http://www.dovenpels.no/sintef-weather-widget/trondheim-weather.html)

## Features

- **Real-time Weather Data** - Fetches current weather from MET.no API for Trondheim
- **4-Line Weather Display:**
  - Today's min/max temperature
  - Current conditions with "feels like" temperature (wind chill calculation)
  - Precipitation forecast for next hour
  - Cloud coverage forecast for rest of day
- **Animated Weather States** - Five distinct weather animations:
  - ☀️ Sunny - Rotating sun with drifting clouds
  - ☁️ Cloudy - Slow-moving clouds across the sky
  - 🌧️ Rain - Falling raindrops
  - ❄️ Snow - Falling snowflakes
  - 💨 Wind - Blowing leaves
- **Wind Chill Calculation** - Calculates "feels like" temperature using Canadian wind chill formula
- **SINTEF Educational Content** - "Visste du at..." info box with relevant SINTEF research
- **Responsive Design** - Utopia fluid responsive design system with optimal reading width
- **SINTEF Branding** - Official SINTEF colors and styling

## Technology

- Pure HTML, CSS, and JavaScript (no frameworks)
- MET.no LocationForecast API
- CSS Grid and Flexbox layout
- CSS Keyframe animations
- Utopia fluid responsive typography and spacing
- Google Fonts (Lato)

## Development

To test the application locally, simply open `trondheim-weather.html` in a web browser.

### Test Mode

Hover over the top-right corner to reveal a hamburger menu with test controls for simulating different weather conditions.

## Files

- `trondheim-weather.html` - Main application file
- `weather-app.css` - Custom styles and animations
- `sintef-clean.css` - SINTEF base design system
- `SINTEF_Logo_Sentrert_RGB.jpg` - SINTEF logo
- `CLAUDE.md` - Documentation for Claude Code

## Credits

Built with [Claude Code](https://claude.com/claude-code)

Weather data provided by [MET Norway](https://api.met.no/)

## License

© SINTEF
