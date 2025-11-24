import streamlit as st
import pandas as pd
import random

st.set_page_config(page_title="Color Trading Predictor", layout="centered")

# ---------- PASSWORD SYSTEM ----------
admin_pass = st.sidebar.text_input("Enter Admin Password", type="password")
correct_pass = "20052026"

if admin_pass != correct_pass:
    st.error("❌ Wrong Password — Logging disabled")
    st.stop()
else:
    st.success("✔ Correct Password — Full access enabled")

# ---------- PLAYER ID ----------
user_id = st.sidebar.text_input("Player ID")

st.title("🎨 Color Trading Predictor")
st.write("AI-based color prediction with Big / Small analysis.")

# ---------- MAIN PREDICTION ----------
if st.button("Predict"):
    
    # Create random probability
    percent = [
        random.uniform(10, 60),
        random.uniform(10, 60),
        random.uniform(10, 60)
    ]

    total = sum(percent)
    percent = [round(p / total * 100, 2) for p in percent]

    colors = ["🟢 GREEN", "🔴 RED", "🟡 YELLOW"]
    result = colors[percent.index(max(percent))]

    st.subheader("📊 Prediction Result:")
    st.write(f"**Highest Probability:** {result}")

    df = pd.DataFrame({
        "Color": colors,
        "Probability %": percent
    })

    st.dataframe(df)

