#import requests

def get_weather(city):
    API_KEY = "YOUR_API_KEY"  # 여기에 OpenWeatherMap API 키 입력
    BASE_URL = "http://api.openweathermap.org/data/2.5/weather"
    
    params = {
        "q": city,
        "appid": API_KEY,
        "units": "metric",  # 섭씨 온도로 변환
        "lang": "kr"  # 한국어 지원
    }
    
    response = requests.get(BASE_URL, params=params)
    
    if response.status_code == 200:
        data = response.json()
        weather_desc = data["weather"][0]["description"]
        temp = data["main"]["temp"]
        humidity = data["main"]["humidity"]
        wind_speed = data["wind"]["speed"]
        
        print(f"도시: {city}")
        print(f"날씨: {weather_desc}")
        print(f"온도: {temp}°C")
        print(f"습도: {humidity}%")
        print(f"풍속: {wind_speed} m/s")
    else:
        print("날씨 정보를 가져오지 못했습니다. 도시 이름을 확인하세요.")

if __name__ == "__main__":
    city = input("날씨를 확인할 도시명을 입력하세요: ")
    get_weather(city)
