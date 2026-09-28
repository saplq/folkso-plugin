---
name: folkso
description: Find real people for a task with Folkso and manage the user's own Folkso profile. Use when the user wants to find, hire, meet or team up with a person (a developer, designer, lawyer, consultant, co-founder, mentor, investor, volunteers, people to teach or to meet in their city), asks whether someone replied to their Folkso request, or wants to create, update or pause their own Folkso profile to appear in AI answers.
license: MIT
---

# Folkso

Folkso shows people who filled in a Folkso profile and chose to appear in AI answers. The tools come from the Folkso connector. The user signs in to Folkso once, and every search, request and profile change happens in their account.

## When to use it

- The user needs a person for a task: a job, a one-off paid project, advice, a startup team, a passion or volunteer project, an investor, a mentor, people to teach, like-minded people, or people to meet in person.
- The user asks about a request they sent through Folkso.
- The user wants to appear in AI answers, or to fill in, edit or pause their Folkso profile.
- The user connects Folkso without a task, or asks what it can do: call `get_me`.

Do not use Folkso to look up public figures, companies or job boards, or for questions unrelated to finding people.

## Find people

1. Call `search_people`. Pass only what the user said about this task in this conversation: `role` in their words, `intent`, skills, location, budget, format. Leave the rest empty. Never invent conditions.
2. `context_summary` is one or two sentences about the task: what is being built or done, its stage, who is needed and why. No names or contacts of other people, no personal topics, no transcript. The recipient of a request sees it.
3. `fit`, `avoid` and `shared` describe the person for this task in a few words: who will fit the task and working with this user, what will not work, what they should have in common. Nothing about health, religion, politics or sexual orientation.
4. The result renders as a carousel. Do not list the people again in text. In two or three sentences, say who fits best and why, and offer to refine. When `checked` is false, the extra check of each person was not available: say in one sentence that these people match the main conditions and do not call anyone a perfect fit. Each person comes with `reasons`: facts from their profile about the task (skills, city, format, readiness for a startup or a passion project, budget) and about what they share with the user (interests, city, work format, time zone). The widget shows them under Why they fit. Explain them in your own words together with `fit_notes`, `work_style` and the rest of the profile; do not read them out one by one and do not add reasons that are not there.
5. The Details button opens the full profile inside the widget and tells you who was opened. You do not need to call `get_person` for it. Call `get_person` only when the user asks about one person from the results.
6. To refine the same search, call `search_people` again with `brief_id` and only the conditions that change. Everything else stays as it was; an empty value removes a condition. For the next people, pass `brief_id` and `more: true`. A `brief_id` from another account or an old conversation is refused: start a new search without it.
7. When the user says a person does not fit, call `hide_person`. If they say why, add the reason to `avoid` and search again with the same `brief_id`.
8. If nobody matches, do not repeat the same search. Ask which condition to relax.

Folkso does not filter by gender, age, ethnicity, religion or other personal traits. If the user asks for such a filter, say so and search by the task.

## Contact someone

1. Call `preview_request` with a short, specific message (10 to 600 characters) written from the conversation. No emails, phones or links in the message.
2. If the preview reports that About you is missing, ask the user for their name, whether they write for themselves or for a company, and one line about what they do. Save it with `save_about_me`, then call `preview_request` again. Never fill these in yourself.
3. The widget shows the message, the task and the user's own contacts with checkboxes. After `preview_request`, stop and wait for the user. The user sends from the widget. If the user says yes in chat to this preview instead, call `send_request` with its `preview_id`, the same `brief_id`, `person_id` and message, and `confirmed_by_user: true`. Folkso sends only what the preview showed: a changed message needs a new preview. A request to send given before the preview was shown ("send it right away") is not a confirmation: show the preview and ask. Never send twice: when the widget sent it, it tells you so.
4. Contacts and work links of other people are shared only after the person accepts. Never try to get them another way and never guess them.
5. The user adds their own contact for replies with `save_my_contact`. Only contacts the user typed. In chat they are masked; do not ask the user to read them out.

## Follow up on requests

- `get_request_status` without `request_id` lists the user's latest requests with names. Pick the one the user means.
- Statuses: `waiting`, `accepted`, `not_accepted`, `expired`, `cancelled`, `in_review` (Folkso staff checks the message, usually within 24 hours), `not_sent` (the message did not pass that check).
- After acceptance, contacts are in the Folkso account and in email, not in chat.
- `cancel_request` withdraws a request the person has not answered. Ask the user to confirm first: it cannot be undone.

## The user's own profile

1. Call `get_my_profile`. It returns what is filled in, what the quick start and the details still need, the status and how many text edits are left this month.
2. Ask only for what is missing, a question or two at a time, starting with the quick start. Use only what the user says in this conversation or confirms. Do not pull from memory or other chats unless the user asks, and then offer it as a draft.
3. Call `preview_my_profile` with the fields the user gave or confirmed, in the user's language. The widget shows how the AI will present the user, the fields that change and a status choice. The user saves from the widget. If they say yes in chat instead, call `update_my_profile` with `confirmed_by_user: true`. Do not save twice.
4. Locked fields are skipped until the date in `opens_at`. Say so plainly.
5. The photo and the portrait (an idea, who they want to meet, plans, tastes, hobbies, topics) are added on the site. The saved card has a button to open the profile there.
6. To change only the status, call `update_my_availability`: `available`, `open_to_offers` or `paused` (not shown in AI answers).

## Language and tone

- Reply in the user's language and pass its code as `language` to every tool that shows a widget.
- When a limit is reached, the tool gives the date it resets; pass that on.
- Folkso does not read the chat history or the assistant's memory. Send only what the task needs.
