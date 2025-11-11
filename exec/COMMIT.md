IMPORTANT: Use commit-workflow skill if available:
    Check .claude/skills/commit-workflow/SKILL.md
    
Otherwise follow these steps:

Execute these instructions for committing in SIM:

## Pre-Commit

1. **Review changes**:
   ```bash
   git status
   git diff
   ```

2. **Ensure changes complete and tested locally**:
   `npm run ci` - run this in the project root

## Pair Programming Check

3. **Ask: Are you pair programming on this change? (Y/N)**

   **If YES:**
   - Ask: "Who are you pairing with? (name or partial email)"
   - Look up their git identity from commit history:
     ```bash
     git log --all --format="%an <%ae>" | sort -u | grep -i "<search-term>"
     ```
   - Confirm: "Pairing with [Name] <email>? (Y/N)"
   - If incorrect, ask again for correct name/email

   **If NO:** Continue to CI step

## Known Contributors (for reference)

- **Sidu Ponnappa**: sidu@realfast.ai
- **Aniket Hendre**: hendre.ani@gmail.com
- **Bharat**: bharat@realfast.ai
- **Saurav Shah**: saurav@realfast.ai
- **Namanpreet Singh**: namanpreet.singh@realfast.ai
- **Ganesh Hegde**: ganesh.hegde@realfast.ai
- **Harsh**: harsh@realfast.ai
- **Shubham Kumar**: shubham.kumar@realfast.ai
- **Suraj Chandola**: suraj@realfast.ai
- **Claude Code**: noreply@anthropic.com

## CI Build

4. **Run CI build**:
   ```bash
   npm run ci
   ```
   - Wait for full build completion
   - CI includes: Apex tests, LWC tests, ESLint, PMD static analysis

## Commit

5. **If CI is FULLY GREEN** (and ONLY if fully green):

   **Solo Commit Format**:
   ```
   [clickup-ticket-id] Brief description of change

   - Detailed change 1
   - Detailed change 2
   - More changes as needed

   ClickUp: https://app.clickup.com/t/clickup-ticket-id
   ```

   **Pair Programming Commit Format**:
   ```
   [clickup-ticket-id] Brief description of change

   - Detailed change 1
   - Detailed change 2
   - More changes as needed

   ClickUp: https://app.clickup.com/t/clickup-ticket-id

   Co-authored-by: Partner Name <partner@example.com>
   ```

6. **Mob Programming Commit Format**:
   ```
   [clickup-ticket-id] Brief description of change

   - Detailed change 1
   - Detailed change 2
   - More changes as needed

   ClickUp: https://app.clickup.com/t/clickup-ticket-id

   Co-authored-by: Partner A Name <partnerA@example.com>
   Co-authored-by: Partner B Name <partnerB@example.com>
   ```

   **CRITICAL for Pair Commits**:
   - Blank line REQUIRED before `Co-authored-by:` trailer
   - Use exact name and email from git history lookup
   - Format: `Co-authored-by: Name <email>`
   - Each additional co author on a new line

6. **If CI is RED**: Fix issues and retry from step 4

## Post-Commit

7. **Don't update this file** (exec/COMMIT.md)

8. **Push to remote** when ready for team review:
   ```bash
   git push
   ```

---

## Notes

- NO CLAUDE ADS IN COMMIT MESSAGE
- Blank line before Co-authored-by is REQUIRED for proper git attribution
- Multiple co-authors (mob programming):
  ```
  Co-authored-by: Person1 <email1>
  Co-authored-by: Person2 <email2>
  ```
- CI command for SIM: `npm run ci` (NOT `rake ci` like Manazer)

---

## Workflow Summary

```
┌─────────────────────┐
│ Review changes      │
│ (git status/diff)   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Pair programming?   │
└──────┬──────────────┘
       │
   ┌───┴───┐
  YES     NO
   │       │
   ▼       │
┌────────┐ │
│ Lookup │ │
│ partner│ │
│ name/  │ │
│ email  │ │
└───┬────┘ │
    │      │
    └──┬───┘
       ▼
┌─────────────┐
│ npm run ci  │
└──────┬──────┘
       │
   ┌───┴───┐
  GREEN   RED
   │       │
   ▼       ▼
┌──────┐ ┌──────┐
│Commit│ │ Fix  │
│ with │ │issues│
│Co-   │ └──────┘
│author│
│if    │
│pairing
└──────┘
```

---

## Example Interactions

**Solo Commit**:
```
Assistant: Are you pair programming on this change? (Y/N)
User: N
Assistant: Running CI build...
[... CI passes ...]
Assistant: Committing...
[86d0mm2mc] Add multi-author support
...
ClickUp: https://app.clickup.com/t/86d0mm2mc
```

**Pair Commit**:
```
Assistant: Are you pair programming on this change? (Y/N)
User: Yes
Assistant: Who are you pairing with? (name or email)
User: vaibhav
Assistant: Found: Vaibhav Chauhan <vaibhav.chauhan@realfast.ai>
Assistant: Is this correct? (Y/N)
User: Y
Assistant: Running CI build...
[... CI passes ...]
Assistant: Committing with co-author...
[86d0mm2mc] Implement feature

- Added validation
- Updated tests

ClickUp: https://app.clickup.com/t/86d0mm2mc

Co-authored-by: Vaibhav Chauhan <vaibhav.chauhan@realfast.ai>
```
