# Inheritance

- [Follow on Bluesky](https://bsky.app/profile/leonlonsdale.dev)
- [Join Discord](https://discord.gg/dhrdFh98UA)

- Classes can inherit the attributes and methods of other classes.
- This is useful because it allows us to create a new class that is a modified version of an existing class.
- The original class is called the parent class, and the new class is called the child class.
- Inheritance is particularly useful in keeping code DRY (Don't Repeat Yourself) and in the organisation of code - when we have a need to create multiple classes that share some common attributes and methods, it is better to create a parent class that contains these common attributes and methods, and then create child classes that inherit from them.

For example:

```python

class Human:
	def __init__(self, name, date_of_birth):
		self.name = name
		self.dob = date_of_birth

	def walk():
		# walk

	def talk():
		# talk
```

- This would be a parent class as humans, have names and a date of birth, and can walk and talk.

```python
class MedicalPractitioner(Human):
	def __init__(self, name, date_of_birth):
		super().__init__(name, date_of_birth qualifications)
		self.qualifications = qualifications

	def assess_patient():
		# assess patient
```

- This would be a child class. It `inherits` the name and date of birth attributes, and the walk() and talk() methods from the Human class.
- But we can go further.

```python
class Doctor(MedicalPractitioner):
	def __init__(self, name, date_of_birth, qualifications):
		super().__init__(name, date_of_birth, qualifications)


	def prescribe_medicine():
		# prescribe medicine

class Surgeon(Doctor):
	def __init__(self, name, date_of_birth, qualifications):
		super().__init__(name, date_of_birth, qualifications)

	def operate():
		# perform surgery

class Nurse(MedicalPractitioner):
	def __init__(self, name, date_of_birth, qualifications):
		super().__init__(name, date_of_birth, qualifications)

	def treat_wounds():
		# treat
```
