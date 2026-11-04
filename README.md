# Taskly

A personal + college task tracker PWA for the RealtimeTasks Firebase project. The current UI runs with local demo data so the product can be reviewed before Firebase credentials are configured.

## Run locally

Install Node.js 20+ and npm, then run:

```bash
npm install
npm run dev
```

Copy `.env.example` to `.env.local` and fill in the Firebase Web App values. These `VITE_` values are safe to ship to the browser; Firebase Auth and Firestore security rules are the protection boundary. Never add Firebase Admin credentials or Google client secrets here.

## Shared backend contract

Use these Firestore collections so alternate classmate frontends stay compatible:

```text
users/{uid}
  displayName, email, photoURL, collegeId, classId, createdAt

users/{uid}/tasks/{taskId}
  title, status: "todo" | "in_progress" | "done"
  deadline: Timestamp, tag, priority: "low" | "medium" | "high"
  mode: "personal" | "college", notes, createdAt, updatedAt

colleges/{collegeId}/timetable/{entryId}
  classId, dayOfWeek, startTime, endTime, subject, faculty, room, color

colleges/{collegeId}/members/{uid}
  role: "student" | "editor" | "admin", classId
```

Suggested permissions:

- A signed-in user can read/write only `users/{their uid}` and their own tasks.
- Members can read timetable entries for their `collegeId` / `classId`.
- Only `editor` and `admin` roles can create or edit shared timetable entries.
- Only `admin` can manage college membership. Vansh should be the Firebase project admin for Auth providers, Firestore rules, indexes, and Vercel environment variables.

The provided Firebase config belongs in `.env.local`, not committed source. Add Google sign-in in Firebase Authentication, then wire the Firebase adapter into `src/main.tsx` when the shared rules and membership claims are ready.
