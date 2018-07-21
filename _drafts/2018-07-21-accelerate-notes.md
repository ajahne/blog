---
layout: single
title:  'Accelerate - Chapter Notes: Part 1'
date:   2018-7-21 4:12:29 -0400
categories: leadership books
tags: books, leadership, management
header:
  image: /assets/images/accelerate-chapter-notes.jpg
---
[Leaders are readers](https://www.goodreads.com/quotes/95682-not-all-readers-are-leaders-but-all-leaders-are-readers) and with that in mind, I push myself to read as often as I can.  Currently I am reading ["Accelerate"](https://www.amazon.com/Accelerate-Software-Performing-Technology-Organizations/dp/1942788339) and am taking notes as I go.  Below are my notes, gut reactions, and a few "notes to self" from Part 1.

## Table of Contents:
- [Forward by Martin Fowler](#forward-by-martin-fowler)
- [Forward by Courtney Kissler](#forward-by-courtney-kissler)
- [Chapter 1: Accelerate](#chapter-1-accelerate)
- [Chapter 2: Measuring Performance](#chapter-2-measuring-performance)
- [Chapter 3: Measuring and Changing Culture](#chapter-3-measuring-and-changing-culture)
- [Chapter 4: Technical Practices](#chapter-4-technical-practices)
- [Chapter 5: Architecture](#chapter-5-architecture)
- [Chapter 6: Integrating Infosec into the Delivery Lifecycle](#chapter-6-integrating-infosec-into-the-delivery-lifecycle)
- [Chapter 7: Management Practices for Software](#chapter-7-management-practices-for-software)
- [Chapter 8: Product Development](#chapter-8-product-development)
- [Chapter 9: Making Work Sustainable](#chapter-9-making-work-sustainable)
- [Chapter 10: Employee Satisfaction, Identity, and Engagement](#chapter-10-employee-satisfaction-identity-and-engagement)
- [Chapter 11: Leaders and Managers](#chapter-11-leaders-and-managers)

## Forward by Martin Fowler
- Speed depends on stability
  - Good IT gives you both
- Westrum-generative organizational culture?
- This book focuses on the journey from commit to production, not the entire software development process

## Forward by Courtney Kissler
- Optimize for speed
- Focus on the right things to measure
- Focus the move to outcome based team structures
- Limit blast radius (start with 1 or 2 teams)
- Use data to drive actions
- Doesn’t happen overnight
- Need senior leadership support

## Chapter 1: Accelerate
- Techniques that accelerate technology transformations: CI, CD, lean practices, collaborative culture
- Executives overestimate how much DevOps the org is doing, those doing it do not
- (Assume) potential for growth and enhanced value delivery is greater than executives currently realize
- Focus on capabilities over maturity model
- Follow a continuous improvement paradigm
- Best companies never consider themselves “mature” or “done”
- Teams have their goals, content, way of doing things. What we should focus on depends on those things. Not one size fits all.
- Focus on key outcomes
- Industry is always changing. What is good now, is no longer good enough in a year
- Focus on the right capabilities
- Never settle for yesterday’s accomplishments
- Research showed that none of the following predicted performance: age and technology used for the application, whether operations or development team performed deployments, whether a change approval board is implemented
- Do not trade speed for stability or vice versa

## Chapter 2: Measuring Performance
- Lines of code (LOC), velocity, and utilization are not good measures of productivity and high performance
  - LOC: more lines doesn’t equate to better software, it can lead to bloated code bases, too little means you might create code that’s unreadable (e.g. one liners)
  - Velocity: teams can game the system with story points. Say something is harder than truly is
  - Utilization: if everyone is at 100% no bandwidth to fix bugs, or switch to other tasks that might crop up. Once utilization gets too high there is no bandwidth for changes, unplanned work, improvement work.
- Focus on outcomes not output, focus on a global outcome
- Optimize for: deployment frequency, lead time for changes, Mean Time To Restore (MTTR), change failure rate
- High performing teams continue to get better each year

## Chapter 3: Measuring and Changing Culture
- Organizational culture can exist at three levels in organizations: basic assumptions, values, and artifacts (pg 29)
- Can culture predict software delivery performance? Authors (findings) say yes.
- They found that Westrum Organizational culture predicts software delivery performance and organizational performance
- Companies with safer environments and better communication perform better
- Investigations that stop at “human error” are not just bad, but dangerous. Human error should instead be the start of the investigation
- Goal is to improve information flow, so people have more timely/better information or to find better tools to help prevent catastrophic failures following apparently mundane operations
- You can act your way to a better culture by implementing lean management and continuous delivery
- Culture change: instead of changing people’s mind, first change what they do

## Chapter 4: Technical Practices
- Continuous Delivery: enabler of more frequent, higher quality, and lower-risk software releases
- Agile has management/team and technical practices, need to ensure you are doing all
- Definition of continuous delivery is outstanding (p42-43)
- Build quality in, work in small batches, computers perform repetitive tasks; people solve problems, relentlessly pursue continuous improvement, everyone is responsible
- A key goal of CD is changing the economics of software delivery so the cost of pushing out individual changes is very low
- A key objective for management: Set measurable, achievable, time-bound goals for your outcomes (i.e. the outcomes of CD), help the team work towards them
- _Note to self: change definition of done - done does not mean dev complete, done means all tests are written and code passes all tests (add documentation too?)_
- To implement CD, we need a foundation of:
  - comprehensive configuration management(provision, build, and deploy purely based on what we have in version control),
  - CI (build in small branches, integrate to trunk/master frequently, each change triggers a build process),
  - and continuous testing (inter heal part, test from the beginning)
- Need to implement a deployment pipeline
- Teams that did well with CD, identified more strongly with the org they worked for
- Goal: deploy to production on demand, anyone
- Desired outcome: teams can deploy to production on demand; fast feedback on the quality and deployability is available to everyone in the team
- Investments in technology are also investments in people
- CD makes work more sustainable (less deployment pain, less burnout)
- Keeping system and application configuration in version control is more correlated to software delivery performance than keeping application code in version control
- Have automated tests that are reliable

## Chapter 5: Architecture
- Focus on deployability and testability
- We can do most of our testing without requiring an integrated environment (i.e. staging)
- We can deploy or release our app independent of other services it depends on
- Systems must be loosely coupled: that is, can be changed and validated independently of each other
- Pg 62 has nice breakdown of loosely coupled architecture
- _Note to self: require minimum communication between teams for deployment_
- Whoa this is so true, I’ve read it before, but now I see it: “organizations which designs systems are constrained to produce designs which are copies of the communication structure of the organization"
- Goal: architecture should support the ability of teams to get their work done - from design to deployment - without requiring high-bandwidth communication between teams
- Metric: number of deploys per day per developer (_let’s get this up_)
- Factors that predict high delivery performance:
  - goal-oriented generative culture
  - modular architecture
  - CD
  - effective leadership
- _Explore this_: allow teams to choose their own tools (mostly teams do, but what about standard languages? Ahhh, standardize the language within the team, less about cross-team)
- Architects should focus on engineers and outcomes, not tools and technologies
- Tools and technologies must help people achieve outcomes and enable behaviors we care about

## Chapter 6: Integrating Infosec into the Delivery Lifecycle
- _Note to self: Get developers familiar with OWASP Top 10 and how to prevent them_
- Research shows building security into software development not only improves delivery performance, but also improves security quality
- Have security reviews conducted for all major features - in such a way that doesn’t slow down development process (_how do we do this?_)
- Infosec experts should be part of entire process from the beginning: design, attend and provide feedback on demos, ensure security features are tested as part of the automated test suite
- Infosec needs to provide training, developers have to be aware of security issues
- Be "Rugged"

![The Rugged Movement]({{site.baseurl}}/assets/images/accelerate-the-rugged-movement.jpg){:height="100%" width="100%"}

## Chapter 7: Management Practices for Software
- _Note to self: check out the lean software development book series_
- Lean management: limit Work in progress (what is this?), visual management, feedback from production, lightweight change approvals
- _Note to self: we do have visual displays (Kanban), but no info on quality and productivity, failures or defect rates_
- N2S: look up better visual displays
- Lean management decreases burnout, leads to a more generative culture, and improves software delivery performance
- Limiting WIP (looked it up) is about reducing the current work in progress to focus the team, reduce team overload, reduce context switching, locate bottlenecks faster
- Approval by an external body does not correlate with any increased stability of production systems - it slows things down, shown to be worse than having no change approval process at all
- Recommendation: use lightweight change approval process based on peer review, combined with a deployment pipeline to detect and reject bad changes
- _Note to self: breakdown what needs review and what does not_
- Deployment pipeline is mission critical
- Change acceptance board is risk management theatre

## Chapter 8: Product Development
- Most agile is faux agile
- Lean emphasizes testing product design and business model by performing user feedback frequently
- Take an experimental approach to product development - build and validate prototypes from the beginning, work in small batches, evolve and pivot business models early and often
- Slice products and features into small batches that can be released in a week
- Do teams have a good understanding of the flow of work from business to the customers
- Actively and regularly seek customer feedback
- Do development teams have the authority to create and change specifications as part of development process - make flow of work through the delivery process visible to everyone

## Chapter 9: Making Work Sustainable
- Deployment pain: fear and anxiety related to pushing code to production
- Findings: where code deployments are most painful, you’ll find the poorest software delivery performance, organizational performance, and culture
- Technical practices that improve our ability to deliver software with both speed and stability also reduce the stress and expert associated with pushing to production
- Remove manual steps
- Work to reduce burnout
- Employees have both a duty of care and fiduciary obligation to ensure staff do not get burned out
- Burnout can be prevented, reversed
- Ensure work is meaningful and ensure employees understand how their own work ties to strategic objectives
- Managers often fix the employee while ignoring the environment (_guilty_)
- Foster safe environment that emphasizes learning from failure over blaming; communicate a strong sense of purpose; invest in employee development; ask employees what is preventing them from reaching objectives and fixing those things; give employee time, space, and resources to experiment and learn; employees must have authority to make decisions that affect their work and their jobs, particularly in areas where they are responsible for the outcomes
- Improving technical practices reduce burnout
- Human error is never the root cause of failure in systems
- Five factors most correlated to burnout: organizational culture; deployment pain; effectiveness of leaders; organizational investment in devops; organizational performance
- Team leader: limit work in process, eliminate roadblocks
- Implement weekly experimentation time (_how can we implement this?_)
- Organizational and individual values must align

## Chapter 10: Employee Satisfaction, Identity, and Engagement
- Loyal employees are more engaged and do their best work
- When employees see the connection between the work they do and it’s positive impact on customers, they identify more strongly with the company’s purpose
- eNPS - employee Net Promoter Score
- CD creates a virtuous cycle - investments in technology and prices make the work better for our people, which makes them more motivated, identifying with the organization more, leading to move development - help reduce burnout
- Ensure people have tools and resources to do their job
- Automate menial tasks (performance monitoring, deployment, testing)
- Diversity matters
- Create an inclusive organization; all organizational members feel welcome and valued for who they are and what they bring to the table
- As a leader watch for (and address) harassment, microagressions, and unequal pay

![Chapter 10]({{site.baseurl}}/assets/images/accelerate-chapter-10-page.jpg){:height="100%" width="100%"}

## Chapter 11: Leaders and Managers
- leadership doesn’t mean you have people reporting to you on an organizational chart - leadership is about inspiring and motivating those around you
- 5 characteristics of a transformational leader: vision, inspirational communication, intellectual stimulation, supportive leadership, personal recognition
- Transformative leadership vs servant leadership
- Transformative leadership helps drive high performing teams
- Leaders cannot achieve goals on their own
- Leadership helps build great teams, great technology, and great organizations - indirectly enables teams to rearchitect their systems and implement the necessary continuous delivery (and lean management) practices
- Transformational leadership enables the practices that correlate with high performance
- Invest in DevOps
- Make deployments less painful
- Connect strategic objectives of the business to the work teams do
- Make performance metrics visible and align these with organizational goals
- Delegate more authority to employees
- Knowledge is power and give it (power) to those who have knowledge
- Pg 123 has concrete ways to invest in your team
- Real value of a leader is amplifying the work of their teams
- Enable cross-functional collaboration: build trust with counterparts in other teams, encourage people to move between departments, actively seek and reward work that facilitates collaboration
- Create a climate of learning: budget for books and conferences, make it safe to fail, lunch and learn, share with demo days
- Make effective use of tools: teams should choose their tools, make monitoring a priority
