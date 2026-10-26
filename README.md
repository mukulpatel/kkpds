# Dehgam Shahar Sanatan Samaj website (test copy)

Static website built with React + TypeScript + Vite. Gujarati is the default language, with an English toggle. There is no server, database or login, so it can be hosted for free.

## 1. Change your settings first

Edit **`src/config.ts`**:

```ts
export const PUBLIC_URL = 'https://yourdomain.org';          // your website address
export const FORM_EMAIL = 'your-community-email@gmail.com';  // receives Contact + Suggestion forms
```

The first time someone submits a form, FormSubmit sends an activation email to `FORM_EMAIL`. Click the link in it (check Spam) so later messages are delivered.

## 2. Run it on your computer (optional)

You need Node.js 22 or newer.

```bash
npm install
npm run dev        # opens at http://127.0.0.1:5180
npm run build      # production files go to dist/
npm run preview    # preview the production build at http://127.0.0.1:4180
```

## 3. Put it on GitHub

1. Create a new **private** repository on GitHub, for example `samaj-website`.
2. Upload all files from this folder. (`node_modules/` and `dist/` are excluded by `.gitignore`.)

```bash
git init
git add .
git commit -m "Initial website"
git branch -M main
git remote add origin https://github.com/<your-username>/samaj-website.git
git push -u origin main
```

## 4. Host it free on Cloudflare Pages with your own domain

1. Log in at dash.cloudflare.com, then go to **Workers & Pages → Create → Pages → Connect to Git**.
2. Pick the repository and set:
   - Framework preset: **Vite** (or none)
   - Build command: `npm run build`
   - Build output directory: `dist`
   - Environment variable: `NODE_VERSION` = `22`
3. Click **Save and Deploy**. You get a free `*.pages.dev` address within a minute or two.
4. Open the project's **Custom domains** tab, add `yourdomain.org` (and `www.yourdomain.org`). If the domain's DNS is on Cloudflare, records and HTTPS are created automatically.
5. From now on, every push to `main` republishes the site automatically.

**Alternative: GitHub Pages.** This needs a public repository on the free plan. Under **Settings → Pages**, choose **GitHub Actions** and use a standard Vite Pages workflow. Cloudflare Pages is recommended because the repository can stay private.

## Where to edit content

Every bilingual text uses `bi('ગુજરાતી', 'English')`. Edit both.

| Content | File |
| --- | --- |
| Website address and form email | `src/config.ts` |
| Name, logo, contact, statistics, menu, UI text | `src/data/site.ts` |
| Committee (Karobari Samiti) | `src/data/committee.ts` |
| About, objectives, membership rules, privacy, disclaimer | `src/data/content.ts` |
| Events, notices, gallery albums, documents | `src/data/publications.ts` |
| Form fields and labels | `src/data/forms.ts` |
| Colours and layout | `src/styles.css` (`--maroon`, `--saffron`, `--cream`, …) |
| Logo | `public/images/logo.png` |

Photos go in `public/images/`, and documents (PDF/HTML) in `public/documents/`.

## Important: keep private data out

Everything in this project is **public** once deployed: every file under `public/` and every text in `src/`.

- Never add member lists, phone numbers, spreadsheets, ID documents or bank details.
- Show committee phone numbers only with each person's consent (`publicPhone: true`).
- The Member directory page deliberately shows "Coming soon". A private directory needs a proper login system and server, not a static site.

## Tests (optional)

```bash
npx playwright install chromium
npm test
```

These check every page in both languages on desktop and mobile, the forms, filters and gallery.

## What changed from the original

- Started fresh with no Git history, so the older public member-directory PDF in the original repository's history is not carried over.
- Removed the unused old password server (`server/`), the member-directory generation scripts, and Windows-only launch files.
- Moved the website address and form email into `src/config.ts`.
- Fixed the Gujarati "Loading" text that showed as `???`, and made logo/favicon links work on any domain.
