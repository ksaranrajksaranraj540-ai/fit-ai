import streamlit as st
from datetime import date

st.set_page_config(
    page_title="Fit AI",
    page_icon="💗",
    layout="wide"
)

# Pink fitness website design
st.markdown("""
<style>
.stApp {
    background-color: #fff5f8;
}
h1, h2, h3 {
    color: #c44578;
}
div.stButton > button {
    background-color: #e879a5;
    color: white;
    border-radius: 12px;
    border: none;
    padding: 10px 20px;
}
</style>
""", unsafe_allow_html=True)

st.title("💗 Fit AI")
st.subheader("Your Simple Fitness Assistant")
st.write("Build healthy habits, one day at a time! 🌸")

st.divider()

# User details
st.header("👤 Your Details")

col1, col2, col3 = st.columns(3)

with col1:
    name = st.text_input("Your name", "Friend")
    age = st.number_input(
        "Age", min_value=13, max_value=100, value=18
    )

with col2:
    height = st.number_input(
        "Height (cm)", min_value=100.0,
        max_value=230.0, value=160.0
    )
    weight = st.number_input(
        "Weight (kg)", min_value=20.0,
        max_value=250.0, value=55.0
    )

with col3:
    activity = st.selectbox(
        "Activity level",
        ["Beginner", "Light activity", "Regular activity"]
    )
    goal = st.selectbox(
        "Your goal",
        ["Stay active", "Build strength",
         "Improve flexibility", "Build healthy habits"]
    )

# Workout suggestions
st.divider()
st.header("🏃 Your Workout Plan")

workouts = {
    "Beginner": [
        "5 minutes gentle warm-up",
        "10 minutes comfortable walking",
        "5 minutes gentle stretching"
    ],
    "Light activity": [
        "5 minutes warm-up",
        "10–15 minutes brisk walking",
        "5 minutes stretching"
    ],
    "Regular activity": [
        "5 minutes warm-up",
        "15 minutes walking or cycling",
        "5 minutes stretching"
    ]
}

st.write("Suggested activities for", name or "you")

for workout in workouts[activity]:
    st.write("☐", workout)

st.caption(
    "Choose a comfortable level and rest when needed. "
    "These are general suggestions, not medical advice."
)

# Food suggestions
st.divider()
st.header("🥗 Balanced Food Ideas")

meal_col1, meal_col2, meal_col3 = st.columns(3)

with meal_col1:
    st.subheader("🌅 Breakfast")
    st.write("Idli + sambar")
    st.write("Dosa + egg")

with meal_col2:
    st.subheader("☀️ Lunch")
    st.write("Rice + vegetables")
    st.write("Dal or egg with curd")

with meal_col3:
    st.subheader("🌙 Dinner")
    st.write("Chapati + vegetables")
    st.write("Idli + sambar")

st.info(
    "These are example meal ideas. Choose portions and foods "
    "that suit your appetite, preferences and dietary needs."
)

# Water tracker
st.divider()
st.header("💧 Water Tracker")

if "water" not in st.session_state:
    st.session_state.water = 0

if "water_date" not in st.session_state:
    st.session_state.water_date = str(date.today())

if st.session_state.water_date != str(date.today()):
    st.session_state.water = 0
    st.session_state.water_date = str(date.today())

st.write("Record each glass of water you drink.")

water_col1, water_col2 = st.columns(2)

with water_col1:
    if st.button("➕ Add one glass"):
        st.session_state.water += 1

with water_col2:
    if st.button("🔄 Reset today's count"):
        st.session_state.water = 0

st.metric("Glasses recorded today", st.session_state.water)
st.caption(
    "Drink according to thirst, weather and activity. "
    "Water needs differ from person to person."
)

# Daily habits
st.divider()
st.header("✨ Daily Healthy Habits")

habit1 = st.checkbox("I did some movement today")
habit2 = st.checkbox("I ate balanced meals")
habit3 = st.checkbox("I drank water regularly")
habit4 = st.checkbox("I took time to rest")

completed = sum([habit1, habit2, habit3, habit4])

st.progress(completed / 4)
st.write(f"Habits completed: {completed}/4")

# Fitness summary
st.divider()
st.header("📊 Your Summary")

st.write("**Name:**", name or "Friend")
st.write("**Age:**", age)
st.write("**Activity:**", activity)
st.write("**Goal:**", goal)

if st.button("Generate my fitness summary"):
    st.success(f"Great, {name or 'Friend'}! Your plan is ready.")

    st.write("### Your next steps")
    st.write("- Pick a comfortable activity.")
    st.write("- Enjoy balanced, regular meals.")
    st.write("- Drink water throughout the day.")
    st.write("- Rest and adjust activities to your needs.")

st.caption(
    "Fit AI is a beginner educational project. "
    "It does not diagnose health conditions or provide "
    "personalised medical or nutritional advice."
)

st.markdown("---")
st.write("Made with 💗 using Python and Streamlit")
