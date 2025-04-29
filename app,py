from flask import Flask, render_template, request

app = Flask(__name__)

# City database
cities = [
    {"name": "Riyadh", "region": "central", "climate": "hot", "tripType": "culture", "budget": "high", "transport": "plane", "ageGroup": "young"},
    {"name": "Khobar", "region": "east", "climate": "hot", "tripType": "relax", "budget": "mid", "transport": "car", "ageGroup": "middle-aged"},
    {"name": "Al Ahsa", "region": "east", "climate": "hot", "tripType": "culture", "budget": "low", "transport": "car", "ageGroup": "senior"},
    {"name": "Jeddah", "region": "west", "climate": "hot", "tripType": "relax", "budget": "high", "transport": "plane", "ageGroup": "young"},
    {"name": "AlUla", "region": "west", "climate": "hot", "tripType": "adventure", "budget": "high", "transport": "plane", "ageGroup": "young"},
    {"name": "Red Sea Project", "region": "west", "climate": "hot", "tripType": "relax", "budget": "high", "transport": "plane", "ageGroup": "middle-aged"},
    {"name": "Abha", "region": "south", "climate": "cold", "tripType": "relax", "budget": "mid", "transport": "plane", "ageGroup": "middle-aged"},
    {"name": "Al Taif", "region": "west", "climate": "cold", "tripType": "relax", "budget": "mid", "transport": "car", "ageGroup": "senior"},
    {"name": "Jazan", "region": "south", "climate": "hot", "tripType": "adventure", "budget": "low", "transport": "plane", "ageGroup": "young"}
]

@app.route('/')
def home():
    lang = request.args.get('lang', 'en')  # Language selector
    return render_template('index.html', lang=lang)

@app.route('/quiz', methods=['GET', 'POST'])
def quiz():
    if request.method == 'POST':
        age = int(request.form['age'])
        climate = request.form['climate']
        budget = request.form['budget']
        tripType = request.form['tripType']
        transport = request.form['transport']
        region = request.form['region']

        if 18 <= age <= 30:
            ageGroup = "young"
        elif 31 <= age <= 50:
            ageGroup = "middle-aged"
        else:
            ageGroup = "senior"

        scores = []
        for city in cities:
            score = 0
            if city["region"] == region: score += 2
            if city["climate"] == climate: score += 2
            if city["tripType"] == tripType: score += 2
            if city["budget"] == budget: score += 1
            if city["transport"] == transport: score += 1
            if city["ageGroup"] == ageGroup: score += 1
            scores.append((city["name"], score))

        scores.sort(key=lambda x: x[1], reverse=True)
        top_cities = scores[:3]

        return render_template('quiz.html', result=top_cities)

    return render_template('quiz.html', result=None)

@app.route('/city/<cityname>')
def city_page(cityname):
    return f"<h1>Welcome to {cityname.title()}!</h1><p>More info about {cityname} coming soon.</p><a href='/'>Back to Home</a>"

if __name__ == '__main__':
    app.run(debug=True)

