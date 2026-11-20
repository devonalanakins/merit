# The pre-merge checklist I run before any AI-written code merges

One page. One gate. If any piece is missing, it does not ship.

## What Merit does, and what it does not do

Merit validates a versioned contract and a receipt. It compares the receipt to frozen acceptance, rejects changed requirements, mismatched SHAs, and failed checks, and inspects a PR's head SHA and checks through the read-only GitHub API.

Merit does not issue a GO. It cannot independently reproduce a test or observe production. Every assessment marks independently_verified as false, and at most says ready_for_human_review as true. The human still makes the call.

## The gate

1. Frozen contract first. Requirements are frozen before the code is written. If the requirements changed, freeze them again and start the check over.
2. Receipt matches the contract. The receipt is checkable, versioned, and matches the frozen acceptance. A mismatched SHA or a changed requirement is a fail.
3. The PR's real checks. Inspect the PR's head SHA and its real checks. All required checks pass. A green build the agent arranged for itself does not count.
4. Failing test first. The agent reproduces the bug with a failing test before it fixes anything. A fix with no failing test first is a claim, not evidence.
5. The agent never grades its own work. The agent does not edit its own tests to pass, and it does not mark its own work complete. Acceptance needs a separate test and a separate reviewer.
6. Read the diff like a user. Read the diff, read the logs, and test it like a user. If you cannot explain what changed, it does not ship.
7. Explain it in plain words. Can you explain the change to a teammate in plain words? If you cannot, it is not finished, even if the tests pass.
8. Human makes the call. A human reviews the contract, the receipt, the checks, and the diff, then decides. Merit prepares the review. It never merges for you.

## How to use it

Run it in order. Stop at the first fail. Fix that piece, then run the gate again from the top.
