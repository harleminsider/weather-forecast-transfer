# weather-forecast-transfer
import requests

def get_weather(city):
    api_key = "your_api_key_here"  # Replace with your actual API key
    base_url = "http://api.openweathermap.org/data/2.5/weather"
    
    params = {
        "q": city,
        "appid": api_key,
        "units": "metric"
    }
    
    response = requests.get(base_url, params=params)
    if response.status_code == 200:
        data = response.json()
        weather = {
            "city": data["name"],
            "temperature": data["main"]["temp"],
            "humidity": data["main"]["humidity"],
            "weather": data["weather"][0]["description"]
        }
        return weather
    else:
        return {"error": "Could not fetch weather data."}

def send_weather_report(city, recipient):
    weather_data = get_weather(city)
    
    if "error" in weather_data:
        print(weather_data["error"])
        return
    
    message = (f"🌦 Weather Forecast for {weather_data['city']} 🌦\n"
               f"Temperature: {weather_data['temperature']}°C\n"
               f"Humidity: {weather_data['humidity']}%\n"
               f"Condition: {weather_data['weather']}")
    
    # Simulate sending (In real case, integrate with an email/SMS API)
    print(f"Sending weather report to {recipient}:")
    print(message)
    
# Example usage
city_name = "London"
recipient_email = "example@example.com"
send_weather_report(city_name, recipient_email)
fregtrb
