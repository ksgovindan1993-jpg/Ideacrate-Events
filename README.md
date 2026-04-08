# 🎡 IdeaCrate Edutainment — Live Events Dashboard

**Orange Hub · Orange Wheels · Abu Dhabi**

A fully live, real-time events scheduling dashboard. Centre teams add events, everyone sees updates instantly.

---

## 🚀 How to Deploy (15 minutes, free)

### Step 1 — Put this on GitHub Pages

1. Go to [github.com](https://github.com) → sign in or create free account
2. Click **"New repository"**
3. Name it: `ideacrate-events`
4. Set to **Public**
5. Click **"Create repository"**
6. Click **"uploading an existing file"**
7. Drag and drop `index.html` and `README.md` → click **Commit changes**
8. Go to **Settings → Pages** → Source: **Deploy from branch** → Branch: **main** → folder: **/ (root)** → Save
9. Your live URL will be: `https://YOUR-USERNAME.github.io/ideacrate-events`

---

### Step 2 — Set up Supabase (free live database)

1. Go to [supabase.com](https://supabase.com) → **Start your project** (free)
2. Create new project → region: **Middle East (Bahrain)** → wait ~2 min
3. Go to **SQL Editor** → **New query** → paste and run this SQL:

```sql
create table if not exists public.events (
  id uuid primary key default gen_random_uuid(),
  date date not null,
  center text not null,
  brand text not null check (brand in ('Hub','Wheels')),
  party_time text, kids text, package text, package_norm text,
  parties integer not null default 1, notes text,
  add_ons text, discount text, created_by text,
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);
alter table public.events enable row level security;
create policy "Public read" on public.events for select using (true);
create policy "Public insert" on public.events for insert with check (true);
create policy "Public update" on public.events for update using (true);
create policy "Public delete" on public.events for delete using (true);
alter publication supabase_realtime add table public.events;
```

4. Go to **Settings → API** → copy:
   - **Project URL** (e.g. `https://abcdefgh.supabase.co`)
   - **anon public** key (starts with `eyJ...`)

---

### Step 3 — Connect on first open

1. Open your GitHub Pages URL
2. Paste your Supabase Project URL and anon key
3. Click **"Connect & Launch"**
4. Done! 🎉

---

## 📤 Sharing with Teams

Share your GitHub Pages URL with:
- **Centre Teams** → they use **+ Add Event** to submit events live
- **HR & Marketing** → they see the live dashboard, filter by centre/brand, export reports

Every event added by any centre appears **instantly** for everyone — no refresh needed.

---

## 📥 Uploading Existing Excel Data

1. Open the dashboard
2. Click **⬆ Upload Excel**
3. Select your existing Excel file (must have sheets named like "Hub 2025", "Wheels 2026")
4. All events import to the live database immediately

---

## 📊 Export Options

| Format | What you get |
|--------|-------------|
| Excel (.xlsx) | 4 sheets: All Events, By Centre, By Package, Monthly Summary |
| PDF | Print-ready report with charts + full event listing |
| PowerPoint | 5-slide deck with brand colours and charts |

---

## 🔐 Security Note

- The Supabase anon key is designed to be public — it only allows the operations defined in your RLS policies
- All data is stored in your own Supabase account — IdeaCrate owns the data
- To restrict who can add/delete events, you can add Supabase Auth later

---

## 📁 Files

| File | Purpose |
|------|---------|
| `index.html` | The entire app — dashboard, calendar, forms, exports |
| `README.md` | This guide |

That's it. One file. No build tools. No Node.js. Just HTML.
