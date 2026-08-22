# I Made Wisnu Kusuma Putra — Portfolio

Personal portfolio and two interactive prototypes built to demonstrate backend/full-stack
engineering approach for internal enterprise systems (condominium operations and banking
credit decisioning).

**Live site:** `https://madewithwisnu.github.io/wisnu-portfolio/`

## Structure

```
portfolio/
├── index.html                     # Main portfolio (profile, skills, experience, projects)
├── condominium-demo.html          # Demo 1 — Condominium Management System
├── credit-simulation-demo.html    # Demo 2 — Credit Simulation Engine
└── README.md
```

## Tech stack (prototype layer)

Plain HTML, CSS, and vanilla JavaScript — no build step, no dependencies. State is held
in-memory in the browser, so it's meant for demonstration and UX/workflow review, not as a
persisted production system.

**Proposed production stack** (per each demo's notes): ASP.NET Core Web API + Blazor for the
front end, C# services for business/calculation logic, SQL Server for persistence, and
claims-based RBAC for role separation.

## Run locally

No server required — just open the file in a browser:

```bash
git clone https://github.com/madewithwisnu/wisnu-portfolio.git
cd <repo-name>
open index.html     # macOS
# or double-click index.html on Windows/Linux
```

Or serve it locally if you prefer a URL instead of a `file://` path:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## Demo 1 — Condominium Management System

A prototype internal ops tool for a residential property ("Grand Meridian Residences"),
covering resident/unit records, maintenance fee collection, and facility bookings.

**Role simulated:** Property / Building Management Staff — the person who manages resident
records, tracks who has paid maintenance fees, and approves facility usage. There is no
login step in the prototype; every visitor sees the staff view.

### How to use it

1. Open `condominium-demo.html`. The top stat row shows a live snapshot: total units,
   occupied units, fees collected this month, and today's facility bookings.
2. **Residents & Units tab**
   - Click **+ Add Resident**, fill in unit number, name, owner/tenant type, and phone,
     then **Save**. A new resident is added to the registry, and a matching "due" fee
     record is auto-created in the Payments tab — mirroring how onboarding a resident
     should also open their billing record.
   - Click **Remove** on any row to take a resident off the registry (e.g. move-out).
3. **Maintenance Fees tab**
   - Each row is one unit's fee status for the period. Click the status pill
     (`paid` / `due` / `overdue`) to cycle it — this simulates marking a payment as
     received or flagging it overdue, the way staff would update a ledger.
4. **Facility Bookings tab**
   - Click **+ New Booking**, choose a facility (Function Hall, Pool, BBQ Pit, Gym, Tennis
     Court), enter the requesting unit, date, and time slot, then **Book**.
   - Click **Cancel** to remove a booking, e.g. if a resident withdraws a request.
5. All changes recalculate the stat row instantly — there's no save/submit delay, since
   the point of the prototype is to validate the workflow, not the persistence layer.

### What it's meant to show

- Schema thinking: Units, Residents, Ledger (fees), and Bookings as separate but related
  entities.
- A staff-facing operational dashboard, the kind of "internal web" tooling referenced in
  the Advancer job description.
- Where the real implementation would plug in: fee status changes and bookings would call
  an ASP.NET Core API, persist to SQL Server, and be gated by role (e.g. only staff can
  mark fees as paid; residents would only see their own unit).

---

## Demo 2 — Credit Simulation Engine

A prototype loan/credit simulator that mirrors the shape of the Credit Decision Engine and
Financial Simulation System work described in the Experience section — configurable loan
terms, a live amortization schedule, and a simple decisioning rule.

**Role simulated:** Loan/Credit Officer — the person who enters an applicant's loan
request and financial profile to get an instant read on repayment terms and approval risk,
before it goes to a full underwriting process.

### How to use it

1. Open `credit-simulation-demo.html`.
2. Fill in the **Loan Parameters** panel:
   - **Principal** — the loan amount requested.
   - **Tenor** — repayment period in months.
   - **Annual interest rate** — as a percentage.
   - **Interest scheme** — toggle between **Flat** (interest calculated on the original
     principal for the full tenor) and **Effective** (interest calculated on the
     declining balance each month — a standard amortizing loan).
   - **Applicant monthly income** and **Existing monthly debt** — used for the
     affordability check.
3. Click **Run Simulation**.
4. Read the results:
   - **Monthly Installment / Total Interest / Total Repayment** — the headline numbers
     for this loan configuration.
   - **Decision banner** — a debt-to-income (DTI) based verdict:
     - **Approve** — DTI ≤ 35%
     - **Manual Review** — DTI between 35% and 50%
     - **Reject** — DTI > 50%
     (DTI = (existing debt + new installment) ÷ monthly income.)
   - **Amortization Schedule** — a full month-by-month breakdown of installment,
     principal portion, interest portion, and remaining balance, scrollable if the tenor
     is long.
5. Change any input and re-run to compare scenarios — e.g. how extending tenor from 24 to
   36 months changes the monthly installment and the approval outcome.

### What it's meant to show

- Two real amortization methods implemented correctly (flat vs. effective/reducing
  balance), not just a placeholder formula.
- A simple, transparent, rule-based decisioning layer — the same category of logic behind
  the BNI/Mitsui credit and financial simulation work, scaled down to something reviewable
  in a browser.
- Where the real implementation would plug in: the amortization and DTI logic would move
  into C# services behind an ASP.NET Core API, results persisted to SQL Server per
  application, and the decision thresholds made configurable per lending policy.

---

## Contact

- Email: wisnukusuma99@gmail.com
- Phone: +62 878 8203 0450
- LinkedIn: [linkedin.com/in/mdwisnukusuma](https://linkedin.com/in/mdwisnukusuma)
