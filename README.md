# Rowing plan

A private 5k training plan for a club rower. It is rebuilt every morning from the team's erg sheet, so each new
test moves the zones, milestones and plan without anyone touching the code.

The page is public, but it holds no data. Everything about the athlete is in `data.enc`, encrypted with
AES-256-GCM using a key derived from a passphrase (PBKDF2-SHA256, 250 000 iterations), and the page decrypts it
in the browser. Names and body mass never enter it.

- **Engine:** [`research/training/`](https://github.com/josh-porg/CoxswainSimulator_V_0/tree/main/research/training)
  in CoxswainSimulator_V_0. It holds the plan generator, the squad yardstick, the site builder, the page shell, and
  the methods and evidence.
- **This repository:** `config.json` (team week, free days, volume settings, key races, start, target; no
  personal data) and the workflow.
- **Secrets:** `ERG_SHEET_ID`, `ATHLETE_NAME` and `SITE_PASSPHRASE`.

To change the plan, edit `config.json`, for example `available_days`, `own_aerobic_minutes_start` or
`fall_key_race_md`. Then run the workflow from the Actions tab, or wait for the morning rebuild.

**Stopping it:**

```bash
gh workflow disable update.yml -R josh-porg/rowing-plan       # stop the daily rebuilds
gh api -X DELETE repos/josh-porg/rowing-plan/pages            # take the page down
```

This is not medical advice. Warning signs listed on the page (missed periods, bone or rib pain, repeated
illness) mean seeing a doctor.
