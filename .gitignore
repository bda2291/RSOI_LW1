import flask
import requests
import json
import webbrowser

choise = ""
client_id = "fpoobzspmsnfm02"
client_secret = "l2ig8e7dcz51jhc"
redirect_uri = "http://127.0.0.1:5000"
access_token = " "
base_url = "https://api.dropboxapi.com/1/"
base_url1 = "https://api.dropboxapi.com/2/"
base_url2 = "https://www.dropbox.com/1/oauth2/authorize"+\
            "?client_id="+client_id+\
            "&response_type=code"+\
            "&redirect_uri="+redirect_uri

def get_current_account():
    url = base_url1 + "users/get_current_account"
    headers = {
        "Authorization": "Bearer "+access_token,
        "Content-Type": "application/json"
    }
    data = None
    r = requests.post(url, headers=headers, data=json.dumps(data))
    try:
        print (r.json())
    except:
        print (r)

def shutdown_flask():
        func = flask.request.environ.get('werkzeug.server.shutdown')
        if func is None:
            raise RuntimeError('Not running with the Werkzeug Server')
        func()
        return "Done"

app = flask.Flask(__name__)

@app.route("/") 
def blabla():
    global access_token

    params = {
        "client_id": client_id,
        "client_secret": client_secret,
        "redirect_uri": redirect_uri,
        "grant_type": "authorization_code",
        "code": flask.request.args.get("code")
    }

    r = requests.post(base_url+"/oauth2/token", params=params).json()
    access_token = r['access_token']
    shutdown_flask()
    return "access_token= "+access_token

def register(): 
    webbrowser.open(base_url2)
    return app.run()

MENU = ('''
Варианты действий
    1. Запросить информацию о пользователе без авторизации.
    2. Запросить информацию о пользователе с предварительной авторизацией.
    3. Выход из программы.
    ''')
while choise != "3":
    print(MENU)
    choise = input("Выберите нужное Вам действие: ")
    if choise == "1":
        get_current_account()
        print("Требуется предварительная авторизация")
    elif choise == "2":
        register()
        get_current_account()
    elif choise == "3":
        print("Программа завершена")
    else:
        print("Пункта меню", str(choise), "не существует")
        input("Нажмите Enter, для продолжения...")
