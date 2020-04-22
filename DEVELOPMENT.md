# Steering

Parties and responsibilities
#### Working Party
Open group consisting of representatives from service providers, communication operators, citynets and system providers. Group responsibilities are
  * Writing requirements for functionality according to the needs of the entire line of business
  * Clarifying the needs of the company that one represents
      
      
#### Technical Working Party
Open group consisting of representatives from service providers, communication operators, citynets and system providers. Group responsibilities are, based on requirements from Working Party as well as approved functionality by Steering Group,
  * Continuous technical maintenance of workspaces (Github repositories and specifications, Slack etc.)
  
#### Steering Group
Selected group consisting of representatives from Tjänsteleverantörsföreningen and Svenska Stadsnätsföreningen. Group responsibilities are 
  * Management of projects and specfications driven by the Swedish telecommunication companies (API, address, invoice)
  * Approval and prioritizing requirements
  * Ensure that the working group has the tools needed for their work (licenses, software etc.)

# Processes

#### New API functionality
1. Create issue and describe the suggested functionality, it's purpose and which version request applies to
      1) Type: Enhancement
      2) Priority: Low, Medium, High, Critical
      3) Status: Available
2. Working Party will complete suggestion or require completion from creator
      1) Status: On Hold
3. Vote to accept suggestion (5 thumbs up from company representatives to escalate suggestion to Steering Group)
      1) Status: Review Needed
4. Steering Group decides on suggestion
      1) Milestone: version (if approved)
      2) Status: Denied (if denied) and close issue
      3) Priority: Low, Medium, High, Critical
5. Technical Working Party manages issues approved by Steering Group and assigns to a person
      1) Assignee: Name
      2) Status: In Progress
6. Pull request is created
7. Technical Working Party completes pull request or requires completion from creator
      1) Status: On Hold
8. Technical Working Party publishes changes
      1) Status: Completed and close issue

#### Maintenance of existing API functionality
1. Create issue and describe the suggested functionality, it's purpose and which version request applies
      1) Status: Available
      2) Type: Bugfix, Maintenance
      3) Priority: Low, Medium, High, Critical
2. Working Party completes suggestion or requires completion from creator
      1) Status: On Hold
3. Vote to accept suggestion (5 thumbs up from company representatives to approve) 
      1) Milestone: version
      
Mere bugfixes don't need votes, may be escalated directly to Technical Working Party

#### Other
1. Create issue and describe the suggested functionality, it's purpose and intended recipient
      1) Status: Available
      2) Request type: Question, 
      3) Priority: Low, Medium, High, Critical
2. Working Party completes suggestion or requires completion from creator
      1) Status: On Hold
3. Depending on the nature of the issue, the steps to follow will either be to approve by Working Group or Steering Group
      1) Status: Review Needed
