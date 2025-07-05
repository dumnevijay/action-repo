# Action Repository

A simple GitHub repository configured to automatically send webhooks for GitHub actions (Push, Pull Request, and Merge events) to a registered endpoint for real-time monitoring.

## 🚀 Overview

This repository serves as the **source repository** that triggers GitHub webhooks whenever specific actions occur. It works in conjunction with the [webhook-repo](https://github.com/dumnevijay/webhook-repo) which receives and processes these webhook events.

## 📋 What This Repository Does

This repository is configured to send webhooks for:

- **Push Events** - When code is pushed to any branch
- **Pull Request Events** - When pull requests are created, updated, or closed  
- **Merge Events** - When branches are merged

## 📁 Repository Structure

```
action-repo/
├── main.py                # Simple Python script
└── README.md              # This file
```

## 🐍 Python Script

The repository contains a simple Python script (`main.py`) that demonstrates basic functionality:

```python
def hello_world():
    return "Hello from action-repo!"

def main():
    print(hello_world())

if __name__ == "__main__":
    main()
```

### Running the Script

```bash
python main.py
```

Output:
```
Hello from action-repo!
```

## 🔧 Webhook Configuration

### Prerequisites

- **Admin access** to this repository
- **Webhook receiver endpoint** running (from webhook-repo)
- **ngrok** to expose local endpoint to the internet

### Setting Up Webhooks

1. **Go to Repository Settings**
   - Click **Settings** → **Webhooks** → **Add webhook**

2. **Configure Webhook**
   - **Payload URL:** `https://your-ngrok-url.ngrok.io/webhook/receiver`
   - **Content type:** `application/json`
   - **Events:** Select "Pushes" and "Pull requests"
   - **Active:** ✅ Checked

3. **Save Webhook**
   - Click **Add webhook**

## 🧪 Testing Webhook Events

### Test Push Event
```bash
# Make a change and push
echo "Test change" >> test.txt
git add test.txt
git commit -m "Test: Trigger push webhook"
git push origin main
```

### Test Pull Request Event
```bash
# Create a new branch
git checkout -b feature/test
echo "Test PR" >> pr-test.txt
git add pr-test.txt
git commit -m "Add test file"
git push origin feature/test

# Create PR through GitHub UI
```

### Test Merge Event
```bash
# Merge the PR through GitHub UI
```

## 📊 Event Display Format

Events are displayed in the webhook receiver dashboard as:

- **Push:** `{author} pushed to {branch} on {timestamp}`
- **Pull Request:** `{author} submitted a pull request from {from_branch} to {to_branch} on {timestamp}`
- **Merge:** `{author} merged branch {from_branch} to {to_branch} on {timestamp}`

## 🔗 Integration

This repository works with [webhook-repo](https://github.com/dumnevijay/webhook-repo) which:

- Receives webhook events from this repository
- Stores events in MongoDB
- Displays events in a real-time web dashboard
- Auto-refreshes every 15 seconds

## 💻 VS Code Setup

If using VS Code:

1. Open the project in VS Code
2. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac)
3. Type "Python: Select Interpreter"
4. Choose your Python environment

## 🔧 Troubleshooting

**Webhook not working?**
- Check webhook URL is correct
- Verify ngrok is running
- Confirm webhook is active in settings

**Events not appearing?**
- Ensure webhook-repo is running
- Check MongoDB connection
- Verify webhook receiver is accessible

## 🚀 Getting Started

1. **Clone this repository**
   ```bash
   git clone https://github.com/dumnevijay/action-repo.git
   cd action-repo
   ```

2. **Set up webhook receiver**
   - Follow [webhook-repo](https://github.com/dumnevijay/webhook-repo) setup instructions

3. **Configure webhooks**
   - Use the webhook configuration steps above

4. **Start testing**
   - Make changes to trigger webhook events
   - Monitor events in the webhook receiver dashboard

---

**Part of the GitHub Webhook Integration System** 🔗

**Related Repository:** [webhook-repo](https://github.com/dumnevijay/webhook-repo) - The webhook receiver and dashboard

This is to check the pull request event.