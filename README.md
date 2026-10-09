# DevOps Engineering Assignment

## Part A: Theoretical Questions

### Q1. What is DevOps Engineering, and how does it differ from traditional development and operations roles?

DevOps Engineering is the practice of uniting software development (Dev) and IT operations (Ops) so that software is built, tested, released and run as one continuous, automated process. A DevOps Engineer builds the pipelines, infrastructure and monitoring that let teams ship changes quickly and reliably.

| Aspect | Traditional Developer / Ops | DevOps Engineer |
| --- | --- | --- |
| Focus | Developers write features; Ops keeps servers running | Owns the full path from code to production |
| Handoff | Code is thrown "over the wall" to Ops | Shared ownership, no wall |
| Releases | Manual, infrequent, high risk | Automated (CI/CD), frequent, low risk |
| Infrastructure | Set up by hand | Defined as code (Terraform, Ansible) |
| Failures | Blame between teams | Shared responsibility, blameless reviews |
| Feedback | Slow, after release | Fast, through monitoring and automated tests |

### Q2. How does DevOps fit into the SDLC? (three or more phases)

DevOps spans the whole SDLC instead of sitting only at the end. It adds value in these phases:

- **Planning:** Work is tracked in shared boards (Jira, GitHub Projects), and operations concerns such as scalability and monitoring are raised early.
- **Coding:** Git workflows, pull requests and code review keep the main branch healthy and every change traceable.
- **Build and Test:** CI tools (GitHub Actions, Jenkins) compile the code and run unit, integration and security tests on every commit, so bugs are caught within minutes.
- **Release and Deploy:** CD pipelines and strategies such as blue-green or canary releases make deployments repeatable and easy to roll back.
- **Operate and Monitor:** Metrics, logs and alerts (Prometheus, Grafana, ELK) feed real production data back into the next planning cycle, closing the loop.

### Q3. What values does a DevOps Engineer bring to an organization? (four values)

1. **Faster delivery.** Automated pipelines turn a release that took days of manual work into one that takes minutes. Example: a team moves from monthly releases to several deployments per day.
2. **Reliability and stability.** Automated tests, health checks and monitoring catch problems before users do. Example: an alert on rising error rates triggers an automatic rollback of a bad release.
3. **Cost efficiency.** Auto-scaling, right-sized cloud resources and automation of repetitive work reduce waste. Example: non-production environments shut down at night, cutting the cloud bill.
4. **Collaboration and culture.** DevOps Engineers connect developers, testers, security and operations around shared goals. Example: a shared incident channel and runbooks mean everyone knows who does what during an outage.

### Q4. Why is prior Software Engineering (SWE) experience helpful before becoming a DevOps Engineer?

- **Understanding the product:** Someone who has written and shipped code knows how applications are structured, configured and where they usually break.
- **Scripting and automation:** DevOps work is largely code (Bash, Python, YAML, Terraform), so programming fluency is used daily.
- **Version control and testing habits:** Git, branching, code review and test design are the foundation of CI/CD.
- **Empathy for developers:** Knowing the developer's pain points leads to pipelines and tools that people actually want to use.
- **Faster debugging:** Reading stack traces and logs and tracing a bug through code is a skill built in SWE roles.

### Q5. Why is networking knowledge (DNS, ports, protocols, IP addressing) important for DevOps?

Every deployed system communicates over a network, so most outages have a networking component.

- **DNS:** Maps names like `example.com` to IP addresses. A wrong or stale record makes a healthy site unreachable.
- **Ports:** Services listen on specific ports (80/443 for web, 22 for SSH, 5432 for PostgreSQL). Firewalls and security groups must allow the right ones, and only those.
- **Protocols:** Knowing HTTP/HTTPS, TCP, UDP and TLS helps with load balancers, certificates and diagnosing slow or failing connections.
- **IP addressing and subnets:** Needed to design VPCs, private and public subnets, and to configure routing and access rules.

Tools such as `ping`, `dig`, `curl`, `netstat` and `traceroute` are used constantly to find where a request is failing.

### Q6. What soft skills are essential for a DevOps Engineer, and how do they help during incidents?

- **Communication:** Clear, calm status updates keep the team and stakeholders informed so no one duplicates work or guesses.
- **Collaboration:** Incidents cross team boundaries; working well with developers, QA and support gets the right people on the problem quickly.
- **Calm under pressure:** A steady engineer follows a process instead of making panicked changes that worsen the outage.
- **Ownership and accountability:** Taking responsibility for the fix and for the follow-up prevents repeat failures.
- **Documentation and learning:** Writing runbooks and blameless post-mortems turns each failure into lasting improvement.

### Q7. Why are patience and a troubleshooting mindset important in DevOps? (real-life example)

Problems in distributed systems are rarely obvious, and the first guess is often wrong. Patience means testing one hypothesis at a time, reading logs carefully and not skipping steps. A troubleshooting mindset means working from evidence: what changed, what is the symptom, and where does it start?

**Example:** After a new release, users report that the website is slow. A rushed engineer restarts servers repeatedly with no effect. A patient engineer checks monitoring, sees that only requests touching the database are slow, finds that the release added a query with no index, and fixes it by adding the index. The cause was found by methodically narrowing down the problem, not by guessing.

---

## Part B: Scenario-Based Questions

### Scenario 1. Onboarding a student who is new to GitHub and cloud platforms

1. **Welcome and orientation (Day 1).** Share the course roadmap, a one-page "start here" guide and the communication rules (which channel is for what, expected response times). Add them to Slack/Discord/WhatsApp and the course calendar.
2. **GitHub basics.** Have them create an account, set up SSH keys or a token, and complete a guided exercise: fork a practice repository, clone it, create a branch, commit, push and open a pull request. Provide a short Git cheat sheet (`clone`, `add`, `commit`, `push`, `pull`, `branch`).
3. **Cloud basics.** Create a free-tier account (AWS, Azure or GCP) with a billing alert set up first. Walk through the console, launch one small virtual machine, connect via SSH, then shut it down.
4. **Documentation.** Point them to the course README, wiki and official docs, and a short FAQ. Record screen-share walkthroughs they can replay.
5. **Pair with a buddy.** Assign a mentor or peer for questions, and hold a weekly 15-minute check-in.
6. **Small wins.** Give a first task such as fixing a typo in the docs via pull request, so they practice the real workflow with low risk.
7. **Feedback loop.** Ask what was confusing and update the onboarding guide for the next student.

### Scenario 2. Production application goes down during a deployment

1. **Acknowledge and communicate.** Declare an incident, post in the incident channel, and assign roles (incident lead, communicator, investigator). Tell stakeholders an investigation is underway.
2. **Assess impact.** Check monitoring dashboards and alerts: which services, users and regions are affected, and since when?
3. **Check what changed.** The outage started during a deployment, so the release is the prime suspect. Review the deploy log, the commit list and any config or infrastructure changes.
4. **Restore service first.** If the new release is the likely cause, roll back to the last known good version (or switch traffic back in a blue-green setup). Restoring users takes priority over finding the root cause.
5. **Investigate.** Read application and server logs, check resource use (CPU, memory, disk), health checks, database connectivity, DNS, certificates and network rules. Test one hypothesis at a time.
6. **Verify recovery.** Confirm that error rates, latency and health checks return to normal, and run a smoke test of key user flows.
7. **Communicate resolution.** Post a clear update to the team and stakeholders.
8. **Post-incident review.** Hold a blameless post-mortem: timeline, root cause, what worked, what didn't. Create action items such as more tests, a canary stage, better alerts and an updated runbook.

### Scenario 3. Frequent releases but decreasing stability

Speed and stability are not opposites. DevOps balances them by making each change smaller, safer and easier to undo.

- **Stronger CI:** Run automated unit, integration and security tests on every commit, and block merges when tests fail.
- **Progressive delivery:** Use canary releases, blue-green deployments and feature flags to expose changes to a small group first and switch them off instantly if needed.
- **Quality gates in CD:** Require passing tests, code review and staging validation before production.
- **Observability:** Add monitoring, logging, tracing and alerts on key signals (error rate, latency, saturation) so issues are seen within minutes.
- **Service level objectives (SLOs) and error budgets:** Define how much unreliability is acceptable. When the error budget is used up, pause feature work and focus on stability.
- **Fast rollback:** Make every release reversible with a single command.
- **Small batch sizes:** Smaller changes are easier to review, test and diagnose.
- **Blameless post-mortems:** Learn from each failure and turn the lessons into automation.

### Scenario 4. Communication problems during incidents in a distributed team

Proper onboarding to communication platforms means every member knows the tools, channels and expectations before an incident happens.

- **One agreed place for incidents:** A dedicated channel (for example #incidents) plus a video bridge means no time is lost deciding where to talk.
- **Defined roles and escalation:** Everyone knows who the incident lead is and who to page next, through an on-call tool such as PagerDuty or Opsgenie.
- **Alerts to the right people:** Integrating monitoring alerts into chat gets the whole team the same information at the same moment.
- **Shared documentation:** Runbooks, architecture diagrams and contact lists are stored in one wiki that new members are shown how to find.
- **Time-zone handoffs:** Clear handoff notes and a follow-the-sun rota keep long incidents moving across regions.
- **Practice:** Run game days and mock incidents so the tools and process feel familiar under stress.
- **Written record:** A running timeline in the channel makes the post-mortem accurate and easy.

The result is faster detection, less confusion, shorter recovery time (MTTR) and less stress on the team.

---

## Part C: Technical / Practical Tasks

### Task 1. Local DevOps demo application

The app is a simple static page (`index.html` in this repository) served with Python's built-in web server.

```bash
python3 -m http.server 8000
```

Verify it is running:

```bash
curl -I http://localhost:8000
```

**Screenshot 1: server running in the terminal**

![Terminal showing the local server running](screenshots/01-server-running.png)

**Screenshot 2: app open in the browser at localhost:8000**

![Browser showing the app at localhost:8000](screenshots/02-localhost-browser.png)

**How running applications locally helps in DevOps workflows:**

- Developers can test changes quickly, with no deployment wait and no cost.
- Bugs are caught before code reaches CI/CD or production.
- The same app can be run in Docker locally to confirm the container works before deploying.
- Engineers can reproduce production problems safely in a local copy.
- It lets you check ports, logs and configuration, which are the same things that matter in production.

### Task 2. Exposing the local application with ngrok

```bash
ngrok config add-authtoken <YOUR_TOKEN>
ngrok http 8000
```

**Screenshot 3: ngrok terminal showing the Forwarding line**

![ngrok terminal with the public URL](screenshots/03-ngrok-terminal.png)

**Screenshot 4: app open in the browser through the public ngrok URL**

![Browser showing the app through the ngrok URL](screenshots/04-ngrok-browser.png)

**Public URL generated by ngrok:** `PASTE-YOUR-NGROK-URL-HERE`

**Real-world use case:** Webhook testing. Services such as Stripe, GitHub or Slack send events to a public URL, which a laptop does not have. With ngrok, a developer can receive those webhooks on the app running locally, inspect the requests, and debug the handler before deploying. It is also used to show a work-in-progress site to a client or teammate without deploying it.
