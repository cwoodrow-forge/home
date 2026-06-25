---
categories:
  - "[[Learning]]"
subjects:
  - "[[Technology]]"
type: mission
description: "Python mission 3: calculate total army points cost using loops and accumulators."
tags:
  - python
  - coding
created: 2026-06-18
---
Last Updated: `=date(this.file.mtime)`

tags: [python, mission, day03]
status: active
xp_reward: 10

# ⚙️ Mission III — Count the Strength

## 🎯 Objective
Calculate the total points of your army.

---

## 📋 Success Criteria
- Each unit has points
- Total is calculated correctly
- Output is clear

---

## 💡 Hints

<details>
<summary>Hint 1</summary>

You will likely need to loop through your units.

</details>

<details>
<summary>Hint 2</summary>

Consider how to accumulate a running total.

</details>

---

## 🧪 Your Code
~~~python
# Detachment roster – count of each unit type
detachment = {
"Legionary": 10,
"Breacher": 20,
"Assault Marine": 5
}

# Display the detachment roster

print(f"########## FORCES AVAILABLE ##########")

print("\nDetachment Roster:")
for unit_name, count in detachment.items():
	print(f" {unit_name}: {count}")

# Calculate total points for the detachment
total_points = 0
for unit_name, count in detachment.items():
	# Find the unit in legionaries list
	unit_data = next((u for u in legionaries if u["name"] == unit_name), None)
	if unit_data:
		unit_total = count * unit_data["points_cost"]
		total_points += unit_total
		
print(f"Total Detachment Points: {total_points}")
~~~

---

## 🧠 What I Learned
- 

---

## 🚧 Problems Encountered
- 

---

## ✅ Completion Checklist
- [x] Points added to units
- [x] Total correct
- [x] Clean output
- [x] Git commit done

## References

Any references go here. See: Reference note.