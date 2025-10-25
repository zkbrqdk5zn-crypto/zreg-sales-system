# zreg-sales-system
زريق لمواد البناء 
from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

# بيانات مؤقتة
users = {'admin':'admin'}
products = [{'name':'اسمنت','price':50,'quantity':100},
            {'name':'حديد','price':200,'quantity':50}]

@app.route('/')
def index():
    return render_template('index.html', products=products)

@app.route('/login', methods=['GET','POST'])
def login():
    if request.method=='POST':
        username = request.form['username']
        password = request.form['password']
        if username in users and users[username]==password:
            return redirect(url_for('index'))
        else:
            return "اسم المستخدم أو كلمة المرور خاطئة"
    return render_template('login.html')

if __name__=="__main__":
    app.run(host='0.0.0.0', port=5000, debug=True)
