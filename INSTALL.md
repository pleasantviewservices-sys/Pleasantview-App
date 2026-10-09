# Locking down Pleasantview: install steps (about 15 minutes, on your PC)

Do these in order. Steps 1 to 3 change nothing your crew will notice. Step 5 is the lock.

## 1. Install the sign-in functions (Supabase)
1. Supabase → your "Final App" project → **SQL Editor** → **New query**.
2. Open `1-install-functions.sql`, copy everything, paste it in, press **Run**. It should say "Success. No rows returned."
Nothing is locked yet. The old app keeps working.

## 2. Upload the new app files (GitHub)
1. Unzip `pleasantview-app-files.zip`.
2. GitHub → your Pleasantview-App repo → **Add file → Upload files**. Drag in ALL the unzipped files (`index.html`, `books.html`, `sw.js`, `manifest.webmanifest` and the icons). Commit.
3. Wait one minute for GitHub Pages to update.

## 3. Test it before locking
- Open the crew app on your phone. You will be asked to sign in again (that is the new server sign-in). Sign in as Owner.
- Open Route, finish a property, open Clients → History → "Printable Service Record".
- Have one employee sign in on their phone and finish a property.
- Open Books, unlock with your owner PIN.
If anything looks wrong, stop here and tell me. Nothing has been locked yet.

## 4. Update the 11:59 email function (only if you haven't already)
Supabase → Edge Functions → daily-report → paste in the latest `daily-report/index.ts` → Deploy.

## 5. Lock the data
SQL Editor → New query → paste `2-lock-down.sql` → Run.
After this, nobody can read or change your data without signing in. Old copies of the app stop working until they are refreshed.

## To undo the lock at any time
SQL Editor → paste `3-undo-lock-down.sql` → Run. Your data is never touched by any of these scripts.

## What changed for you
- Two people finishing the same property at once no longer overwrite each other.
- Employees can no longer see PINs, client phone numbers or emails, Hardscaping, or Books.
- 5 wrong PINs locks that name for 10 minutes.
- Books has a small "Accountant sign-in" link under the Unlock button.
- Edit Client has "Photo required before a visit can be finished".
- Clients → History has "Printable Service Record" (optional date range).

## Good to know
- Photos are still stored in a public photo folder (anyone with a photo's exact link can see it). The links are long and unguessable, but they are not password protected.
- Owner and employee PINs are still stored as plain text in the database, but only the owner (after signing in) can read them.
