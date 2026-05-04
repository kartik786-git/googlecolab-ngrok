# googlecolab-ngrok

# first cell
!sudo apt-get install zstd # Install zstd, a fast lossless compression tool often used for handling large model files
!curl -fsSL https://ollama.com/install.sh | sh # Download and run the official Ollama installation script to set up the local AI runner
!wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz # Download the compressed archive for ngrok, which allows you to expose your local server to the internet
!tar xvzf ngrok-v3-stable-linux-amd64.tgz # Extract (unzip) the ngrok files so the application can be executed


# second cell
from google.colab import userdata
auth_token = userdata.get('NGROK_AUTH_TOKEN') # 1. Get your secret ngrok token from Colab's "Secrets" (left sidebar 🔑 icon)
!./ngrok authtoken {auth_token} # 2. Add the token to ngrok configuration
# 3. Start the Ollama server and the ngrok tunnel together in the background
# We use & to run them simultaneously without blocking the next command
# 4. Wait 10 seconds for the server to wake up, then start the AI model
!ollama serve & ./ngrok http 11434 --host-header="localhost:11434" --domain="your domain name" --log stdout & sleep 5s && ollama run gemma4:e4b

<img width="1876" height="905" alt="image" src="https://github.com/user-attachments/assets/7f32904b-6b68-494b-9932-e4f8f71bcb2e" />

<img width="1439" height="993" alt="image" src="https://github.com/user-attachments/assets/d815d547-db15-44f5-9a79-07c148e9b4fe" />

<img width="904" height="327" alt="image" src="https://github.com/user-attachments/assets/683cf8a4-1a0b-400d-bd3b-2b0769a90afb" />
<img width="1871" height="859" alt="image" src="https://github.com/user-attachments/assets/86546f8c-0000-4a13-a6c7-d2e5df6d73e1" />
