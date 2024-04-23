def get_email_otp(email):
    otp = -1
    condition_one = False
    condition_two = False
    condition_three = False
    condition_four = False
    condition_five = False



    if len(email) > 12:
        otp = 10
        condition_one = True
    if email.split(".")[-1].lower() in ('org', 'in'):
        otp = 11
        condition_two = True
    if email[5] in (',', '_'):
        otp = 12
        condition_three = True
    if email[:2].lower() == email[-2:]:
        otp = 13
        condition_four = True
    if any(char.isdigit() for char in email):
        condition_five = True
        indices_sum = 0
        for idx,char in enumerate(email):
            if char.isdigit():
                indices_sum += idx
        otp = indices_sum

    if all([condition_one, condition_two, condition_three, condition_five, condition_four]):
        otp = 10 + 11 + 12 + 13 + indices_sum

    return otp

email_lst = ['stevesmith@abc.com',
             'str@abc.in',
             'smith_a@a.us',
             'Usgano@s_us',
             'ac123@abc.co',
             'xy@xyz.co',
             'inest_s23@abc.in',
             'robinsingh@abc.com',
             'tommy@abc.in',
             'smith_a@a.co',
             'w123@ty.com',]

for email in email_lst:
    print(f"{email} : {get_email_otp(email)}")



<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
</head>
<body>
    <h1>Calculator</h1>
    <form action="/calculate" method="post">
        <label for="num1">Enter first number:</label>
        <input type="number" id="num1" name="num1" required>
        <label for="num2">Enter second number:</label>
        <input type="number" id="num2" name="num2" required>
        <label for="operation">Select operation:</label>
        <select id="operation" name="operation">
            <option value="add">Addition (+)</option>
            <option value="subtract">Subtraction (-)</option>
            <option value="multiply">Multiplication (*)</option>
            <option value="divide">Division (/)</option>
        </select>
        <button type="submit">Calculate</button>
    </form>
</body>
</html>

==================================

from flask import Flask, render_template, request

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/calculate', methods=['POST'])
def calculate():
    num1 = float(request.form['num1'])
    num2 = float(request.form['num2'])
    operation = request.form['operation']
    result = None

    if operation == 'add':
        result = num1 + num2
    elif operation == 'subtract':
        result = num1 - num2
    elif operation == 'multiply':
        result = num1 * num2
    elif operation == 'divide':
        if num2 != 0:
            result = num1 / num2
        else:
            return "Error: Cannot divide by zero"

    return render_template('result.html', num1=num1, num2=num2, operation=operation, result=result)

if __name__ == '__main__':
    app.run(debug=True)


    
