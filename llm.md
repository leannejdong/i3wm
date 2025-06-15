# Building with AI

## Ollama

### Install
```
curl -fsSL https://ollama.com/install.sh | sh
ollama pull mistral:7b-instruct-q4_0  # Quantized 4-bit
ollama serve &  # Runs API at localhost:11434
```

### Run

1. Method 1
```
ollama run mistral
```
2. via docker
```
ollama pull mistral  # Or replace "mistral" with "llama3", "gemma", etc.
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:main
```

Access the Web Interface
Go to http://localhost:3000 in your browser.

Sign up (first user is admin).

Select your model (e.g., mistral) and start chatting!

`docker rm open-webui`

### Removal
To completely remove Ollama from Arch Linux, you should first stop and disable the Ollama service, then remove the binary and any associated files, and finally remove any created user and group. This ensures a clean uninstall. 
Here's a breakdown of the steps: 
Stop and Disable the Ollama Service:
If Ollama was installed as a systemd service, stop it:

`sudo systemctl stop ollama`
Disable the service to prevent it from starting on boot:
`sudo systemctl disable ollama`
Remove the Ollama Binary and Systemd Service File: 
Remove the Ollama executable. The location might vary, but a common location is /usr/local/bin/ollama. 

`sudo rm /usr/local/bin/ollama`
If you created a systemd service file, remove it:
`sudo rm /etc/systemd/system/ollama.service`
Reload the systemd daemon to reflect the changes:
`sudo systemctl daemon-reload`
Remove Model Files (Optional, but recommended):
Ollama stores models in a specific directory. You can find it by checking the output of ollama list or by checking the default locations:
macOS: ~/.ollama/models
Linux: /usr/share/ollama/.ollama/models
Windows: C:\Users\%username%\.ollama\models 
Remove the model files. You can list and remove them individually using ollama rm <model_name> or remove the entire directory if you want to remove all models. 
If you want to remove all models, and you are certain you want to do so, you can use the following command: 
`ollama list | awk 'NR>2 {print $1}' | xargs -I {} ollama rm {}`
This command lists the models, extracts the names, and then uses ollama rm to remove each one. 
Remove the Ollama User and Group (If Applicable):
If Ollama installation created a dedicated user and group, remove them:
```
sudo userdel ollama
sudo groupdel ollama
```
Verify Removal:
Check if the Ollama binary is still present:
`type ollama`
If it's not found, it's been removed. 
If you removed the systemd service, it should no longer be listed:
`systemctl status ollama`
Remove Configuration Files (Optional):
While not strictly necessary, you can remove any remaining configuration files. These are often located in the user's home directory. For example, you might find files in ~/.ollama. 
By following these steps, you can ensure that Ollama is completely uninstalled from your Arch Linux system. 
