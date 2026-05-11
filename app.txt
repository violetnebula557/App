import streamlit as st

# Recommendations data
recommendations = {
    "confused": {
        "mood": "Confused & want twists",
        "psychological": {"book": "Gone Girl", "series": "Sharp Objects", "story": "Wife disappears, husband suspect"},
        "murderMystery": {"book": "Evelyn Hardcastle", "series": "Poker Face", "story": "Same day repeats 8 times"}
    },
    "slow": {
        "mood": "Slow burn & creepy",
        "psychological": {"book": "The Silent Patient", "series": "Hill House", "story": "Painter kills husband, stops speaking"},
        "murderMystery": {"book": "Thursday Murder Club", "series": "Only Murders", "story": "Retirees solve cold cases"}
    },
    "fast": {
        "mood": "Fast & bloody",
        "psychological": {"book": "Intensity", "series": "You", "story": "Killer invites himself into someone's life"},
        "murderMystery": {"book": "Good Girl's Guide", "series": "Mare of Easttown", "story": "Student reopens murder case"}
    }
}

# App title
st.title("🎭 Thrill or Kill?")
st.caption("Pick your mood → Get your next obsession")

# Mood buttons in 3 columns
col1, col2, col3 = st.columns(3)

with col1:
    if st.button("🧩 Confused & want twists", use_container_width=True):
        st.session_state.mood = "confused"

with col2:
    if st.button("🐢 Slow burn & creepy", use_container_width=True):
        st.session_state.mood = "slow"

with col3:
    if st.button("⚡ Fast & bloody", use_container_width=True):
        st.session_state.mood = "fast"

# Genre selection
genre = st.radio(
    "Choose your genre:",
    ["🧠 Psychological Thriller", "🔪 Murder Mystery"],
    horizontal=True
)

# Convert to data key
genre_key = "psychological" if "Psychological" in genre else "murderMystery"

# Show recommendations if mood is selected
if "mood" in st.session_state and st.session_state.mood:
    mood_data = recommendations[st.session_state.mood]
    
    st.divider()
    st.subheader(f"🎯 For your mood: {mood_data['mood']}")
    
    with st.container(border=True):
        st.markdown(f"**📚 Book:** {mood_data[genre_key]['book']}")
        st.markdown(f"**📺 Series:** {mood_data[genre_key]['series']}")
        st.markdown(f"**📖 Story:** {mood_data[genre_key]['story']}")
    
    if st.button("🗑️ Clear & start over"):
        del st.session_state.mood
        st.rerun()
else:
    st.info("👆 Click a mood button above to get recommendations")