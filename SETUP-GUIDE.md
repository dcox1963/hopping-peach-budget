# 🍑 Hopping Peach Budget — Setup Guide

You have a real budget **app** (file: `hopping-peach-budget.html`) pre-loaded with your numbers.
It already works on its own. Do **Part A** to use it today; do **Part B** (about 10 minutes,
one time) when you want you and your wife to see the **same live data** on both phones.

---

## Part A — Use it now (1 minute)

1. Get the file onto your iPhone (AirDrop it to yourself, email it, or save it to iCloud Drive).
2. Open it — it opens in Safari.
3. Enter the shared code: **328** (you can change this later, see Part C).
4. Tap **Share** (the box-with-arrow icon) → **Add to Home Screen**. Now it has an icon and
   opens full-screen like a real app.

At this stage each phone keeps its **own** copy. Do Part B to sync them together.

---

## Part B — Turn on live sync (≈10 min, one time)

This connects the app to a **free** Google Firebase database so both phones share one budget.
No credit card, no coding — you only copy 5 values into the file.

### Step 1 — Create the free database
1. On a computer, go to **https://console.firebase.google.com** and sign in with any Google account.
2. Click **Add project** → name it `peach-budget` → keep clicking Continue → **Create project**.
   (You can turn Google Analytics off — not needed.)

### Step 2 — Turn on the database
1. In the left menu, click **Build → Realtime Database** → **Create Database**.
2. Pick the location closest to you → choose **Start in locked mode** → **Enable**.

### Step 3 — Turn on anonymous sign-in
1. Left menu: **Build → Authentication** → **Get started**.
2. Open the **Sign-in method** tab → click **Anonymous** → toggle **Enable** → **Save**.

### Step 3½ — Allow signed-in app access
1. Go back to **Build → Realtime Database** and open the **Rules** tab.
2. Replace the rules with the following, then click **Publish**:

   ```json
   {
     "rules": {
       "budget": {
         ".read": "auth != null",
         ".write": "auth != null"
       }
     }
   }
   ```

This avoids Firebase's temporary test-mode rules, which expire and can leave the app unable to
sync. It also blocks completely unauthenticated database requests.

### Step 4 — Get your 5 values
1. Click the **gear icon** (top left) → **Project settings**.
2. Scroll to **Your apps** → click the **`</>` (Web)** icon.
3. Nickname it `peach` → **Register app**.
4. You'll see a `firebaseConfig` block. Keep this screen open — you need these values:
   `apiKey`, `authDomain`, `databaseURL`, `projectId`, `appId`.
   - If you don't see `databaseURL`, copy it from the Realtime Database page — it looks like
     `https://peach-budget-default-rtdb.firebaseio.com`.

### Step 5 — Paste them into the app
1. Open `hopping-peach-budget.html` in any text editor (Notes works, or TextEdit on Mac).
2. Near the top, find the block that starts with `window.PEACH_CONFIG`. Replace each `"PASTE_HERE"`
   with the matching value from Firebase. It should end up looking like:

   ```
   firebase: {
     apiKey:      "AIzaSyABC123...",
     authDomain:  "peach-budget.firebaseapp.com",
     databaseURL: "https://peach-budget-default-rtdb.firebaseio.com",
     projectId:   "peach-budget",
     appId:       "1:12345:web:abc123"
   }
   ```
3. Save the file.

### Step 6 — Share with your wife
- Send her the **updated** file (the one with your values pasted in). She opens it, enters code
  **328**, and adds it to her home screen too.
- Now when either of you marks a bill paid or edits a number, it updates on **both** phones.
- The little pill at the top right will say **LIVE SYNC** when it's connected (it says **LOCAL**
  until Part B is done).

> Want it even easier to open? Drag the saved file onto **https://app.netlify.com/drop** to get a
> web link you can both bookmark — no app file to pass around.

---

## Part C — Good to know

- **Change the code:** in the file, edit `passcode: "328"` to any code you both like.
- **Privacy:** the code is a convenience lock, not strong account security. Anyone who obtains the
  hosted app/file and its Firebase configuration may be able to reach the shared budget. Keep the
  file/link private, do not store highly sensitive financial identifiers in it, and use local-only
  mode if you do not need sharing.
- **Add/edit anything:** tap a row to edit it, tap the box on a bill to mark it paid, use
  "+ Add" at the bottom of each list. Everything (income, bills, savings, goals) is editable.
- **New month:** just update the amounts and un-check the paid bills — or ask me to add a
  "start fresh month" button.

Questions or want me to tweak the design, categories, or add features (charts, due-date reminders,
multiple months)? Just say so.
