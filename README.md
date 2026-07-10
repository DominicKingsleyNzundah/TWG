# Improving Health Research Visibility through Metadata: A Microlearning Approach Using the DDI Codebook Standard

Self-contained H5P course folder, ready to drop into your assigned spot
in the shared repo. Everything it needs (player + both H5P packages)
lives inside this folder using relative paths only — nothing outside
it is required.

## What's inside

```
my-course/
├── index.html         ← course shell: sidebar nav, progress lock/unlock, loads each part
├── h5p-player/         ← h5p-standalone player library
├── course/             ← your H5P.CoursePresentation package (5 modules, videos via YouTube)
└── final-quiz/         ← your standalone H5P.QuestionSet (5 questions, 4/5 to pass)
```

`index.html` shows `course` first; once you click "Mark complete &
continue" it unlocks and switches to `final-quiz`. Progress + the
unlock state are remembered per-browser via `localStorage`
(key `course-progress:ddi-metadata-microlearning`) — see the note on
that below.

## Deploying

Just place this whole `my-course/` folder (rename it if you like) into
your assigned folder in the shared repo and push. If the repo already
has GitHub Pages enabled at the root, your course will be reachable at
`https://<org>.github.io/<repo>/<your-folder-name>/`. No other setup
needed — everything resolves relatively from wherever the folder ends
up.

## Videos

All 5 videos in the course presentation are embedded as YouTube links
(youtube.com / youtu.be URLs) — nothing is self-hosted, so there's no
video file weight in this folder and no GitHub file-size concerns.

Note: your original `.h5p` export also contained two large local
`.mp4` files (~150MB combined) inside the course package. I checked
and neither was actually referenced anywhere in the course content —
they were leftover/orphaned from an earlier edit — so I excluded them
from this build to keep the repo light. If that's unexpected (i.e. you
did intend two of the modules to use self-hosted video instead of
YouTube), let me know and I can rebuild with them included, ideally
re-hosted via YouTube instead given the file sizes.

## Local testing

Opening `index.html` directly via `file://` will NOT work — browsers
block the fetches H5P needs over the file protocol. Test locally with
any static server from inside this folder, e.g.:

```
npx http-server .
```

then open the URL it prints (e.g. `http://127.0.0.1:8080`).

## Progress tracking

Completion / unlocking is tracked with `localStorage` in the learner's
browser. It resets if they clear browser data or switch
browsers/devices — there's no backend here to persist it centrally.
Real cross-device tracking (e.g. syncing back to your existing Moodle
course) would need a small backend or xAPI endpoint, which is a bigger
step beyond a static folder like this.

## Updating content later

If you re-export either `.h5p` file from your authoring tool:

1. Rename the new export from `.h5p` to `.zip` and extract it.
2. Replace the contents of `course/` (for the course presentation) or
   `final-quiz/` (for the quiz) with the newly extracted files.
3. Leave `index.html` and `h5p-player/` untouched — they don't need to
   change unless you're adding/removing an entire content piece.
