# Troubleshooting: User Likes State and Logging

## Problem

If you see a TypeScript error like:

```
Type 'boolean' is not assignable to type 'number'.
```

or your like button logic is:

```
setLikeCounts((prev) => ({ ...prev, [videoId]: true }))
```

but your state is declared as:

```
const [likeCounts, setLikeCounts] = useState<{ [id: string]: number }>({})
```

then you have a type mismatch: you are storing a boolean in a state that expects a number.

## Solution

Change the like handler to set the value to 1 (or any number), not true:

```
setLikeCounts((prev) => ({ ...prev, [videoId]: 1 }))
```

This matches the state type and avoids TypeScript errors.

## Why set to 1?

In this app, we only care if the user has liked a video (not how many times). Setting the value to 1 is a simple way to flag that the user has liked it, and it matches the state type `{ [id: string]: number }`. All user likes are logged as 1 in the state and can be sent to the backend for analytics or tracking. The UI only uses this to show the red heart, not to increment the public like count.

---

## How the Instagram-style Chat Layout Was Implemented

To make the chat page always show the chat list on the left and the conversation on the right (like Instagram DMs):

- The conditional rendering that previously hid the chat list when a chat was selected was removed.
- A two-column layout was created: the left column always shows the chat list, and the right column shows the conversation if a chat is selected (or a placeholder if not).
- The selected chat is highlighted in the list.
- The Sidebar remains on the far left for navigation.

This approach allows users to always see all chats while viewing a conversation, providing a modern, immersive chat experience similar to Instagram DMs.
