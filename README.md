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
