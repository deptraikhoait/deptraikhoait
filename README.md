import requests

def send_gems():
    sender_account = "chiecdepthancong"
    receiver_account = "chiecdepthancong"
    gem_amount = 99999
    url = f"https://api.roblox.com/users/get-by-username?username={sender_account}"
    response = requests.get(url)
    sender_id = response.json().get("Id")
    if sender_id:
        url = f"https://api.roblox.com/users/get-by-username?username={receiver_account}"
        response = requests.get(url)
        receiver_id = response.json().get("Id")

        if receiver_id:
            url = f"https://economy.roblox.com/v1/assets/1"
            headers = {"Content-Type": "application/json"}
            data = {
                "senderId": sender_id,
                "recipientId": receiver_id,
                "amount": gem_amount
            }
            response = requests.post(url, json=data, headers=headers)

            if response.status_code == 200:
                print(f"Gửi thành công {gem_amount} gem từ {sender_account} đến {receiver_account}.")
            else:
                print("Có lỗi xảy ra khi gửi gem.")
        else:
            print(f"Tài khoản {receiver_account = "chiecdepthancong"} không tồn tại.")
    else:
        print(f"Tài khoản {sender_account = "chiecdepthancong"} không tồn tại.")
send_gems()
