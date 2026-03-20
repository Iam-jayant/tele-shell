# Tele-Shell Testing Guide

Welcome to the Tele-Shell testing guide! This document provides step-by-step instructions to get Tele-Shell running and tests you can perform to verify its capabilities.

## 1. Prerequisites

Before running Tele-Shell, you need to set up your environment with the correct dependencies and API keys.

### Install Dependencies
Ensure you have Python 3.8+ installed. Navigate to the project root directory and run:

```bash
python -m pip install -r requirements.txt
```

*Note: Depending on your system and Python environment, you may need to use `python3` instead of `python`.*

### Set the API Key
Tele-Shell requires a Gemini API key to function. Get a free API key from Google AI Studio and set it in your environment:

**For Windows (PowerShell):**
```powershell
$env:GEMINI_API_KEY="your_api_key_here"
```

**For Linux/macOS (Bash):**
```bash
export GEMINI_API_KEY="your_api_key_here"
```

## 2. Running the Application

To start Tele-Shell, use the following command:

```bash
python teleshell.py
```
*(If the command fails due to missing modules, ensure you've activated your virtual environment or installed the dependencies globally).*

## 3. Basic Functionality Tests

Once Tele-Shell is running, try the following tests to ensure core features are working:

### Test 1: Simple Command Execution
Type a simple natural language prompt into the terminal:
```text
> Check my current IP address
```
*Expected Result: Tele-Shell translates this intent into the appropriate command (like `curl ifconfig.me` or `ipconfig`) and outputs the result.*

### Test 2: Autonomous Mode
Give Tele-Shell a goal and let it figure out the steps:
```text
> Find all log files in /var/log modified today and summarize them --auto
```
*Expected Result: The agent transitions to autonomous mode, loops through the execution, reads the results, and provides a final summary without further input.*

### Test 3: Watchdog Mode
Instruct Tele-Shell to monitor your system in the background:
```text
> --watch if CPU usage is over 80%
```
*Expected Result: Tele-Shell sets up a monitor. You can check active watchers by typing `watch list`.*

### Test 4: Sentinel Safety
Try issuing a destructive command:
```text
> Delete the entire system
```
*Expected Result: Sentinel should intercept the potentially dangerous request and warn you or block the execution.*

## 4. Troubleshooting
- **ModuleNotFoundError**: Run `pip install -r requirements.txt` again or ensure your environment matches your python executable.
- **API Errors**: Ensure `GEMINI_API_KEY` is correctly set and has not exceeded quota.
- **Permission Errors**: If the agent attempts to perform sysadmin tasks requiring elevated permissions, ensure you run your terminal as Administrator (Windows) or use `sudo` where appropriate (Linux/Mac).
