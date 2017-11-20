++++++++++++++++++++++++++++
Brainstorm: CPython tutorial
++++++++++++++++++++++++++++

Draft: https://cpython-core-tutorial.readthedocs.io/

Summary
=======

* A tutorial made of quest
* A quest is made of missions
* A mission is an exercice which takes 10-15 minutes
* Validating an exercice gives access to a key and to an object
* Inventory: in practice, a list of cute pictures
* Web app to track your progress
* Mentored game where the mentor is the only one allowed to complete (validate)
  a mission
* Themes: student can choose a theme, new themes can be added later

  * Emoji: smiley, keys, congrats, snake, etc
  * RPG: knights, dragon, horse, castle, etc.
  * Theme: list of pictures, one key = one picture, one object = one picture

First Quest: basic setup
========================

* Install Git
* Compile Python
* Run test_os

Second Quest: GitHub and bpo setup
==================================

* Create a GitHub account: "github_account" key
* Create a BPO account: "bpo_account" key
* Link GitHub to BPO: need "github_account" and "bpo_account" keys
* Sign the CLA

Milestones
==========

Milestone 1: open bar
---------------------

* No need to create an account
* Don't track progress
* PoC website with "basic setup" and "GitHub and BPO setup" quests
* DB schema: user
* Add users: user login, contact email, password, optional BPO nick,
  optional GH nick
* Add quests: (quest name)
* Add missions: (quest name, mission name)

Theme
-----

* Theme: (theme name)
* Theme item: (theme name, item name, picture path)

Milestone 2: add inventory, self validation
-------------------------------------------

"You need to complete mission XXX to access to this quest."

"You need to complete mission XXX to access to this mission."

* Add quest_locks: (quest name, needed item) x N
* Add quest_items: (quest name, given item) x N
* Add mission_locks: (quest name, needed item) x N
* Add mission_items: (quest name, given item) x N
* Add user_inventory: (user login, item)

Milestone 3: add mentors
------------------------

* mentors table: (student login, mentor login) x N
* a student cannot validate a step him/herself if he/she has at least one mentor
* a student has to accept to be mentored
* valitate_mission(user login)

Milestone 4: tool
-----------------

* REST API
* user private token/cookie
* (quest name, mission name, user items)
* action: validate a mission

Random notes
============

* Don't:

  * Account time: don't give more credit to developers with more free time.
    We need more diversity.

* The tutorial becomes a game
* 3 types of validation:

  * openbar: full access to all articles
  * student validates its own progress
  * locked: a mentor validates the student's progress

* Locks: allow to import an old game into a new game?
* Non-linear story: lot of quests, splitted into small missions, complete
  a missing to get a key to unlock the next mission
* Design the tutorial to allow to easily extend the tutorial: add new quests,
  split a long missing into smaller missions, even remove missions?
* Non goal: get the highest score and share it online
* Python program for the tutorial:

  * install dependencies
  * help to compile Python
  * validate some steps?

* A mission can just be text to read, for diversity, CoC for example
