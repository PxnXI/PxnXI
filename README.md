import random
import requests

def get_lottery_results():
  """ดึงข้อมูลผลรางวัลสลากกินแบ่งรัฐบาลย้อนหลัง"""
  url = "https://www.glo.lotto.go.th/th/lotto/history"
  response = requests.get(url)
  if response.status_code == 200:
    data = response.json()
    lottery_results = []
    for result in data["results"]:
      lottery_results.append(result["prize_number_1"])
    return lottery_results
  else:
    print("Error: Failed to fetch lottery results")
    return []

def generate_random_number():
  """ฟังก์ชันสุ่มตัวเลข 6 ตัว โดยไม่ซ้ำกับผลรางวัลที่ออกแล้ว"""
  lottery_results = get_lottery_results()
  while True:
    random_number = generate_random_number_helper()
    if random_number not in lottery_results:
      return random_number

def generate_random_number_helper():
  """ฟังก์ชันสุ่มตัวเลข 6 ตัว"""
  random_number = ""
  for _ in range(6):
    random_digit = str(random.randint(0, 9))
    random_number += random_digit
  return random_number

# ตัวอย่างการใช้งาน
random_number = generate_random_number()
print(random_number)
