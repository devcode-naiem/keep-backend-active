[![Keep Backend Active](https://github.com/devcode-naiem/keep-backend-active/actions/workflows/keep-backend-active.yml/badge.svg)](https://github.com/devcode-naiem/keep-backend-active/actions/workflows/keep-backend-active.yml)
# Keep Backend Active

A GitHub Actions workflow to ensure your backend remains active by periodically pinging it. This solution is free, lightweight, and fully integrated into your codebase, eliminating the need for third-party services or external monitoring tools. It ensures that free-tier backends (like Render or Heroku) do not go idle due to inactivity, improving response times for users.

---

## 🚀 Why Use This Workflow?

### **Key Benefits**
- **Free to Use**: Leverages GitHub Actions, which is free for public repositories and includes a generous free tier for private ones.
- **No Third-Party Services**: No need for additional services like UptimeRobot or external cron jobs. Everything is self-contained in your repository.
- **Customizable**: Fully configurable workflow, allowing you to adjust the ping frequency, logging, and failure handling to suit your needs.
- **Professional-Grade**: Includes retry logic, robust error handling, and instant notifications via GitHub’s built-in email alerts.
- **Open Source**: You can clone, copy, or adapt this workflow for your own projects.

---

## 🛠️ How It Works

### **Core Features**
1. **Scheduled Pings**:
   - Sends periodic requests to your backend to prevent it from going idle.
   - Configured to run every 5 minutes by default (adjustable via a cron job).

2. **Retry Logic**:
   - Automatically retries ping requests if the backend does not respond as expected.

3. **Failure Handling**:
   - Logs detailed error messages.
   - Sends email notifications via GitHub if the backend is unresponsive.

4. **Customizable Environment Variables**:
   - Easily update the backend URL and other parameters without modifying the workflow file.

5. **Detailed Logging**:
   - Tracks response times, HTTP status codes, and other metrics.

---

## 🧑‍💻 Setup Instructions

### **1. Clone or Copy the Repository**
You can either clone this repository or copy the workflow file into your existing project.

#### Clone:
```bash
git clone https://github.com/devcode-naiem/keep-backend-active.git
```

#### Copy the Workflow File:
1. Navigate to `.github/workflows/keep-backend-active.yml` in this repository.
2. Copy the file into the `.github/workflows/` directory of your project.

---

### **2. Configure Environment Variables**
1. Go to your repository’s **Settings** > **Secrets and variables** > **Actions**.
2. Add a new secret:
   - **Name**: `BACKEND_API_URL`
   - **Value**: Your backend’s health check endpoint (e.g., `https://your-backend.com/api/health`).

---

### **3. Customize the Workflow**
- Adjust the cron schedule in the workflow file (`*/5 * * * *` for every 5 minutes).
- Update retry logic, notification methods, or add integrations (Slack, Discord, etc.) as needed.

---

### **4. Monitor Workflow Execution**
- Go to the **Actions** tab in your repository.
- Check the logs of the workflow runs for successful pings or failure details.

---

## 📌 Example Use Cases

- **Prevent Free-Tier Backends from Going Idle**: Avoid delays caused by "cold starts" on platforms like Render, Heroku, or Vercel.
- **Monitor Backend Health**: Ensure your backend responds as expected and receive instant failure notifications.
- **Simplify Operations**: Eliminate dependency on third-party uptime services.

---

## ⚙️ Advanced Features

### **1. Retry Logic**
- Automatically retries failed requests to avoid false negatives.

### **2. Instant Notifications**
- Uses GitHub’s built-in email notifications for failures.

### **3. Metrics Tracking**
- Logs response times and HTTP status codes for debugging and optimization.

---

## 🤝 Contributions

Contributions are welcome! Feel free to open an issue or submit a pull request to suggest improvements or report bugs.

---

## 📜 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## 🛎️ Support

If you find this project useful, please consider starring the repository to show your support!

---

## 💡 Feedback

Have suggestions or feedback? Open an issue or reach out via GitHub Discussions.

---

## 📂 Example Workflow File

```yaml
name: Keep Backend Active

on:
  schedule:
    - cron: '*/5 * * * *' # Run every 5 minutes
  workflow_dispatch:

jobs:
  keep-backend-alive:
    runs-on: ubuntu-latest

    env:
      BACKEND_API_URL: ${{ secrets.BACKEND_API_URL }}
      EXPECTED_STATUS_CODE: 200

    steps:
      - name: Log Workflow Start
        run: echo "Starting Keep Backend Active workflow at $(date)"

      - name: Ping Backend API
        run: |
          RESPONSE=$(curl -s -o /dev/null -w "%{http_code}" $BACKEND_API_URL)
          echo "Received HTTP status code: $RESPONSE"
          if [ "$RESPONSE" -ne "$EXPECTED_STATUS_CODE" ]; then
            exit 1
          fi

      - name: Log Success
        run: echo "Backend is active. Workflow completed successfully."
```

---

With this repository, you can ensure your backend remains active and responsive without relying on external services. It’s free, customizable, and fits seamlessly into your existing GitHub Actions workflows. Happy coding!


