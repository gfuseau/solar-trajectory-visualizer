# Solar Trajectory Visualizer

## Overview

The **Solar Trajectory Visualizer** is a standalone, single-file HTML application designed to simulate the path of the Sun across the "Sky Dome" for any location on Earth.

Built with vanilla JavaScript and the HTML5 Canvas API, this tool visualizes complex celestial mechanics in an intuitive, hemispherical view where the observer is at the center, looking up at the Zenith.

## Features

### 1. Interactive Sky Dome

* **Perspective:** Top-down view of the celestial hemisphere.

* **Center:** The Zenith (90° altitude, directly overhead).

* **Outer Ring:** The Horizon (0° altitude).

* **Solar Path:**
  * Day Path (Blue): The trajectory of the sun while it is above the horizon.

  * Night Path (Dark Blue): The trajectory continues below the horizon to visualize the complete 24-hour cycle.

* Compass: Clear cardinal markers (N, S, E, W) to help orient the observer.

### 2. User Controls

* Quick City Selector: Instantly jump to interesting locations like Buenos Aires, Stockholm, Quito, or Antarctica to see extreme solar behaviors.

* Latitude Slider: Adjust from -90° (South Pole) to 90° (North Pole).

* Date Slider: Cycle through the 365 days of the year to observe seasonal shifts (Solstices and Equinoxes).

* Time Slider: Move the sun through the day to see Sunrise, Solar Noon, and Sunset.

### 3. Real-Time Telemetry

The application calculates and displays:

* Altitude: The angle of the sun above the horizon.

* Azimuth: The compass direction of the sun (Degrees from North).

* Declination: The celestial latitude of the sun relative to the celestial equator.

* Day Length: The duration of sunlight for the selected date and latitude.

## Mathematical Model

The application uses **Spherical Trigonometry** to convert the Sun's Equatorial coordinates into the observer's Horizontal coordinates.

### 1. Solar Declination ($\delta$)

This approximates the tilt of the Earth relative to the Sun for a specific day ($d$):


$$\delta \approx 23.45^\circ \cdot \sin\left(\frac{360}{365} \cdot (d - 81)\right)$$

### 2. Hour Angle ($H$)

Converts the local solar time ($t$) into degrees from solar noon:


$$H = 15^\circ \cdot (t - 12)$$

### 3. Solar Altitude ($a$)

Calculated using the observer's Latitude ($\phi$), Declination ($\delta$), and Hour Angle ($H$):


$$\sin(a) = \sin(\phi)\sin(\delta) + \cos(\phi)\cos(\delta)\cos(H)$$

### 4. Solar Azimuth ($A$)

Determines the compass direction. The formula calculates the angle from the South/North pole, which is then corrected to standard compass bearings (0° = North, 90° = East):


$$\cos(A) = \frac{\sin(\delta) - \sin(a)\sin(\phi)}{\cos(a)\cos(\phi)}$$

## Code Structure

The project follows a modular architecture within a single file to ensure maintainability and readability (DRY principles):

1. **Configuration:** Centralized constant object (`THEME`) for colors and visual settings.

2. **SolarMath Module:** Pure functions that handle all physics and trigonometry calculations.

3. **Graphics Module:** specialized functions for Canvas rendering (`drawGrid`, `drawPath`, `drawSun`), separating the *how* it looks from the *math* of where it is.

4. **UI/DOM Module:** Handles event listeners, DOM updates, and specific "insight" logic (e.g., explaining why the sun sets South-West in Buenos Aires during February).

## Usage

Simply open `solar_trajectory.html` in any modern web browser. No installation or external servers are required.
