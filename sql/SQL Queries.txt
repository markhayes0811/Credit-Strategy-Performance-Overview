SQL Queries - ** These were run and added is MS Access

- ApprovalRate_Overall

SELECT
    COUNT(*) AS total_apps,
    AVG(approved_AB) AS approval_rate
FROM
    credit_applications;

---

- AverageLoanAmount_ByStrategy

SELECT
    strategy_group,
    AVG(loan_amount) AS avg_loan_amount
FROM
    credit_applications
GROUP BY
    strategy_group;

---

- AverageLoanAmount_Overall

SELECT
    AVG(loan_amount) AS avg_loan_amount
FROM
    credit_applications;

---

- DefaultRate_ApprovedOnly

SELECT
    AVG(default_12m) AS default_rate_on_approved
FROM
    credit_applications
WHERE
    approved_AB = 1;

---

- ExpectedLoss_Portfolio

SELECT
    SUM(expected_loss) AS total_expected_loss,
    AVG(expected_loss) AS avg_expected_loss_per_loan
FROM
    credit_applications;

---

- PD Risk Segmentation

SELECT
    IIF(
        pd_model < 0.05,
        '0–5%',
        IIF(
            pd_model < 0.10,
            '5–10%',
            IIF(
                pd_model < 0.20,
                '10–20%',
                IIF(pd_model < 0.30, '20–30%', '30%+')
            )
        )
    ) AS pd_band,
    COUNT(*) AS loans,
    AVG(default_12m) AS realized_default_rate,
    AVG(profit) AS avg_profit
FROM
    credit_applications
WHERE
    approved_AB = 1
GROUP BY
    IIF(
        pd_model < 0.05,
        '0–5%',
        IIF(
            pd_model < 0.10,
            '5–10%',
            IIF(
                pd_model < 0.20,
                '10–20%',
                IIF(pd_model < 0.30, '20–30%', '30%+')
            )
        )
    );

---

- PDBands_Approved

SELECT
    IIF(
        pd_model < 0.05,
        '0–5%',
        IIF(
            pd_model < 0.10,
            '5–10%',
            IIF(
                pd_model < 0.20,
                '10–20%',
                IIF(pd_model < 0.30, '20–30%', '30%+')
            )
        )
    ) AS pd_band,
    COUNT(*) AS loans,
    AVG(default_12m) AS realized_default_rate,
    AVG(profit) AS avg_profit_per_loan,
    SUM(profit) AS total_profit
FROM
    credit_applications
WHERE
    approved_AB = 1
GROUP BY
    IIF(
        pd_model < 0.05,
        '0–5%',
        IIF(
            pd_model < 0.10,
            '5–10%',
            IIF(
                pd_model < 0.20,
                '10–20%',
                IIF(pd_model < 0.30, '20–30%', '30%+')
            )
        )
    );

---

- Portfolio Metrics Query

SELECT
    credit_applications.strategy_group,
    Count(*) AS total_apps,
    Avg(credit_applications.approved_AB) AS approval_rate,
    Avg(IIf(approved_AB = 1, default_12m, NULL)) AS default_rate_approved,
    Sum(IIf(approved_AB = 1, profit, 0)) AS total_profit,
    Avg(IIf(approved_AB = 1, profit, NULL)) AS avg_profit_per_approved
FROM
    credit_applications
GROUP BY
    credit_applications.strategy_group;

---

- Profit_ByStrategy

SELECT
    strategy_group,
    COUNT(*) AS total_apps,
    AVG(approved_AB) AS approval_rate,
    AVG(IIF(approved_AB = 1, default_12m, NULL)) AS default_rate_approved,
    AVG(loan_amount) AS avg_loan_amount,
    SUM(profit) AS total_profit,
    AVG(IIF(approved_AB = 1, profit, NULL)) AS avg_profit_per_approved
FROM
    credit_applications
GROUP BY
    strategy_group;