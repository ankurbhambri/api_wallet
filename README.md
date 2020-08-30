Requirement for this project for setup:

-> Create a vitual environment.
== virtualenv -p python3.6 venv
-> Activate your virtual environment using this command
== source venv/bin/activate
-> Install required python libraries by using pip installer.
== pip install -r requirements.txt
-> Migrate database.
== python manage.py migrate
-> Finally, run your django runserver.
== python manage.py runserver



# Rest Framework Auth Token for Authentication
--To generate a token, just for testing purpose, is using the command line utility again
Ex - python manage.py drf_create_token root


# JWT based authentication
--To authenticate and obtain the token. The endpoint is /api/token/ and it only accepts POST requests.
Ex - http post http://127.0.0.1:8000/api/token/ username=vitor password=root

# Please keep these things in mind while authenticating using JWT
The JWT is acquired by exchanging an username + password for an access token and an refresh token.

The access token is usually short-lived (expires in 5 min or so, can be customized though).

The refresh token lives a little bit longer (expires in 24 hours, also customizable). It is comparable to an authentication session. After it expires, you need a full login with username + password again.

--To get a new access token, you should use the refresh token endpoint /api/token/refresh/ posting the refresh token:
Ex - http post http://127.0.0.1:8000/api/token/refresh/ refresh="Put previous refresh token here"


# Post API 1 endpoint that allows users to see wallet details.
	request
	{
	    "username": "ankur1",
	    "password": "root"
	}
	response
	{
    "id": 29,
    "username": "ankur1"
	}
Ex-  http://localhost:8000/users/ 


# Post API 2 endpoint that allows users to see wallet details.
	response
	{
        "id": 2,
        "balance": 40.0,
        "user_upi": "ankur@27"
    }
Ex-  http://localhost:8000/wallet_details/

# Post API 3 endpoint that allows users to be Add Amount.
    request 
    {
        "amount": ""
    }
    response
	{
	    "user_upi": "ankur@27",
	    "balance": 40.0,
	    "amount": 20,
	    "status": "Amount Added To Your Wallet Sucessfully"
	}
Ex-  http://localhost:8000/add_amount/

# Post API 4 endpoint that allows users to be Pay Amount.
    request 
    {
        "user_upi": "",
        "pay_amount": ""
    }
    response
    {
	    "sender": "ankur@27",
	    "receiver": "root@26",
	    "transaction_type": "debited",
	    "deducted_amount": 20,
	    "balance_left": 20.0
	}
Ex-  http://localhost:8000/pay_amount/ 

# API 5 endpoint that prints a user month wise transactions.
	response
	{
	    "user_upi": "ankur@27",
	    "user_name": "ankur",
	    "current_month_credited_amount": 60,
	    "current_month_deducted_amount": 20,
	    "wallet_balance": 40.0
	}
Ex-  http://localhost:8000/all_transactions/