# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a SINTEF weather display application for Trondheim, Norway. It's designed to be displayed on a large screen (storskjerm) and shows real-time weather information with animated visual effects. The application fetches data from MET.no's LocationForecast API and displays it in Norwegian with SINTEF branding.

## Architecture

### Core Files

- **trondheim-weather.html**: Main application file containing HTML structure, weather API integration logic, and animation rendering
- **weather-app.css**: Custom styles including Utopia fluid responsive design system, weather animations, and component styling
- **sintef-clean.css**: Minimal SINTEF design system (cleaned version containing only normalize, typography, brand colors, and buttons)
- **SINTEF_Logo_Sentrert_RGB.jpg**: SINTEF logo displayed at top of screen
- **wind-loop.mp4**: Video file (not currently used, kept for reference)

### Application Flow

1. **Data Fetching** (`fetchWeather()`): Fetches weather data from MET.no API for Trondheim coordinates (LAT: 63.4305, LON: 10.3951)
2. **Data Processing**: Aggregates today's weather data (temperatures, wind speeds, precipitation, cloud coverage)
3. **Text Generation**: Formats Norwegian text: "Laveste meldte i dag er X grader og høyeste meldte er X grader" with wind and precipitation details
4. **Animation Selection** (`showWeatherAnimation()`): Determines which weather animation to display based on conditions:
   - **Snow** (❄️): precipitation > 1mm AND temp < 2°C
   - **Rain** (🌧️): precipitation > 0.5mm
   - **Wind** (💨): wind speed > 5 m/s (shows NorthWind info)
   - **Cloudy** (☁️): cloud coverage > 70%
   - **Sun** (☀️): default condition
5. **Animation Rendering**: Creates DOM elements for weather effects using CSS keyframe animations
6. **Content Animation**: Weather headline and info box fade in with slide-up effect (0.3s delay between them)

### Design System

The app uses **Utopia Fluid Responsive Design** for typography and spacing:
- Typography scale: `--step--2` through `--step-5` using CSS `clamp()`
- Spacing scale: `--space-3xs` through `--space-3xl` using CSS `clamp()`
- SINTEF brand colors defined as CSS custom properties in both stylesheets
- Google Fonts: Lato (weights 300, 400, 700) - currently using 400 throughout

### Animation Techniques

All weather animations use CSS keyframes with negative animation delays to make elements appear already in motion (avoids "waiting" or "clumping" at start):

- **Rain/Snow**: 50-100 elements with negative delays (`animationDelay: -(Math.random() * 2)`)
- **Wind**: Leaf emojis (🍂🍃🍁) blown horizontally with rotation
- **Clouds**: Drift from left (-100px) to right with negative delays for smooth appearance
- **Sun**: Rotating sun with drifting clouds

Text animations use `fadeSlideUp` keyframe (opacity + translateY) with `.animate-in` class trigger.

### Layout Structure

Uses **flexbox** for document flow (no absolute positioning except for animation layers):
- Body: flexbox column with gap spacing
- Logo at top (flex-shrink: 0)
- Weather headline (flex-shrink: 0)
- Weather container (flex: 1) with info box at bottom-left
- Animation layer: fixed fullscreen (z-index: 1)
- Info box: relative (z-index: 10)

### Development Tools

**Hamburger Menu** (top-right corner):
- Hidden by default (`opacity: 0`)
- Reveals on hover with test controls for simulating different weather conditions
- Test buttons trigger `testWeather(type)` function with predefined conditions
- Hover-based menu using `.menu-wrapper:hover` CSS selector

## SINTEF Branding Guidelines

- **Primary color**: SINTEF Blue (`#003c65`)
- **Text on dark backgrounds**: Light green (`#cdfae1`)
- **Info box background**: SINTEF Beige (`#EBEBE6`)
- **Font**: Lato 400 weight throughout (no bold variations currently used)
- **No decorative elements**: Emojis were removed from data display for cleaner look
- **Logo**: Always display SINTEF_Logo_Sentrert_RGB.jpg at top

### Info Box Content by Weather Type

Each weather condition shows relevant SINTEF research information:
- **Sun**: Solar energy and solar cell efficiency research
- **Cloudy**: Weather forecasting and climate modeling technology
- **Rain**: Water management and stormwater handling for flood protection
- **Snow**: Climate change research and adaptation
- **Wind**: NorthWind research center for offshore wind power

## Common Patterns

### Triggering Animations

When updating content that needs animation:
```javascript
const element = document.getElementById('element-id');
element.classList.remove('animate-in');
void element.offsetWidth; // Force reflow
element.classList.add('animate-in');
```

### Temperature Rounding

Always use `Math.round()` for temperature values (no decimals).

### Cache Busting

The weather-app.css link includes version parameter (`?v=8`) to bypass browser caching during development.

### Dark Background Toggle

Body class `.dark-bg` is toggled for weather types with dark backgrounds (rain, wind, cloudy) to change headline text color to light green.

## Testing

Use the hover menu (top-right corner) to test different weather scenarios without waiting for API data. Each test button simulates realistic conditions for that weather type.

## API Integration

- **Endpoint**: `https://api.met.no/weatherapi/locationforecast/2.0/compact`
- **Location**: Trondheim city center (63.4305, 10.3951)
- **Data Points**: Extracts today's hourly data for temperature, wind speed, precipitation amount, and cloud area fraction
- **Aggregation**: Calculates min/max/average values across today's forecast
