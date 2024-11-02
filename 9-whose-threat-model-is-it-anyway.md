# Whose Threat Model is it Anyway!?

Presented by Travis Friesen - Senior Infrastructure Developer at Neo Financial

## Threat Modelling

- Threat Model is what you use to do Threat Modelling
- Think of it like initial parameters for a model of the solar system
- TL;DR Brainstorming
    - Focused and structured brainstorming
    - Finding ways to improve the security of a system by 'modelling potential threats'
- Why do Threat Modelling?
    - Make your systems more secure
    - Find vulnerabilities and bugs (ideally earlier)
    - Focused approach to security
- What is a Threat Model?
    - High-leel diagram of the system we're trying to secure
    - Threat Actors and their motivations
    - Potential goals, resources, 'crown jewel' that a threat actor might be interested in (money, data, CPU time)
- Importance of a good Threat Model
    - Focus on relevant threats
    - Sometimes less important about what's in Threat Model than what isn't
    - All controls have a cost
- Threat Actors: Example categories in order of fuckedness
    - Government Agencies (CIAs, NSAs, KGB, etc)
    - Big-time criminals
    - Hacktivists, competitors
    - Small-time criminals, insiders
    - Script kiddies
- What's not in my Threat Model?
    - The NSA (you aren't that interesting)
    - Your cloud provider

## A Case Study: My Garage Door

- "After learning to pick locks for the first time, I immediately went home and purchased new locks for my front door."
- Locks are for keeping honest people out
- Both of these sentiments demonstrate a failure of threat modelling

- Had a few incidents where people got into the garage and took things
- Upgraded security, but with outside hinges and outer master lock
- Not worried, because criminals are dumb and lazy
- Learning lock picking is a skill that most petty criminals are not investing in (with an asterisk)
- No correlation between people willing to learn to pick locks and people interested in the contents of my garage
- Threat model
    - People in it: People with bolt-cutters
    - People not in it: People who know how to pick locks
- More secure for less money by applying threat modelling

## How to do Threat Modelling

- Step 1: Build your Threat Model
    - Describe system and components at high level
    - Determine threat actors and motivation (What is valuable to them?)
- Step 2: Do the threat modelling
- Tip? Think like an attacker!
    - How could an attacker abuse this system?
    - Easier said than done:
        - Most people don't know how to think like an attacker
        - Requires special skills
- S.T.R.I.D.E.
    - Spoofing
        - What if attacker sends data from fake IP?
    - Tampering
        - Replay messages
        - Modifying cookies or request URLs
    - Repudiation
    - Information Disclosure
        - Revealing error messages, introspection
    - Denial of Service
    - Elevation of Privilege
- Similarly
    - OWASP Top 10
    - MITRE ATT&CK
- Attack trees
    - Root node: Ultimate goal at the top
    - List all the ways they can get to that
- Step 3: Actually fix the bugs and vulnerabilities you find


## Q&A

- Permission to have pictures from Home Alone?
    - I'll let you guess
- What about the window?
    - Have other things for that, have to look at the whole system
- What about driving through your garage?
    - Not in my threat model?
- What's the most valuable thing in your garage?
    - Can't answer
- How to prioritize and order threat actors?
    - Risk analysis: likelihood and impact. One of the earlier times garage was broken into was someone with a shovel, they grabbed a broken fan and left with a lovely shovel
