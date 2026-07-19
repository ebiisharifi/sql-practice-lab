# SQL Practice Lab

156 runnable SQL interview questions in a single HTML file. No signup, no server, no install. Open the page, type a query, hit Run, check your answer against a verified solution. Everything executes right in your browser.

I built this while preparing for data analyst interviews. Most SQL practice sites either lock the good questions behind a paywall or make you read solutions without ever typing anything. I wanted something where I could actually write every query against real tables, get told whether my result set matches, and keep my progress between sessions. So I made it, and I figured other people prepping for the same kind of interviews might get some use out of it.

Live version: https://ebiiisharifi.github.io/sql-practice-lab/

Or just download index.html and open it. That is the whole app.

## What is inside

- 156 questions, every one runnable, with a hint, a full solution, and automatic answer checking
- 24 topic groups, from basic filtering up to gaps-and-islands, relational division, and recursive CTEs
- A "Top 100" set covering the classic patterns that show up in almost every SQL interview (marked with a teal 100 badge)
- A set of questions reported from real bank data-analyst interviews, plus a servicing and risk analytics group with the kind of retention, exposure, and payment-gap questions banks actually ask
- 15 tables across two schema worlds: a banking one (customers, accounts, transactions, payments, clicks, applications) and a company one (employees, departments, products, orders, order_items, salary_history, logins, bookings, employees_archive)
- A free-form Sandbox tab, a Database tab where you can browse every table, a cheat sheet, and a search box that filters all 156 questions as you type

The data is hand-built so the edge cases are actually in there. There is a customer who ordered in January but not February, a five-day login streak, duplicate rows waiting to be found, a department with zero employees, an archive table that disagrees with the live table in exactly four rows, and so on. If a question asks for something, the data contains it.

## Topic breakdown

Warm-up and core: Basics and filtering, Aggregates, GROUP BY and HAVING, Joins, CASE WHEN, Dates, Subqueries and CTEs, Window functions, Core interview patterns, Bonus drills, Reported real-interview questions, Servicing and risk analytics (56 questions total).

Top 100 classics: Ranking and Top-N (12), Window functions (12), Anti-joins and missing data (11), Joins and self-joins (10), Aggregation and HAVING (10), Dates and time (9), Membership and set logic (8), Above-average and subqueries (7), Conditional aggregation and pivots (6), Gaps islands and streaks (5), Duplicates and data quality (5), Advanced and misc (5).

## How answer checking works

When you hit "Check answer" the app runs your query and the reference solution, then compares the result sets. Column order and row order are ignored unless the question explicitly asks for ordered output, in which case order counts. Solve a question and it gets a green dot in the sidebar. Your typed answers and solved list are saved in localStorage, so you can close the tab and come back later. There is a Reset button in the header if you want a clean slate.

## Tech notes

The engine is sql.js (SQLite compiled to WebAssembly) with a MySQL compatibility layer on top, since MySQL is what most analyst interviews use. YEAR, MONTH, QUARTER, DATE_FORMAT, DATEDIFF, DAYNAME and friends are registered as custom functions, and DATE_ADD / DATE_SUB with INTERVAL syntax get rewritten before execution. CURDATE() is pinned to a fixed date so date-relative questions always give the same answer.

Every solution was machine-verified against the shipped data: 156 out of 156 execute and return non-empty results. One honest quirk I hit while building this: LEFT and RIGHT cannot be called as string functions here because the parser treats them as reserved words (think LEFT JOIN). The affected question teaches SUBSTR instead, which is the portable answer anyway.

Big cartesian joins are capped with a row limit and a time budget, so a forgotten join condition gives you a friendly warning instead of freezing the tab.

## Running it locally

Clone the repo or grab index.html, then open it in any modern browser. The only network request is the sql.js library from a CDN, so you need to be online the first time.

## Found a problem?

If a solution looks wrong or a question reads badly, open an issue. I would rather fix it than have someone practice the wrong pattern.

## License

MIT. Use it, fork it, put it in your study group, whatever helps.

Built by Ebrahim Sharifi - https://www.linkedin.com/in/ebrahim-sharifi-ph-d-p-eng-2147b781/
