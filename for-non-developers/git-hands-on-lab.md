# Git Hands-On Lab for Non-Developers
## A Practical Guide to Git for Project Management, Documentation, and Collaboration

This hands-on lab is designed specifically for non-developers who need to use Git for project management, document collaboration, content management, or working with development teams. You'll learn Git through practical, real-world scenarios that don't require programming knowledge.

### Who This Lab Is For
- Project managers working with development teams
- Technical writers and documentation specialists
- Content creators and editors
- Business analysts and product managers
- Anyone who needs to collaborate on files and track changes
- Team members who want to understand what developers do with Git

### Prerequisites
- Git installed on your system (we'll help you check this)
- A GitHub account (free to create)
- Basic computer skills (creating folders, editing text files)
- No programming experience required!

### What You'll Learn
This lab covers practical Git skills through real scenarios:
1. **Setting Up Your Digital Project Workspace**
2. **Tracking Changes in Documents** (like version control for Word docs, but better!)
3. **Working on Different Versions Simultaneously** (branches for different ideas/drafts)
4. **Collaborating Without Overwriting Each Other's Work**
5. **Handling Conflicts When Multiple People Edit the Same Thing**
6. **Going Back to Previous Versions** (better than "Save As" with dates!)
7. **Creating Milestones and Releases** (marking important versions)
8. **Best Practices for Team Collaboration**

---

## Before We Start: Understanding Git

### What is Git?
Think of Git as a **super-powered "Track Changes"** for any type of file. Instead of having files like:
- `Project_Plan_v1.docx`
- `Project_Plan_v2_final.docx`
- `Project_Plan_v2_final_FINAL.docx`
- `Project_Plan_v2_final_FINAL_for_real_this_time.docx`

Git helps you:
- Keep one file with a complete history of all changes
- See exactly what changed, when, and who changed it
- Work on different ideas simultaneously without losing anything
- Collaborate with others without the "email attachment nightmare"
- Go back to any previous version instantly

### Real-World Scenarios Where Git Helps
- **Documentation teams**: Multiple writers working on user manuals
- **Project managers**: Tracking project plans, requirements, and specifications
- **Content creators**: Managing website content, blog posts, or marketing materials
- **Business analysts**: Collaborating on requirements documents and process flows
- **Anyone working with developers**: Understanding how code changes are managed

---

## Lab Setup

### Step 1: Check if Git is Installed
```bash
# Check if Git is installed on your computer
git --version
```
**What you should see**: Something like `git version 2.x.x`
**If you see an error**: You need to install Git first
- **Mac**: Install from [git-scm.com](https://git-scm.com/) or use `brew install git`
- **Windows**: Download from [git-scm.com](https://git-scm.com/)
- **Linux**: Use your package manager (e.g., `sudo apt install git`)

### Step 2: Create Your Practice Project on GitHub
**Why GitHub?** It's like Google Drive or Dropbox, but designed specifically for Git

1. Go to [GitHub.com](https://github.com) and sign up for a free account
2. Click the green "New" button (or "+" in the top right)
3. Repository name: `my-first-git-project`
4. Description: "Learning Git for project collaboration"
5. Make sure it's **Public** (so you can share it later if you want)
6. ✅ Check "Add a README file"
7. Click "Create repository"
8. Copy the repository URL (green "Code" button → HTTPS tab)

### Step 3: Set Up Your Identity
```bash
# Tell Git who you are (this appears in all your changes)
git config --global user.name "Your Full Name"
git config --global user.email "your.email@example.com"

# Check your configuration
git config --list | grep user
```

### Step 4: Choose Your Working Directory
```bash
# Navigate to where you want to keep your project
# This could be your Desktop, Documents folder, or anywhere you like
cd ~/Desktop  # Or cd ~/Documents, or wherever you prefer
```

---

## Section 1: Getting Your Project from GitHub to Your Computer

### "Cloning" = Downloading + Connecting
**Real-world analogy**: Like downloading a shared Google Drive folder, but keeping it synced

```bash
# Download your project from GitHub to your computer
# Replace 'yourusername' with your actual GitHub username
git clone https://github.com/yourusername/my-first-git-project.git

# Move into the project folder
cd my-first-git-project

# Check what Git thinks about your project right now
git status
```

**What you should see**: 
- "On branch main" (you're on the main version)
- "nothing to commit, working tree clean" (no changes yet)
- Your project folder now exists on your computer

```bash
# Look at what's in your project folder
ls -la

# See where this project is connected to online
git remote -v
```

---

## Section 2: Making Your First Changes (The Basic Git Workflow)

### The Three-Step Dance: Add → Commit → Push
**Think of it like**: Drafting an email → Writing the subject line → Sending it

#### Step 1: Create a Project Plan Document
```bash
# Create a project plan (like a simple text document)
cat << 'EOF' > project-plan.md
# My First Git Project Plan

## Project Goals
- Learn Git basics
- Practice collaboration
- Build confidence with version control

## Timeline
- Week 1: Learn basic Git commands
- Week 2: Practice branching and merging
- Week 3: Try collaboration features

## Team Members
- Me (Project Lead)
- [Add team members as they join]
EOF

# Check what Git thinks about this new file
git status
```

**What you'll see**: Git notices there's a new file but says it's "untracked"

#### Step 2: Tell Git to Track Your Changes
```bash
# Add the file to Git's tracking (like "Draft" in email)
git add project-plan.md

# Check status again
git status
```

**Now you'll see**: "Changes to be committed" - Git is ready to save this version

#### Step 3: Commit (Save This Version)
```bash
# Commit with a clear message about what you did
git commit -m "Add initial project plan with goals and timeline"

# See your change history
git log --oneline
```

#### Step 4: Push (Share with Others/Backup Online)
```bash
# Send your changes to GitHub
git push origin main
```

**Success!** Go to your GitHub page and refresh - you'll see your new file there!

### Adding More Project Documents

#### Create a Meeting Notes Template
```bash
# Create a template for meeting notes
cat << 'EOF' > meeting-notes-template.md
# Meeting Notes Template

## Date: [INSERT DATE]
## Attendees: [LIST ATTENDEES]

### Agenda Items
1. [ITEM 1]
2. [ITEM 2]
3. [ITEM 3]

### Decisions Made
- [DECISION 1]
- [DECISION 2]

### Action Items
- [ ] [ACTION ITEM] - Assigned to: [NAME] - Due: [DATE]
- [ ] [ACTION ITEM] - Assigned to: [NAME] - Due: [DATE]

### Next Meeting
- Date: [DATE]
- Topics: [TOPICS]
EOF

# Add and commit the template
git add meeting-notes-template.md
git commit -m "Add meeting notes template for project organization"
```

#### Create a Project Requirements Document
```bash
# Create a requirements document
cat << 'EOF' > requirements.md
# Project Requirements

## Business Requirements
1. Must be easy to use for non-technical team members
2. Should integrate with existing tools
3. Must be completed within budget and timeline

## Technical Requirements
1. Cross-platform compatibility
2. Security compliance
3. Scalable architecture

## User Requirements
1. Intuitive user interface
2. Mobile-friendly design
3. Fast loading times

## Success Criteria
- User adoption rate > 80%
- System uptime > 99%
- Positive user feedback > 4/5 stars
EOF

# Add and commit requirements
git add requirements.md
git commit -m "Add project requirements and success criteria"

# Push all changes to GitHub
git push origin main

# Look at your project's change history
git log --oneline --graph
```

**What you've accomplished**:
✅ Created a project workspace
✅ Added and tracked multiple documents
✅ Created a clear history of changes
✅ Backed everything up to GitHub
✅ Can see exactly what changed and when

---

## Section 3: Working with Different Versions (Branching)

### Understanding Branches
**Real-world analogy**: Like working on different drafts of a document simultaneously
- **Main branch** = The "official" version that everyone sees
- **Feature branch** = Your "draft" version where you try new ideas
- You can switch between them instantly without losing work
- When your draft is ready, you can merge it into the official version

#### Practical Scenario: Testing Different Project Approaches

```bash
# Create a branch to experiment with a different project approach
git checkout -b experiment/agile-approach

# See which branch you're on (the * shows your current branch)
git branch
```

**What you'll see**: `* experiment/agile-approach` (you're now on your experimental branch)

#### Make Changes Without Affecting Main Version
```bash
# Create an alternative project plan focused on Agile methodology
cat << 'EOF' > project-plan-agile.md
# Agile Project Plan

## Sprint Structure
- Sprint Duration: 2 weeks
- Daily Stand-ups: 9:00 AM
- Sprint Review: Every other Friday
- Sprint Retrospective: Following Sprint Review

## Sprint 1 Goals (Weeks 1-2)
- Set up project infrastructure
- Define user stories
- Create initial wireframes

## Sprint 2 Goals (Weeks 3-4)
- Develop minimum viable product (MVP)
- User testing with 5 participants
- Gather feedback and prioritize backlog

## Team Roles
- Scrum Master: [To be assigned]
- Product Owner: [To be assigned]
- Development Team: [List team members]

## Definition of Done
- [ ] Feature is coded and tested
- [ ] Documentation is updated
- [ ] Code review is completed
- [ ] Product Owner accepts the feature
EOF

# Also update your meeting template for Agile ceremonies
cat << 'EOF' > agile-ceremonies.md
# Agile Ceremonies

## Daily Standup Template
- What did I complete yesterday?
- What will I work on today?
- Are there any blockers or impediments?

## Sprint Planning Template
- Review product backlog
- Estimate story points
- Commit to sprint backlog
- Define sprint goal

## Sprint Review Template
- Demo completed features
- Gather stakeholder feedback
- Update product backlog

## Sprint Retrospective Template
- What went well?
- What could be improved?
- What actions will we take?
EOF

# Check what changed compared to main branch
git status

# Add and commit your experimental changes
git add project-plan-agile.md agile-ceremonies.md
git commit -m "Add Agile project methodology as alternative approach"

# Push your experimental branch to GitHub
git push -u origin experiment/agile-approach
```

**What just happened**:
✅ You created a separate "workspace" for trying new ideas
✅ Your original project plan in `main` is completely unchanged
✅ You can switch back and forth between approaches
✅ Your team can see both approaches on GitHub

---

## Section 4: Creating Another Alternative (Branch from Branch)

### Scenario: Trying a Hybrid Approach
**Real situation**: Maybe pure Agile isn't right, but a hybrid approach might work

```bash
# Create a new branch based on your Agile experiment
git checkout -b experiment/hybrid-approach

# Create a hybrid project plan that combines traditional and agile elements
cat << 'EOF' > project-plan-hybrid.md
# Hybrid Project Plan (Traditional + Agile)

## Phase 1: Planning (Traditional)
- Detailed requirements gathering (2 weeks)
- Technical architecture design (1 week)
- Resource allocation and timeline (1 week)

## Phase 2: Development (Agile)
- 2-week sprints with daily standups
- Sprint reviews with stakeholders
- Continuous integration and testing

## Phase 3: Deployment (Traditional)
- User acceptance testing (2 weeks)
- Production deployment plan (1 week)
- Documentation and training (1 week)

## Governance
- Weekly steering committee meetings
- Bi-weekly sprint reviews
- Monthly progress reports to executives

## Risk Management
- Traditional risk register maintained
- Agile retrospectives for continuous improvement
- Monthly risk assessment meetings
EOF

# Create a hybrid meeting schedule
cat << 'EOF' > hybrid-meeting-schedule.md
# Hybrid Meeting Schedule

## Weekly Meetings
- Monday: Sprint Planning (if start of sprint)
- Daily: 15-min standups (Tue-Fri)
- Friday: Sprint Review (if end of sprint)

## Bi-weekly Meetings
- Sprint Retrospectives
- Stakeholder Progress Reviews

## Monthly Meetings
- Executive Steering Committee
- Risk Assessment Review
- Budget and Timeline Review

## Quarterly Meetings
- Project Health Assessment
- Strategic Alignment Review
EOF

# Commit your hybrid approach
git add project-plan-hybrid.md hybrid-meeting-schedule.md
git commit -m "Create hybrid project approach combining traditional and agile methods"

# Push this new alternative to GitHub
git push -u origin experiment/hybrid-approach
```

**Now you have three different approaches**:
1. **main** - Original traditional approach
2. **experiment/agile-approach** - Pure Agile methodology
3. **experiment/hybrid-approach** - Hybrid traditional + Agile

---

## Section 5: Choosing and Merging the Best Approach

### Scenario: Team Decides on the Hybrid Approach
**Real situation**: After discussion, your team likes the hybrid approach best

```bash
# Switch back to your main branch (the official version)
git checkout main

# Make sure you have the latest main branch
git pull origin main

# Merge the hybrid approach into main
git merge experiment/hybrid-approach

# Look at your project history
git log --oneline --graph

# Push the updated main branch
git push origin main
```

**What happened**:
✅ Your main project now includes the hybrid approach
✅ All the history is preserved - you can see the evolution of ideas
✅ Your experimental branches still exist if you want to reference them
✅ Your team now has the "official" hybrid methodology

---

## Section 6: Handling Real Collaboration Conflicts

### Understanding Conflicts in Business Context
**Real-world scenario**: Two team members work on the same document simultaneously - this is where Git shines!

**What we'll simulate**:
- You (on main branch) update the project requirements
- A colleague (on hybrid branch) also updates the same requirements  
- When you try to merge, Git finds conflicts and asks you to resolve them
- This happens in real teams all the time!

### Set Up a Realistic Conflict Scenario
```bash
# Switch back to main branch 
git checkout main

# You decide to update the project requirements based on stakeholder feedback
cat << 'EOF' > requirements.md
# Project Requirements (Updated)

## Business Requirements
1. Must be easy to use for non-technical team members
2. Should integrate with existing tools
3. Must be completed within budget and timeline
4. **NEW: Must support mobile devices**
5. **NEW: Must comply with GDPR regulations**

## Technical Requirements
1. Cross-platform compatibility
2. Security compliance with ISO 27001
3. Scalable architecture supporting 10,000+ users
4. **NEW: API-first design for future integrations**

## User Requirements
1. Intuitive user interface with minimal training needed
2. Mobile-responsive design
3. Fast loading times (under 3 seconds)
4. **NEW: Accessibility compliance (WCAG 2.1)**

## Success Criteria
- User adoption rate > 85% (increased from 80%)
- System uptime > 99.5% (increased from 99%)
- Positive user feedback > 4/5 stars
- **NEW: Mobile usage accounts for 40%+ of total usage**
EOF

# Commit your changes to main
git add requirements.md
git commit -m "Update requirements based on stakeholder feedback - add mobile and compliance needs"
```

### Now Create the Conflict
```bash
# Try to merge your hybrid approach branch (which also modified requirements)
git merge experiment/hybrid-approach

# Git will show a conflict message like:
# "CONFLICT (content): Merge conflict in requirements.md"
# "Automatic merge failed; fix conflicts and then commit the result."

# Check what Git is telling you
git status
```

**What you'll see**: Git shows which files have conflicts and need your attention

### View and Understand the Conflict
```bash
# Look at the conflicted file
cat requirements.md
```

**What you'll see**: Git adds special markers showing the conflicting sections:
```
<<<<<<< HEAD
(Your changes from main branch)
=======
(Changes from the hybrid-approach branch)
>>>>>>> experiment/hybrid-approach
```

### Resolve the Conflict Like a Project Manager
**Real-world decision**: Combine the best of both versions

```bash
# Create the resolved version that combines both sets of changes
cat << 'EOF' > requirements.md
# Project Requirements (Merged from Stakeholder Feedback & Hybrid Approach)

## Business Requirements
1. Must be easy to use for non-technical team members
2. Should integrate with existing tools and workflows
3. Must be completed within budget and timeline
4. **NEW: Must support mobile devices and responsive design**
5. **NEW: Must comply with GDPR and data privacy regulations**
6. **FROM HYBRID: Should support both agile and traditional project phases**

## Technical Requirements
1. Cross-platform compatibility (Windows, Mac, Linux, Mobile)
2. Security compliance with ISO 27001 standards
3. Scalable architecture supporting 10,000+ concurrent users
4. **NEW: API-first design for future integrations**
5. **FROM HYBRID: Support for both rapid iteration and stable releases**

## User Requirements
1. Intuitive user interface with minimal training needed
2. Mobile-responsive design for tablets and phones
3. Fast loading times (under 3 seconds on all devices)
4. **NEW: Accessibility compliance (WCAG 2.1 Level AA)**
5. **FROM HYBRID: Support for both power users and casual users**

## Success Criteria
- User adoption rate > 85% across all user types
- System uptime > 99.5% during business hours
- Positive user feedback > 4/5 stars
- **NEW: Mobile usage accounts for 40%+ of total usage**
- **FROM HYBRID: Successful completion of both agile and traditional phases**

## Implementation Approach
- Phase 1: Core functionality (traditional planning)
- Phase 2: Iterative improvements (agile sprints)
- Phase 3: Mobile optimization and accessibility features
EOF

# Tell Git the conflict is resolved
git add requirements.md

# Complete the merge with a descriptive message
git commit -m "Merge hybrid approach with stakeholder requirements - combined mobile, compliance, and methodology needs"

# Check your project history
git log --oneline --graph -n 5

# Push the resolved changes
git push origin main
```

### What Just Happened? (Business Impact)
**✅ Successful Collaboration**: 
- You handled simultaneous changes without losing anyone's work
- Combined stakeholder feedback with team methodology preferences
- Created a comprehensive requirements document
- Maintained complete history of all decisions

**Real-world application**:
- No more "Which version is the latest?" confusion
- Clear audit trail of all requirement changes
- Team members can work independently without stepping on each other
- Stakeholder input is preserved and integrated, not overwritten

### Practice Scenario: Meeting Notes Conflict
Let's create another realistic conflict with meeting notes:

```bash
# Create initial meeting notes
cat << 'EOF' > sprint-review-notes.md
# Sprint Review Meeting - [DATE]

## Attendees
- Project Manager
- Development Team Lead
- Product Owner

## Demo Results
- User login feature completed
- Dashboard mockups reviewed
- Database integration in progress

## Feedback
- Stakeholders happy with progress
- Minor UI adjustments requested

## Next Sprint Goals
- Complete dashboard implementation
- Begin user testing phase
EOF

git add sprint-review-notes.md
git commit -m "Add initial sprint review meeting notes"

# Create a branch where a colleague adds their notes
git checkout -b meeting-updates/detailed-feedback

# Colleague adds more detailed feedback
cat << 'EOF' > sprint-review-notes.md
# Sprint Review Meeting - March 15, 2024

## Attendees
- Project Manager (Sarah)
- Development Team Lead (Mike)
- Product Owner (Lisa)
- UX Designer (Alex) - joined remotely
- Stakeholder Representative (Tom)

## Demo Results
- User login feature completed ✅
  - Password reset functionality working
  - Two-factor authentication implemented
- Dashboard mockups reviewed ✅
  - Positive feedback on layout
  - Color scheme approved
- Database integration in progress 🔄
  - 70% complete
  - Performance testing pending

## Detailed Feedback
- Stakeholders very happy with progress
- Minor UI adjustments requested:
  - Larger buttons for accessibility
  - Better error messages
  - Loading indicators needed

## Action Items
- [ ] Implement UI adjustments - Alex (Due: March 22)
- [ ] Complete database integration - Mike (Due: March 20)
- [ ] Prepare user testing plan - Lisa (Due: March 18)

## Next Sprint Goals
- Complete dashboard implementation
- Begin user testing phase with 10 participants
- Address any critical bugs found
EOF

git add sprint-review-notes.md
git commit -m "Add detailed attendee info and action items"
git push -u origin meeting-updates/detailed-feedback

# Switch back to main and make different changes
git checkout main

# You add different information to the same file
cat << 'EOF' > sprint-review-notes.md
# Sprint Review Meeting - March 15, 2024

## Attendees
- Project Manager
- Development Team Lead  
- Product Owner

## Demo Results
- User login feature completed
- Dashboard mockups reviewed
- Database integration in progress

## Feedback
- Stakeholders happy with progress
- Minor UI adjustments requested

## Budget Update
- Sprint completed under budget
- 15% budget remaining for current phase
- Additional resources approved for testing phase

## Risk Assessment
- Low risk for current sprint goals
- Database performance needs monitoring
- User testing timeline is aggressive but achievable

## Next Sprint Goals
- Complete dashboard implementation
- Begin user testing phase
- Conduct security review
EOF

git add sprint-review-notes.md
git commit -m "Add budget and risk assessment information"

# Now merge and resolve the conflict
git merge meeting-updates/detailed-feedback

# Git will show conflicts - resolve them
cat << 'EOF' > sprint-review-notes.md
# Sprint Review Meeting - March 15, 2024

## Attendees
- Project Manager (Sarah)
- Development Team Lead (Mike)
- Product Owner (Lisa)
- UX Designer (Alex) - joined remotely
- Stakeholder Representative (Tom)

## Demo Results
- User login feature completed ✅
  - Password reset functionality working
  - Two-factor authentication implemented
- Dashboard mockups reviewed ✅
  - Positive feedback on layout
  - Color scheme approved
- Database integration in progress 🔄
  - 70% complete
  - Performance testing pending

## Detailed Feedback
- Stakeholders very happy with progress
- Minor UI adjustments requested:
  - Larger buttons for accessibility
  - Better error messages
  - Loading indicators needed

## Action Items
- [ ] Implement UI adjustments - Alex (Due: March 22)
- [ ] Complete database integration - Mike (Due: March 20)
- [ ] Prepare user testing plan - Lisa (Due: March 18)

## Budget Update
- Sprint completed under budget
- 15% budget remaining for current phase
- Additional resources approved for testing phase

## Risk Assessment
- Low risk for current sprint goals
- Database performance needs monitoring
- User testing timeline is aggressive but achievable

## Next Sprint Goals
- Complete dashboard implementation
- Begin user testing phase with 10 participants
- Address any critical bugs found
- Conduct security review
EOF

# Mark conflict as resolved and commit
git add sprint-review-notes.md
git commit -m "Merge detailed meeting notes with budget and risk information"

# Push the final version
git push origin main
```

**What you've mastered**:
✅ **Real conflict resolution** - Combined different team members' contributions
✅ **Business decision making** - Chose what to keep, combine, or modify
✅ **Professional documentation** - Created comprehensive, useful documents
✅ **Team collaboration** - No one's work was lost or overwritten

---

## Section 7: Managing Your Project History (Time Travel for Documents!)

### Understanding Project History
**Real-world scenario**: Sometimes you need to undo changes or go back to a previous version of your project documents

**Business examples**:
- A stakeholder wants to see what the requirements looked like last month
- You accidentally deleted important content and need to recover it
- A decision was made that needs to be reversed
- You want to see the evolution of your project over time

### View Your Project's Change History
```bash
# See a visual timeline of all your project changes
git log --oneline --graph --all

# View changes with more details (who, when, what)
git log --graph --pretty=format:'%h -%d %s (%cr) <%an>' --abbrev-commit

# See just the recent changes (last 5)
git log --oneline | head -5
```

**What you'll see**: A timeline showing:
- Every change made to your project
- Who made each change
- When it was made
- A brief description of what changed

### Scenario: Undoing a Problematic Change
**Real situation**: You added some experimental content that you now want to remove

```bash
# Let's create a change that we'll later want to undo
cat << 'EOF' > experimental-approach.md
# Experimental Project Approach (DRAFT - DO NOT USE)

## Untested Methodology
- This is just an idea we're exploring
- Not approved by stakeholders
- May not work with our constraints

## Risks
- Could delay the project
- Might confuse the team
- Hasn't been validated

**NOTE: This is experimental and should not be implemented yet**
EOF

git add experimental-approach.md
git commit -m "Add experimental approach document (draft only)"

# Push the change
git push origin main
```

### Safely Undo the Change
**The safe way**: Use `git revert` (creates a new change that undoes the previous one)

```bash
# Find the commit you want to undo
git log --oneline -n 3

# Revert the last commit (the experimental document)
TEMP_COMMIT=$(git log --oneline -n 1 | cut -d' ' -f1)
git revert $TEMP_COMMIT

# Git will ask you to confirm - the default message is usually fine
# This creates a new commit that removes the experimental document

# Check that it worked
git log --oneline -n 3
ls -la  # The experimental file should be gone

# Push the revert
git push origin main
```

**What happened**:
✅ The experimental document is removed
✅ The history shows both the addition AND the removal
✅ Nothing is permanently deleted - you can always see what was tried
✅ Stakeholders can see the complete decision trail

### Understanding Reset vs Revert (Business Context)
**Important concept**: Two ways to "undo" changes

#### Demo: The Difference
```bash
# Create a lessons-learned document
cat << 'EOF' > lessons-learned.md
# Project Lessons Learned

## What Worked Well
- Team communication improved with daily standups
- Documentation in Git eliminated version confusion
- Stakeholder feedback integration was smooth

## Areas for Improvement
- Need better initial requirements gathering
- Testing phase should start earlier
- Risk assessment needs more detail

## Recommendations for Next Project
- Continue using Git for all documentation
- Start user testing in week 2, not week 4
- Include security review in initial planning
EOF

git add lessons-learned.md
git commit -m "Add initial project lessons learned document"

# View current history
echo "Current project history:"
git log --oneline -n 3

# Demonstrate soft reset (keeps the content but "uncommits" it)
echo "\nUsing soft reset to modify the last commit..."
git reset --soft HEAD~1
git status  # Shows the file is still staged, ready to commit

# Now recommit with a better message
git commit -m "Add comprehensive lessons learned and recommendations for future projects"

# Push the corrected version
git push origin main
```

**Key Differences**:
- **Revert**: Creates new change that undoes previous change (safe, preserves history)
- **Reset**: Moves backward in history (use carefully, can lose work)

**For non-developers**: 
- Use **revert** when you want to undo something but keep the history
- Use **reset** when you want to modify recent changes before sharing them

---

## Section 8: Creating Project Milestones (Tagging)

### Understanding Tags in Business Context
**Real-world analogy**: Like bookmarking important moments in your project

**Business uses for tags**:
- Mark major project milestones (v1.0 = "Requirements Approved")
- Create snapshots for stakeholder reviews (v0.5 = "Draft for Review") 
- Track deliverable versions (v2.1 = "Final Documentation Package")
- Archive project phases ("Phase-1-Complete", "Phase-2-Complete")

### Create Your First Project Milestone
```bash
# Mark your current project state as a major milestone
git tag project-requirements-complete

# List all your milestones
git tag

# Create a milestone with detailed notes
git tag -a stakeholder-review-v1 -m "Project documentation ready for stakeholder review - includes requirements, methodology, and initial planning"

# View milestone information
git show stakeholder-review-v1
```

**What you'll see**: All the changes included in this milestone and your descriptive message

### Share Milestones with Your Team
```bash
# Push a specific milestone to GitHub
git push origin project-requirements-complete

# Push all milestones at once
git push origin --tags

# Verify milestones are available online
git ls-remote --tags origin
```

**Business benefit**: Team members and stakeholders can easily access any major version

### Creating Milestones for Specific Project Phases
```bash
# Look at your project timeline
git log --oneline -n 5

# Tag the very first commit as your project foundation
FIRST_COMMIT=$(git log --oneline | tail -1 | cut -d' ' -f1)
git tag -a project-foundation $FIRST_COMMIT -m "Initial project setup and basic planning documents"

# Push this historical milestone
git push origin project-foundation

# See all your milestones with descriptions
git tag -l -n1
```

### Practical Milestone Examples
```bash
# Create meaningful business milestones
git tag -a requirements-approved -m "All stakeholder requirements gathered and approved"
git tag -a design-phase-complete -m "Project design and methodology finalized"
git tag -a documentation-ready -m "All project documentation complete and reviewed"

# Push milestone collection
git push origin --tags
```

**Real-world application**:
- ✅ Stakeholders can easily find and reference specific project phases
- ✅ Team can quickly access any major deliverable version
- ✅ Clear project timeline with named milestones
- ✅ Easy rollback to any major project state if needed

---

## Section 9: Advanced Project Management Techniques

### Working with Remote Project Branches
**Business scenario**: Your team has multiple project approaches being developed simultaneously

```bash
# Get the latest information about all team branches
git fetch origin

# See all project approaches (local and remote)
git branch -a

# Work on a colleague's branch locally
git checkout -b local-copy-hybrid origin/experiment/hybrid-approach

# After project decisions are made, clean up unused approaches
git push origin --delete experiment/agile-approach
git push origin --delete experiment/hybrid-approach

# Remove local copies of decided-against approaches
git branch -d experiment/agile-approach
git branch -d experiment/hybrid-approach
git branch -d local-copy-hybrid
```

**Business benefit**: Keep your project workspace clean while preserving the decision history

### Temporarily Saving Work in Progress (Stashing)
**Real scenario**: You're in the middle of updating a document when an urgent change request comes in

```bash
# You're working on updates to the project plan
echo "\n## New Section: Risk Mitigation Strategies\n- [Work in progress...]" >> project-plan.md

# Urgent request comes in - need to switch tasks immediately
# Save your work-in-progress without committing
git stash

# Your workspace is now clean for the urgent task
git status  # Should show "working tree clean"

# Handle the urgent request...
echo "URGENT: Stakeholder meeting moved to tomorrow 9 AM" > urgent-notice.md
git add urgent-notice.md
git commit -m "Add urgent notice about stakeholder meeting change"
git push origin main

# Now return to your original work
git stash list  # Shows your saved work
git stash pop   # Brings back your work-in-progress

# Continue where you left off
git status  # Shows your project-plan.md changes are back

# When ready, commit your completed work
git add project-plan.md
git commit -m "Add risk mitigation strategies section to project plan"
git push origin main

# Clean up the urgent notice
rm urgent-notice.md
git add urgent-notice.md
git commit -m "Remove urgent notice after meeting reschedule handled"
git push origin main
```

**Real-world application**:
- ✅ Handle interruptions without losing work
- ✅ Switch between tasks seamlessly
- ✅ Keep your workspace organized
- ✅ Never lose work-in-progress due to urgent requests

---

## Section 10: Project Cleanup and Summary

### Clean Up Your Project Workspace
**Business scenario**: Project is complete, time to organize and archive

```bash
# View all your project milestones
git tag

# Remove any test milestones (if you created any)
# git tag -d test-milestone  # Only if you want to remove one

# Remove any test milestone from GitHub (if needed)
# git push origin --delete test-milestone  # Only if you want to remove one

# Final project state summary
echo "=== Final Project Workspace State ==="
echo "Project approaches explored:"
git branch -a
echo -e "\nProject milestones created:"
git tag
echo -e "\nRecent project changes:"
git log --oneline -n 5
```

### Create a Summary Document
```bash
# Create a lab summary
cat << 'EOF' > lab-summary.md
# Git Hands-On Lab Summary

## What We Accomplished

### 1. Repository Management
- Cloned a repository from GitHub
- Configured Git user settings
- Pushed changes to remote repository

### 2. Basic Git Operations
- Created and edited files
- Used `git add` to stage changes
- Made commits with descriptive messages
- Pushed commits to remote repository

### 3. Branching
- Created branches with `git checkout -b`
- Switched between branches
- Created branches from other branches
- Pushed branches to remote

### 4. Merging
- Merged feature branches into main
- Handled fast-forward merges
- Resolved merge conflicts manually
- Completed merge commits

### 5. Conflict Resolution
- Created intentional conflicts
- Identified conflict markers
- Manually resolved conflicts
- Completed conflict resolution with merge commit

### 6. Commit Management
- Viewed commit history with `git log`
- Reverted commits with `git revert`
- Demonstrated difference between reset and revert

### 7. Tagging
- Created lightweight tags
- Created annotated tags with messages
- Tagged specific commits
- Pushed tags to remote repository
- Managed tag lifecycle

### 8. Advanced Operations
- Worked with remote branches
- Used git stash for temporary changes
- Cleaned up branches and tags

## Key Git Commands Learned

### Repository Operations
- `git clone <url>`
- `git remote -v`
- `git status`

### Basic Operations
- `git add <file>`
- `git commit -m "message"`
- `git push origin <branch>`
- `git pull origin <branch>`

### Branching
- `git checkout -b <branch-name>`
- `git branch`
- `git merge <branch-name>`

### History and Conflicts
- `git log --oneline --graph`
- `git revert <commit-hash>`
- `git reset --soft HEAD~1`

### Tagging
- `git tag <tag-name>`
- `git tag -a <tag-name> -m "message"`
- `git push origin --tags`

### Cleanup
- `git branch -d <branch-name>`
- `git push origin --delete <branch-name>`
- `git tag -d <tag-name>`

## Best Practices Learned
1. Always write descriptive commit messages
2. Use branches for feature development
3. Resolve conflicts carefully and test afterwards
4. Use annotated tags for releases
5. Keep commit history clean and meaningful
6. Push changes regularly to avoid conflicts
7. Use `git status` frequently to understand repository state

## Next Steps
- Practice with pull requests/merge requests
- Learn about Git hooks
- Explore advanced Git workflows (Git Flow, GitHub Flow)
- Study Git internals and object model
EOF

# Add and commit the summary
git add lab-summary.md
git commit -m "Add comprehensive lab summary and best practices"

# Final push
git push origin main

echo "=== Git Hands-On Lab Completed Successfully! ==="
echo "Check your GitHub repository to see all the changes."
echo "Summary document created: lab-summary.md"
```

---

## Verification Steps

After completing the lab, verify your learning by running these commands:

```bash
# Verify repository state
echo "Repository branches:"
git branch -a

echo -e "\nRepository tags:"
git tag

echo -e "\nRecent commit history:"
git log --oneline --graph -n 10

echo -e "\nRemote configuration:"
git remote -v

echo -e "\nRepository status:"
git status
```

---

## Troubleshooting Common Issues

### Authentication Issues
If you encounter authentication problems:
```bash
# For HTTPS (will prompt for credentials)
git remote set-url origin https://github.com/username/git-lab-practice.git

# For SSH (requires SSH key setup)
git remote set-url origin git@github.com:username/git-lab-practice.git
```

### Merge Conflict Help
If you get stuck with merge conflicts:
```bash
# Abort the merge and start over
git merge --abort

# Or get help with merge tools
git mergetool
```

### Branch Issues
If you're on the wrong branch:
```bash
# See all branches
git branch -a

# Switch to correct branch
git checkout main
```

---

**Congratulations!** You've completed a comprehensive Git hands-on lab covering all major Git CLI operations. You now have practical experience with:

- **Project workspace setup and management**
- **Document version control** (add, commit, push)
- **Testing different approaches simultaneously** (branching)
- **Collaborating without conflicts** (merging and conflict resolution)
- **Project history management** and recovery
- **Creating project milestones** and deliverable tracking
- **Professional project organization** and cleanup

## What This Means for Your Work

You can now:

✅ **Eliminate version confusion** - No more files with "_final_FINAL" in the name
✅ **Collaborate confidently** - Work with team members without overwriting each other's changes
✅ **Track project evolution** - See exactly how your project developed over time
✅ **Recover from mistakes** - Easily go back to previous versions when needed
✅ **Organize deliverables** - Create clear milestones and project phases
✅ **Work with developers** - Understand and participate in technical team workflows

## Keep Learning and Growing

**Continue using Git for your projects!** The more you practice with real work documents, the more natural these skills will become. You're now equipped to bring professional version control to any team or project.

**Share your knowledge** - Help colleagues learn Git and transform how your team collaborates on documents and projects!

---

*🎉 You've successfully bridged the gap between business and technical collaboration! 🎉*
