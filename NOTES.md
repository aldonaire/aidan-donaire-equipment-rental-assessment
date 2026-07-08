# NOTES.md

## 1. Explain one fix

I fixed the double-booking validation.
The original overlap check only detected some overlapping date ranges and missed cases where a new booking completely covered an existing booking. The old code was:
`return start_b <= start_a <= end_b`
While reviewing the code, I noticed that it did not consider the `end_a` parameter, which meant it was only checking one side of the overlap condition. I verified the logic with several date range examples and found that it failed in certain overlapping scenarios.
I updated the validation to use a complete interval overlap check:
`return start_a <= end_b and end_a >= start_b`
This ensures that any booking with overlapping dates will be rejected, including cases where the new booking starts before or ends after an existing booking.

## 2. Show the failure

Existing booking: Jan 10–15  
Previously allowed: Jan 8–18

## 3. AI Usage

I used ChatGPT and Copilot as development assistants during this task. I used ChatGPT mainly for syntax reminders, clarifying programming concepts, and reviewing Git/GitHub commands since I had not worked with them recently.
I also used AI to discuss possible causes of the reported issues and review my proposed fixes. However, I verified all suggestions by reading the existing code, reproducing the bugs locally, testing the changes, and confirming that the application behaved as expected after the fixes.
