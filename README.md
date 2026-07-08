# Estimated Tax Payment Calculator

**🔗 Live app: https://alextarra.github.io/EstimatedTaxCalculator/**

A small, single-file web app for estimating quarterly federal and state tax
payments for self-employment income. No build step, no server, no dependencies
— just open the live link above, or `index.html` in any browser.

## What it does

- Enter estimated **federal** and **state** income-tax rates (%).
- Optionally track **Solo 401(k)** contributions (employee and/or employer, each
  toggled by a checkbox). Contributions are pre-tax for **income tax only** and
  do not reduce self-employment tax.
- Enter each quarter's **net SE profit** and the **IRS** and **state payments**
  you actually made.

## How the calculation works

Based on the 2026 Form 1040-ES SE Tax and Estimated Tax worksheets, but
deliberately simplified to lean toward overpaying. Everything accumulates by
quarter.

**Self-employment tax** (on cumulative net profit) is a flat **15.3%**:

1. SE base = net profit × 92.35%.
2. SE tax = SE base × 15.3% (12.4% Social Security + 2.9% Medicare), with **no
   wage-base cap** — this overpays slightly past the Social Security maximum
   rather than risk underpaying. The 0.9% additional Medicare tax is omitted as
   negligible.
3. Half of the SE tax is deducted before income tax.

**Income tax base** = net profit − ½ SE tax − 401(k) contributions.

- Federal owed (cumulative) = income tax + SE tax.
- State owed (cumulative) = state rate × taxable base (no SE tax).

**Recommended payment this quarter** = cumulative tax owed − payments already
made in prior quarters (federal and state computed separately). A negative
figure means you've paid ahead (shown as *overpaid*).

Because it recomputes on cumulative *actual* income each quarter (rather than
assuming four equal installments), it adapts to uneven self-employment income
and targets your full liability by each period — so you'll slightly overpay
rather than underpay.

## Usage

Open `index.html` in a browser. All entries are saved automatically in that
browser (via `localStorage`) and restored on your next visit. Use **Reset all**
to clear everything.

## Disclaimer

This is a simplified estimator. It does not model tax brackets, itemized
deductions, W-2 withholding, contribution limits, or niche credits/exclusions.
The goal is to land close — slightly over or slightly under. Consult a tax
professional for filing decisions.
