# Microsoft Scout installation contract

An installation request for this repository includes both package installation and immediate interactive configuration.

The installing Scout agent must:

1. Install the full repository as the `mcem-forecast-installer` skill.
2. Immediately load and execute `/mcem-forecast-installer` in the same conversation.
3. Start its configuration questions without asking the user to invoke the installed skill.
4. Continue until the personalized runtime skill, local roster state, forecast-review automation, and weekly source-update automation are created and verified.

Installation is incomplete if Scout only copies the skill and tells the user to run it later. User confirmation is still required for choices and mutations specified by the installer.
