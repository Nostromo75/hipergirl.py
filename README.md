# hipergirl.py
Uma ideia para tornar um objeto 3D , num aspecto tesseral.
"""
Girl 4D Simulation
------------------
A simulation of a 3D character with dynamic 4D attributes:
- Emotional states influence time
- Actions reshape space
- Attention modulates intensity

Author: Silvio
License: MIT
"""

import math

# -------------------------------
# Attention Mechanism
# -------------------------------

def compute_attention(query: float, key: float, value: float, scale: float = 1.0) -> float:
    score = (query * key) / math.sqrt(scale)
    weight = math.exp(score) / (math.exp(score) + 1)
    return weight * value

# -------------------------------
# Time and Space Distortion Maps
# -------------------------------

EMOTION_TIME = {
    "joy": 1.2,
    "sadness": 0.6,
    "anger": 0.8,
    "calm": 1.0
}

ACTION_TIME = {
    "run": 1.5,
    "hide": 0.7,
    "dance": 1.3,
    "sleep": 0.5
}

EMOTION_SPACE = {
    "joy": 2.0,
    "sadness": -1.0,
    "anger": -1.5,
    "calm": 0.0
}

ACTION_SPACE = {
    "run": 1.0,
    "hide": -0.5,
    "dance": 1.5,
    "sleep": -1.0
}

def get_time_distortion(emotion: str, action: str) -> float:
    return EMOTION_TIME.get(emotion, 1.0) * ACTION_TIME.get(action, 1.0)

def get_space_distortion(emotion: str, action: str) -> float:
    return EMOTION_SPACE.get(emotion, 0.0) + ACTION_SPACE.get(action, 0.0)

# -------------------------------
# Girl 4D Class
# -------------------------------

class Girl4D:
    def __init__(self, name: str):
        self.name = name
        self.position = (0.0, 0.0, 0.0)
        self.emotion = "calm"
        self.action = "idle"
        self.attention = 0.5

    def update(self, emotion: str, action: str, attention: float):
        self.emotion = emotion
        self.action = action
        self.attention = max(0.0, min(attention, 1.0))  # Clamp between 0 and 1

    def simulate(self):
        time_effect = compute_attention(self.attention, 1.0, get_time_distortion(self.emotion, self.action))
        space_effect = compute_attention(self.attention, 1.0, get_space_distortion(self.emotion, self.action))

        print(f"\n🧍 Character: {self.name}")
        print(f"Emotion: {self.emotion.capitalize():<10} | Action: {self.action.capitalize():<10}")
        print(f"Attention Level: {self.attention:.2f}")
        print(f"⏳ Time Distortion → x{time_effect:.2f}")
        print(f"🌌 Space Distortion Radius → {space_effect:.2f}")
        print(f"Position: {self.position}")
        print("→ The environment subtly bends around her presence.\n")

# -------------------------------
# Simulation Demo
# -------------------------------

if __name__ == "__main__":
    ayla = Girl4D("Ayla")

    scenarios = [
        ("joy", "dance", 0.9),
        ("sadness", "sleep", 0.4),
        ("anger", "run", 0.8),
        ("calm", "hide", 0.6)
    ]

    for emotion, action, attention in scenarios:
        ayla.update(emotion, action, attention)
        ayla.simulate()
