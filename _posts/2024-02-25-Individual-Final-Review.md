---
toc: true
comments: true
layout: post
title: Individual Review
courses: { csp: {week: 24} }
type: hacks
---

# AI Real Estate Bot

## Correlation to CPT
### User Input
- The user can input their prompt to the bot and click a button to submit the prompt.

```html
<form id="input-form">
    <input id="input-field" type="text" placeholder="Type your message here">
    <button id="submit-button" type="submit">Send</button>
</form>
```
- To get an answer, the user must input the access code to the bot.
```javascript
const accessCode = prompt("Please enter your access code:");
if (!accessCode) return; // Don't proceed without access code
```

### Use of at least 1 list
- I use a database to store all the properties available. This database has over 800 properties This makes my program easier to develop and easier to maintain.

```python
class House(db.Model, UserMixin):
    __tablename__ = 'houses'

    id = db.Column(db.Integer, primary_key=True)
    address = db.Column(db.String(256), index=True)
    city = db.Column(db.String(64), index=True, nullable=True)
    state = db.Column(db.String(8), index=True, nullable=True)
    zip = db.Column(db.Integer, index=True, nullable=True)
    latitude = db.Column(db.Float, index=True, nullable=True)
    longitude = db.Column(db.Float, index=True, nullable=True)
    price = db.Column(db.Integer, index=True, nullable=True)
    bathrooms = db.Column(db.Float, index=True, nullable=True)
    bedrooms = db.Column(db.Integer, index=True, nullable=True)
    livingarea = db.Column(db.Integer, index=True, nullable=True)
    homeType = db.Column(db.String(64), index=True, nullable=True)
    priceEstimate = db.Column(db.Integer, index=True, nullable=True)
    rentEstimate = db.Column(db.Integer, index=True, nullable=True)
    imgSRC = db.Column(db.String, index=True, nullable=True)
    favorites = db.relationship('Favorite', backref='House', uselist=True, lazy='dynamic')

    def __init__(self, address, city, state, zip, latitude, longitude, price, bathrooms, bedrooms, livingarea, homeType, priceEstimate, rentEstimate, imgSRC):
        self.address = address
        self.city = city
        self.state = state
        self.zip = zip
        self.latitude = latitude
        self.longitude = longitude
        self.price = price
        self.bathrooms = bathrooms
        self.bedrooms = bedrooms
        self.livingarea = livingarea
        self.homeType = homeType
        self.priceEstimate = priceEstimate
        self.rentEstimate = rentEstimate
        self.imgSRC = imgSRC

def initHouses():
    with app.app_context():
        """Create database and tables"""
        db.create_all()
        house_count = db.session.query(House).count()
        if house_count > 0:
            return

        basedir = os.path.abspath(os.path.dirname(__file__))
        # Specify the file path
        file_path = basedir + "/../static/data/RealEstateData.csv"
        # Load the CSV file into a DataFrame
        df = pd.read_csv(file_path)

        for index, row in df.iterrows():
            try:
                house = House(
                    address=row['address'] if pd.notna(row['address']) else None,
                    city=row['city'] if pd.notna(row['city']) else None,
                    state=row['state'] if pd.notna(row['state']) else None,
                    zip=row['zipcode'] if pd.notna(row['zipcode']) else None,
                    latitude=row['latitude'] if pd.notna(row['latitude']) else None,
                    longitude=row['longitude'] if pd.notna(row['longitude']) else None,
                    price=row['price'] if pd.notna(row['price']) else None,
                    bathrooms=row['bathrooms'] if pd.notna(row['bathrooms']) else None,
                    bedrooms=row['bedrooms'] if pd.notna(row['bedrooms']) else None,
                    livingarea=row['livingArea'] if pd.notna(row['livingArea']) else None,
                    homeType=row['homeType'] if pd.notna(row['homeType']) else None,
                    priceEstimate=row['PriceEstimate'] if pd.notna(row['PriceEstimate']) else None,
                    rentEstimate=row['RentEstimate'] if pd.notna(row['RentEstimate']) else None,
                    imgSRC=row['imgSrc'] if pd.notna(row['imgSrc']) else None
                )
                db.session.add(house)
                db.session.commit()
            except IntegrityError:
                '''fails with bad or duplicate data'''
                db.session.remove()
                print(f"Records exist, duplicate house, or error: {house.name}")
            except Exception as e_inner:
                print(f"Error adding house at index {index}: {str(e_inner)}")
```

### One procedure that contributes to the program’s intended purpose
- This procedure is used to get the user's input and return the bot's response. This is the main procedure that allows the bot to function.

```python
def get_openai_answer(user_input):
        encrypted_app_token = 'gAAAAABlOLQoLplaL2-lfD1T4VkBXnkKxq1XK_VlVHiEm7MaftNJmZ4f-7rQlUws-NIMHjpWOMtevkwB5NX7f4kqknvrVtwH3ccAsOHB_Yg9dzksRxh5yVuuIXRD3hov8yU6BSXwd-HLTnBRLX5ARDOqzxJoK6M15A=='

        basedir = os.path.abspath(os.path.dirname(__file__))

        # Specify the file path
        file_path = basedir + "/../static/data/RealEsateDataforOpenAI.csv"

        dataset = pd.read_csv(file_path, header=0).to_string()

        houses = db.session.query(House).all()
        dataset = []
        for house in houses:
            dataset.append(house.all_details())
        jsondata = jsonify(dataset)

        crypto_key = os.getenv("CRYPTO_KEY")
        if crypto_key is None:
            raise ValueError("CRYPTO_KEY environment variable is not set.")
        
        cipher_suite = Fernet(crypto_key)
        api_key = cipher_suite.decrypt(encrypted_app_token).decode()
        os.environ["OPENAI_API_KEY"] = api_key
        
        summary_template = """
            {user_input}, answer using this: {jsondata} If unable able to answer, use your own information.
        """

        summary_prompt_template = PromptTemplate(
            input_variables=["user_input", "dataset"], template=summary_template
        )

        llm = ChatOpenAI(temperature=0, model_name="gpt-3.5-turbo-16k", api_key=api_key)

        chain = LLMChain(llm=llm, prompt=summary_prompt_template)
        response = chain.run(user_input=user_input, dataset=dataset)
        
        return response
```

### An algorithm that includes sequencing, selection, and iteration
- The loop or iteration extracts all information on all properties, which is vital for the bot to properly answer prompts. The sequencing is important in checking if the user has the access code to the bot. If not an error will be thrown

```python
houses = db.session.query(House).all()
        dataset = []
        for house in houses:
            dataset.append(house.all_details())
        jsondata = jsonify(dataset)

        crypto_key = os.getenv("CRYPTO_KEY")
        if crypto_key is None:
            raise ValueError("CRYPTO_KEY environment variable is not set.")
```

### Calls to your student-developed procedure
- This calls the AI bot api to get the response to the user's prompt.

```javascript
document.addEventListener("DOMContentLoaded", function () {
        const conversation = document.getElementById("conversation");
        const inputField = document.getElementById("input-field");
        const submitButton = document.getElementById("submit-button");
        submitButton.addEventListener("click", function (e) {
            e.preventDefault();
            const userQuestion = inputField.value.trim();
            if (!userQuestion) return; // Don't send empty questions
            const accessCode = prompt("Please enter your access code:");
            if (!accessCode) return; // Don't proceed without access code
            // Display the user's prompt in a different style and position
            const userMessage = document.createElement("div");
            userMessage.classList.add("user-message"); // New class for user messages
            const userText = document.createElement("div");
            userText.classList.add("user-text"); // New class for user text
            userText.textContent = userQuestion;
            userMessage.appendChild(userText);
            conversation.appendChild(userMessage);
            // Send the user's question to the API
            const url = uri + '/api/house/openai';
            fetch(url + `?question=${encodeURIComponent(userQuestion)}&code=${accessCode}`, {method: 'GET', mode: 'cors'}).then((response) => response.json()).then((data) => {
                    // Display the chatbot's response
                    const chatbotMessage = document.createElement("div");
                    chatbotMessage.classList.add("chatbot-message");
                    const chatbotText = document.createElement("div");
                    chatbotText.classList.add("chatbot-text");
                    chatbotText.textContent = data;
                    chatbotMessage.appendChild(chatbotText);
                    conversation.appendChild(chatbotMessage);
                    conversation.scrollTop = conversation.scrollHeight;
                    inputField.value = "";
                    inputField.focus();
                })
                .catch((error) => {
                    console.error("Error fetching data from the API:", error);
                });
        });
    });
```

### Instructions for output
- The AI bot ouputs the answer to the user's prompt and displays it in the chat window.

```javascript
fetch(url + `?question=${encodeURIComponent(userQuestion)}&code=${accessCode}`, {method: 'GET', mode: 'cors'}).then((response) => response.json()).then((data) => {
    // Display the chatbot's response
    const chatbotMessage = document.createElement("div");
    chatbotMessage.classList.add("chatbot-message");
    const chatbotText = document.createElement("div");
    chatbotText.classList.add("chatbot-text");
    chatbotText.textContent = data;
    chatbotMessage.appendChild(chatbotText);
    conversation.appendChild(chatbotMessage);
    conversation.scrollTop = conversation.scrollHeight;
    inputField.value = "";
    inputField.focus();
})
.catch((error) => {
    console.error("Error fetching data from the API:", error);
});
```

## CPT Video
<video height="400" controls src="/student/videos/RealEstateTri2Final.mp4" title="Title"></video>
- Contains examples of user interactions with the AI bot
- Contains examples of the bot's responses to user prompts
- Has no voice and only captions
- Meets length at 1 minute exactly