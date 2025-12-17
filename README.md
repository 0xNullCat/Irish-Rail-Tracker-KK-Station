# 🚂 Irish Rail Train Tracker Tools

Real-time train tracking for Kilkenny Station using the Irish Rail API.

## 📋 Overview

Two Python scripts for tracking trains at Kilkenny Station:

1. **Kilkenny Station Arrivals** - View all trains arriving at Kilkenny
2. **Partner Train Tracker** - Track a specific train with personalized pickup timing

## 🚀 Quick Start

### Prerequisites

- Python 3.7+
- `requests` library

### Installation

```bash
# Install required dependencies
pip install requests

# Or if using the project virtual environment
source .venv/bin/activate
pip install requests
```

## 📱 Tools

### 1. Kilkenny Station Arrivals

Shows all trains arriving at Kilkenny Station in the next 4 hours.

**Usage:**
```bash
python tools/kilkenny_station_arrivals.py
```

**Features:**
- ✅ Real-time arrival information
- ✅ Shows origin, destination, and train type
- ✅ Displays delay information
- ✅ Shows last known location
- ✅ Sorted by arrival time

**Sample Output:**
```
================================================================================
                    KILKENNY STATION - TRAIN ARRIVALS
                       Updated: 2025-12-17 18:30:00
================================================================================

Train #1
  Train Code:    A524
  From:          Dublin Heuston
  To:            Waterford
  Type:          Train
  Direction:     To Waterford
  Due In:        15 minutes
  Arrival:       18:45 (scheduled: 18:45)
  Departure:     18:50 (scheduled: 18:50)
  Status:        En Route - ✓ On time
  Last Location: Departed Athy
--------------------------------------------------------------------------------

Total trains: 3
```

### 2. Partner Train Tracker 💕

Personalized tracker for the 19:08 Dublin Heuston → Kilkenny train with pickup timing.

**Usage:**
```bash
python tools/partner_train_tracker.py

# Or create an alias for quick access
alias wherebae='python tools/partner_train_tracker.py'
```

**Features:**
- 💚 Tracks the 19:08 train specifically
- 🚗 Calculates when to leave for pickup (25 min drive + 5 min buffer)
- ⏰ Smart countdown and arrival alerts
- 🎯 Shows real-time location
- 😄 Fun, personalized messages based on delays
- 📊 Shows all other Dublin → Kilkenny trains

**Configuration:**

Edit these values in the script to customize:
```python
self.drive_time_minutes = 25  # Your drive time to station
self.buffer_minutes = 5       # Buffer for parking/walking
```

**Sample Output:**
```
================================================================================
                        🚂💕 PARTNER TRAIN TRACKER 💕🚂
                  Tracking the sacred 19:08 Heuston → Kilkenny
                               Updated: 18:30:00
================================================================================

🎯 FOUND YOUR HUMAN'S TRAIN!
────────────────────────────────────────────────────────────────────────────────

🚂 Train Code: A524
🏰 Started from: Dublin Heuston at 17:37
🏠 Getting off at: Kilkenny
🚂 Train continues to: Waterford

🌾 CURRENT LOCATION: Departed Athy
🚄 Status: En Route

⏰ ARRIVING IN: 38 minutes
   📺 Still time for another episode...

📅 Scheduled Arrival: 19:08
🎯 Expected Arrival:  19:08

✨ ON TIME! Irish Rail is showing off today!

================================================================================
                           🚗 PICKUP MISSION CONTROL 🚗
────────────────────────────────────────────────────────────────────────────────
Current time: 18:30
Train arrives: 19:08
Drive time: 25 min
Buffer (parking/walking): 5 min
You'll arrive at station: 19:03

                          ⏰ Leave in 8 minutes
                       Time to start wrapping things up!

                    🕐 Suggested departure time: 18:38
================================================================================
```

## 🎨 Features in Detail

### Delay Messages

The Partner Train Tracker includes fun, context-aware messages based on delay severity:

- **On Time:** "✨ ON TIME! Irish Rail is showing off today!"
- **1-3 min late:** "🤷 Time to blame the leaves/sun/wrong kind of rain"
- **4-10 min late:** "😬 Still time to tidy that passenger seat!"
- **10+ min late:** "🆘 MINUTES LATE! Probably stuck behind a cow at Cherryville"

### Pickup Timing Alerts

Smart alerts based on when you need to leave:

- **😌 20+ minutes:** "Plenty of time! They're still ages away"
- **🧘 10-20 minutes:** "Relax, you've got time. Finish that tea"
- **⏰ 5-10 minutes:** "Time to start wrapping things up!"
- **⚡ 1-5 minutes:** "GRAB YOUR KEYS AND GO RIGHT NOW!"
- **🚨 Past time:** "LEAVE NOW! LEAVE NOW! LEAVE NOW!"

### Location Emojis

Visual indicators for train locations:
- 🏰 Dublin
- 🚉 Heuston
- 🐴 Kildare
- 🌾 Athy
- 🌲 Carlow
- 🏠 Kilkenny

## 🔧 Technical Details

### API Information

Both scripts use the official Irish Rail Real-Time API:
- **Base URL:** `http://api.irishrail.ie/realtime/realtime.asmx`
- **Endpoint:** `getStationDataByNameXML`
- **No API key required**
- **Free to use**

### Data Refresh

The scripts fetch live data on each run. For continuous monitoring:

```bash
# Run every 2 minutes (macOS/Linux)
watch -n 120 python tools/partner_train_tracker.py

# Or create a simple loop
while true; do
    python tools/partner_train_tracker.py
    sleep 120
done
```

### XML Namespace

The Irish Rail API uses XML with namespace:
```python
ns = {'ir': 'http://api.irishrail.ie/realtime/'}
```

All element queries must include this namespace.

## 🛠️ Troubleshooting

### "No arrivals found"

**Possible causes:**
1. No trains scheduled in the next 4 hours
2. Train hasn't departed yet (shows ~1 hour before departure)
3. Internet connectivity issues
4. Irish Rail API is down

**Solutions:**
- Check Irish Rail website for schedule
- Ensure internet connection
- Try again in a few minutes

### Wrong Train Showing

The Partner Tracker looks for trains with scheduled arrival at 19:08 or 19:15. 
To track a different time, modify this line:

```python
if '19:08' in scheduled or '19:15' in scheduled:
```

### Timing Calculations Off

Adjust your drive time and buffer:

```python
self.drive_time_minutes = 25  # Change this
self.buffer_minutes = 5       # And this
```

## 📝 Code Quality

Both scripts follow PEP8 standards:
- ✅ Maximum line length: 79 characters
- ✅ Proper imports organization
- ✅ Type hints included
- ✅ Docstrings for all functions
- ✅ Error handling for API failures

## 🤝 Contributing

Feel free to enhance these scripts:
- Add SMS/email notifications
- Create a web interface
- Add support for other stations
- Include weather information
- Track multiple trains

## 📄 License

These scripts are for personal use. Irish Rail API terms apply.

## 🙏 Acknowledgments

- Irish Rail for providing the public API
- Built with ❤️ for never missing a pickup

## 📞 Support

For Irish Rail schedule inquiries: [www.irishrail.ie](https://www.irishrail.ie)

---

**Pro Tip:** Add the Partner Tracker to your shell profile for quick access:
```bash
# Add to ~/.zshrc or ~/.bashrc
alias wherebae='python ~/path/to/partner_train_tracker.py'
```

Then just type `wherebae` anytime! 🚂💕
