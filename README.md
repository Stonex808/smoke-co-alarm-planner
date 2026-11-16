# Smoke & CO Alarm Expiry Planner

B.A.N.K. standalone site (candidate c32-smoke-co-alarm-expiry, score 17/25). Not part of the off-grid hub, so there's no hub link.
Planned URL: https://smoke-co-alarm-planner.vercel.app/

A static single page (`index.html`, inline CSS/JS, no build step, no external fonts or scripts). It's a household log for every smoke, CO, and combo alarm in a home:

- Add rows: room, type (smoke / CO / combo), brand (Kidde / First Alert / Other / Unknown), and either a manufacture date (month optional; if missing, January is assumed, the earlier and safer guess), a replace-by date printed on the label, or "no readable date".
- Replace-by = manufacture + service life. The defaults are smoke 10 yr, combo 10 yr, CO 7 yr, and the user can pick 5 / 7 / 10. A replace-by date printed on the label is used as-is.
- Status: Expired (the replace-by month has been reached or passed), Replace within 12 mo, OK, Unknown age (flagged for replacement, following Kidde's "if in doubt, replace" advice).
- The list is saved in localStorage (`bank-smoke-co-log-v1`; household name `bank-smoke-co-house-v1`).
- Print button plus a print stylesheet: a household sheet with a 12-month test-log grid.
- An `.ics` file is built client-side: one all-day event per alarm on its replace-by date (overdue or undated alarms get an event for tomorrow), an optional yearly date-check (RRULE YEARLY) and an optional monthly test reminder (RRULE MONTHLY). Lines are CRLF, folded at 75 octets, and text is escaped.
- Brand date-code ciphers are not decoded on purpose. The unit's label always wins.

## Sources (fetched Nov 8, 2026)
- First Alert: https://support.firstalert.com/s/article/Are-my-smoke-alarms-still-good (smoke/heat 10 yr from manufacture; CO/gas 5–7 yr by model; date on the back)
- First Alert: https://support.firstalert.com/s/article/Smoke-or-CO-Alarm-Expiration-Dates (the printed date is the manufacture date, not an expiration date)
- Kidde: https://www.kidde.com/support/smoke-alarms/alarms-replacement-time (smoke/heat 10 yr per NFPA; CO and combo 7–10 yr by model; replace if in doubt)
- Kidde: https://www.kidde.com/support/smoke-alarms/manufacture-date-location (date code on the back label)
- NFPA: https://www.nfpa.org/education-and-research/home-fire-safety/smoke-alarms (test monthly; replace 10 yr after manufacture)

## Affiliate
Amazon search links use `tag=wellpumpplann-20` and `rel="sponsored nofollow noopener"`. The page shows no prices or ratings. The disclosure appears near the top and in the footer.

## Design tokens
paper #f7f6f1 · sheet #fffefa · ink #1f2420 · tab navy #1d3557 · crimson #9f1239 · mustard #8a6a00 · rules #dcd8cc / #c9d4e3
Headings: Palatino Linotype, Palatino, Book Antiqua, serif. Body: Franklin Gothic Book, Libre Franklin, Helvetica Neue, Helvetica, Arial.
Look: a ring-binder safety log, with navy index tabs, punched-hole margin and red margin rule on desktop, and ruled inventory rows that stack into labelled log cards on mobile.

## Deploy
Vercel static (upload the folder). Remember to add the URL to the Amazon Associates website list.
