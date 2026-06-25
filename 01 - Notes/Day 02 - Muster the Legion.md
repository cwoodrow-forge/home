---
categories:
  - "[[Learning]]"
subjects:
  - "[[Technology]]"
type: mission
description: "Python mission 2: represent multiple units using lists and nested dictionaries. Completed."
tags:
  - python
  - coding
created: 2026-06-18
---
Last Updated: `=date(this.file.mtime)`
## Day 2 - Muster the Legion

---
tags: [python, mission, day02]
status: active
xp_reward: 10
---

# ⚙️ Mission II — Muster the Legion

## 🎯 Objective
Represent multiple units in your program.

Each unit must include:
- Name
- At least one additional attribute

---

## 📋 Success Criteria
- Multiple units stored
- Easy to add new units
- Data prints clearly

---

## 💡 Hints

<details>
<summary>Hint 1</summary>

Consider which Python data structure best represents a collection of objects.

</details>

<details>
<summary>Hint 2</summary>

Each unit should probably be a structured object rather than just text.

</details>

---

## 🧪 Your Code
~~~python
# Define a list of legionary units with their attributes

legionaries = [
{ # First legionary unit as a dictionary
"name": "Legionary",
"faction": "Legiones Astartes",
"profile": {"M": 7, "WS": 4, "BS": 4, "S": 4, "T": 4, "W": 1, "I": 4, "A": 1, "Ld": 7, "Sv": "3+"},
"keywords": ["Infantry", "Legion", "Line"],
"wargear": ["Boltgun", "Bolt pistol", "Frag grenades", "Krak grenades", "Power armour"],
},
{ # Second legionary unit as a dictionary
"name": "Breacher",
"faction": "Legiones Astartes",
"profile": {"M": 7, "WS": 4, "BS": 4, "S": 4, "T": 4, "W": 1, "I": 4, "A": 1, "Ld": 7, "Sv": "3+"},
"keywords": ["Infantry", "Legion", "Line"],
"wargear": ["Boltgun", "Boarding Shield", "Power armour"],
},
{ # Third legionary unit as a dictionary
"name": "Assault Marine",
"faction": "Legiones Astartes",
"profile": {"M": 7, "WS": 4, "BS": 4, "S": 4, "T": 4, "W": 1, "I": 4, "A": 1, "Ld": 7, "Sv": "3+"},
"keywords": ["Infantry", "Legion", "Denial"],
"wargear": ["Boltgun", "Bolt pistol", "Frag grenades", "Krak grenades", "Power armour"],
}
] 

for legionary in legionaries:
print(f"Unit Name: {legionary['name']}")
print(f"Faction: {legionary['faction']}")
print("Profile:")
for stat, value in legionary["profile"].items():
print(f" {stat}: {value}")
print("Keywords: " + ", ".join(legionary["keywords"]))
print("Wargear: " + ", ".join(legionary["wargear"]))~~~

---

## 🧠 What I Learned
- dict allows for key-value pairs { } 
- A Dictionary item can also be a list [ ] a tuple ( ) or even another dictionary { }
- The solution was a list containing multiple iterations of dictionary, and each dictionary also contained lists and other dicts. 
- Can nest 'for' iterations within outer for loops. Example: making wargear a dictionary key-value pairs and looping through the values.

#### Enhancement
```python
legionaries = [

{ # First legionary unit as a dictionary
"name": "Legionary",
"faction": "Legiones Astartes",
"profile": {"M": 7, "WS": 4, "BS": 4, "S": 4, "T": 4, "W": 1, "I": 4, "A": 1, "Ld": 7, "Sv": "3+"},
"keywords": ["Infantry", "Legion", "Line"],
"wargear": {"Primary": "Boltgun", "Side": "Bolt Pistol", "Grenade": ["Frag", "Krak"], "Armour": "Artificer"},
},

for legionary in legionaries:
	print(f"Unit Name: {legionary['name']}")
	print(f"Faction: {legionary['faction']}")
	print("Profile:")
	for stat, value in legionary["profile"].items():
print(f" {stat}: {value}")
print("Keywords: " + ", ".join(legionary["keywords"]))
print("Wargear: ")
for category, items in legionary["wargear"].items():
	if isinstance(items, list):
		print(f" {category}: {', '.join(items)}")
	else:
		print(f" {category}: {items}")
```

---

## 🚧 Problems Encountered
- 

---

## ✅ Completion Checklist
- [x] Multiple units stored
- [x] Attributes included
- [ ] Output readable
- [x] Git commit complete

## References

Any references go here. See: Reference note.