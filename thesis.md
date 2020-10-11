---
layout: default
use_math: true
---
# Master Thesis

## Where?
The [Computing Systems Lab](https://www.ugent.be/ea/elis/en/csl) @ UGent.
There's a lot of cool things happening in this research group,
among others a team that works on Computer Security.
I did my thesis in the context of the research of this team.

## What?
Creating a 'just-in-time return oriented programming' (JIT-ROP) attack against a Multi-Variant Execution Environment (MVEE).
This in order to test if the MVEE developed at the research group can withstand this type of attack.

## Some background
To give a quick idea of what this thesis was about.

Return Oriented Programming (ROP):
- One defense mechanism that has become widespread is called 'W $\oplus$ X':
  it disallows pages with both write and execute permission.
- This prevents executing code that injected (by e.g., a buffer overflow).
- But the attacker is inventive: they started using existing code for their nefarious purposes!
- Find sequences of instructions in the executable that are of the following structure:
  ```
  useful instruction(s);
  ret;
  ```
- Construct a ROP chain (a sequence of these code pieces) that achieves your goals.
- Then use a vulnerability to put the addresses in your ROP chain at the correct location
  (the first one overwriting an actual return address) on the stack (writable but not executable).
- These pieces of code will then execute after eachother, and by-pass the protection of W $\oplus$ X.

Multi-Variant Exection environment (MVEE):
- A defense method where a program is run multiple times, where each of these 'variants' has been diversified.
- There is a monitor that compares the variants by synchronizing them at certain points.
- The variants should diverge on an illegal action (when an attack is happening).
- The monitor can then detect this, stop execution and prevent the attacker from succeeding.
- By randomizing the address space layout of the variants, this method can defeat ROP attacks.

The security group where I did my thesis has developed such a MVEE, named GHUMVEE (Ghent University MVEE).
My goal was to find out if the MVEE was capable of handling a new class of attacks: JIT-ROP.

Just-in-time Return Oriented Programming (JIT-ROP):
- A ROP attack that builds the ROP chain 'just-in-time': the location of the reused code is determined at runtime.
- This is possible when attacking scripting environments that have some vulnerabilities that you can exploit:
  + leaking pointers
  + reading memory
  + placing the ROP chain in memory

This was very interesting research, since there was a clear goal and lots to learn.
As it turns out, JIT-ROP attacks could remain undetected by GHUMVEE,
proving again that no security mechanism is perfect.
