# sturdy-funicular
vulnerable_app.py
from flask import Flask, request, render_template_string

app = Flask(__name__)

# Disclaimer: This login mechanism is deliberately insecure.
# It is provided for educational purposes only to demonstrate a potential bypass vulnerability.
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        username = request.form.get('username')
        password = request.form.get('password')
        # Vulnerable logic: bypass authentication if username is "admin"
        if username == "admin":
            return "Access Granted: Logged in as admin (vulnerable bypass demonstration)."
        else:
            return "Access Denied."
    
    # Simple login form for demonstration
    return render_template_string('''
        <h2>Login</h2>
        <form method="post">
            Username: <input type="text" name="username" required><br>
            Password: <input type="password" name="password" required><br>
            <input type="submit" value="Login">
        </form>
    ''')

if __name__ == '__main__':
    # Run in debug mode on localhost only
    app.run(debug=True)
