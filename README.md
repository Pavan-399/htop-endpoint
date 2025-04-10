# htop-endpointvk
pip install -r requirements.txt
python app.py
from flask import Flask
import os
import subprocess
import datetime
import pytz

app = Flask(__name__)

@app.route('/htop')
def htop():
    name = "Pavan Kumar Reddy"  # Your full name
    username = os.getlogin()

    # Get current IST time
    ist = pytz.timezone('Asia/Kolkata')
    time_now = datetime.datetime.now(ist).strftime('%Y-%m-%d %H:%M:%S %Z')

    # Get top command output (first 20 lines for brevity)
    try:
        top_output = subprocess.check_output(['top', '-b', '-n', '1']).decode('utf-8')
        top_lines = '\n'.join(top_output.split('\n')[:20])
    except Exception as e:
        top_lines = f"Error running top: {e}"

    return f"""
    <h1>System Monitor</h1>
    <p><strong>Name:</strong> {name}</p>
    <p><strong>Username:</strong> {username}</p>
    <p><strong>Server Time (IST):</strong> {time_now}</p>
    <pre>{top_lines}</pre>
    """

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
flask
pytz
