Using nohup
The nohup command, standing for "no hangup," allows a command to continue running in the background after you log out from a shell:

sh
Copy code
nohup your-command > output.log 2>&1 &

### Using PowerShell Jobs:

PowerShell jobs are another way to run a script in the background. While they don't directly mimic `nohup`, they are useful for asynchronous task execution. Here's how you can start a Python script as a background job:

powershellCopy code

`Start-Job -ScriptBlock { python .\app.py *> output.log }`