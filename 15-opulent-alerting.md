# Opulent Alerting: Enriching our Lives

Presented by Paul Harrison - Security Operations at Mattermost

## Detection & Response, A Recap

- Indicator
- Detection
- Response
- Mitigation

- In reality
    - Indicator
    - Detection
    - Ack
    - Triage
    - Response
    - Mitigation

- In reality...it's a little more involved
    - Indicator
    - Detection (Hopefully)
    - Ack (Hopefully)
    - Triage (Hopefully)
    - Response (Hopefully)
    - Mitigation (Hopefully)

- Why?
    - Event isn't written to logs, log is too ambiguous
    - Rule quality, missing rule, log source not integrated
    - Missed the page, alert destination broken,...
    - Something was stopped...you think

## Detection Theory

- Detection is piecing together *indicators* to determine something has happened.
- A single event, by itself, may not represent anything
- Multiple single events, over time, may be far more nefarious
    - Example: 4 failed login attempts over 15 minutes then a successful login
- What is "Detection"? Trying to spot a needle or three('ish) in a stack of needles that:
    - Vary in value for various subjective reasons
    - The quality depend on dev's (largely) not sure how or why they write to log anyways
    - May be produced by well funded bad actors actively attempting to avoid detection

## Meaningful Alerting

- What's the point?
    1. Tell you an event was detected
    2. A summary of the finding
    3. Makes record of it
- What are we really trying to accomplish?
    1. Catch bad things
    2. React quickly
    3. Mitigating problems before they blow up (even worse)
- While not getting inundated by false positives and meaningless noise or alerts with so little information you have no idea what's going on

## Enrichment

Imagine this:
- AWS, a production account
- SOP changes are using pull requests; GitHub Actions + Terraform
- Emergency / break-glass acess via local IAM user + MFA
It's 3:00am, you get paged because walbolbob made a change to an S3 bucket's policy in bloblaw-blog-prod. The bucket: bloblaw-blog-blob

Triage:
- Is this actually Bob's IP?
- What's he doing up at 3am?
- Is his device online?
- Why's he using that emergency account?
- What has that IP been up to?

Time's ticking!

- Mean-time-to-Mitigate (MTTM)
    - Detection -> Ack
        - Accuracy of detection rules
        - Effectiveness of determining initial severity
        - If/when to page on clal
    - Ack -> Response
        - Verbose, meaningful data
        - Easy to read and comprehend
        - Anticipating the first steps of response
        - Answer before Asked
    - Response -> Mitigation
        - Common mitigation best practices
        - Understanding what data is required to decide direction
        - Easy access to runbooks and tooling

- How would this work? Our tools:
    - [Panther Labs](https://panther.com/)
    - [Tines](https://tines.com/)
    - [Mattermost](https://mattermost.com/)
- Panther Labs: Detection as code
    - Detection rule/instruction
    - Customizable event output
    - Baseline severity
- Tines:
    - "Story" driven
    - Drag-and-drop automation
    - Infinitely customizable
    - _Very addictive_
    - Steps:
        - Panther Intake
        - Enrichment
        - Delivery
        - Gravy
    - Assemble Context
        - What severity should this be?
        - Should we page?
        - Should we even alert?
        - Bolt-on scoring mechanisms
        - Exception rules
        - IOC lists

## Q&A

- How much effort should I enrich current alerts versus making new alerts?
    - Both, hard to enrich something you don't know exist, if you're trying to alert everything on AWS you're wasting your time. If you know what you're looking for you should be looking to enrich it
- What constitutes as risk when this involves lots of infrastructure change?
    - Security risk is business risk. Representing it as a risk to the business to the finance people is how I convince people
- Does a no-code platform like Tines have enough flexibility?
    - Yes. Have tried in shell scripting and Python, Tines is tremendously flexible and have never ran into issues
