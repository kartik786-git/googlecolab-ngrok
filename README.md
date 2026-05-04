# Google Colab Ngrok Setup

This guide provides step-by-step instructions to set up Ngrok with Google Colab for exposing your local server to the internet.

## Prerequisites

Before you begin, ensure you have the following:
- A Google Colab account.
- Your Ngrok authentication token (you can find this in the Ngrok dashboard).

## Step 1: Install Required Tools

In the first cell of your Google Colab notebook, run the following commands to install necessary tools:

```python
# Install zstd, a fast lossless compression tool often used for handling large model files
!sudo apt-get install zstd 

# Download and run the official Ollama installation script to set up the local AI runner
!curl -fsSL https://ollama.com/install.sh | sh 

# Download the compressed archive for Ngrok, which allows you to expose your local server to the internet
!wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz 

# Extract (unzip) the Ngrok files so the application can be executed
!tar xvzf ngrok-v3-stable-linux-amd64.tgz 
```

## Step 2: Configure Ngrok

In the second cell, set up Ngrok with your authentication token:

```python
from google.colab import userdata

# Get your secret Ngrok token from Colab's "Secrets" (left sidebar 🔑 icon)
auth_token = userdata.get('NGROK_AUTH_TOKEN') 

# Add the token to Ngrok configuration
!./ngrok authtoken {auth_token} 
```

## Step 3: Start the Server and Ngrok Tunnel

Now, start the Ollama server and the Ngrok tunnel together:

```python
# Start the Ollama server and the Ngrok tunnel simultaneously
# Wait 10 seconds for the server to wake up, then start the AI model
!ollama serve & ./ngrok http 11434 --host-header="localhost:11434" --domain="your domain name" --log stdout & sleep 5s && ollama run gemma4:e4b
```

## Output

After running the above commands, you should see output indicating that the server is running and the Ngrok tunnel is active. You can now access your local server via the Ngrok URL provided in the output.

## Troubleshooting

If you encounter any issues, check the following:
- Ensure your Ngrok token is correctly set.
- Verify that the server is running and accessible.

Feel free to reach out for further assistance!
