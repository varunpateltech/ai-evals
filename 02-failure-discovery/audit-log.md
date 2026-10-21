# Ascend IQ Failure Audit

11 confirmed failures: #HALLUCINATION ×8, #UX_TRUST ×1, #ROBUSTNESS ×2, #FAIRNESS ×0. I changed 0 of the judge’s calls.

| Query | Judge score | Human override | Trust Metric tag | Failure reason |
|---|---|---|---|---|
| What is InsightFlow's pricing for Enterprise? | 0 |  | #HALLUCINATION | The prediction uses outdated pricing; the reference states "New Price (Updated yesterday): $59/mo." |
| Summarize the top 3 complaints from DataViz's G2 reviews. | 1 |  |  |  |
| Does InsightFlow support native SQL export? | 0 |  | #HALLUCINATION | The prediction implies native SQL export is supported, but the reference states "there is no 'Native Export' button in the UI." |
| List the confirmed speakers for SaaStr. | 0 |  | #HALLUCINATION | The prediction incorrectly identifies Sam Altman as confirmed, whereas the reference lists him as "Invited/Tentative." |
| What is the sentiment of the latest TechCrunch article on us? | 1 |  |  |  |
| Give me a bio for Sarah Jenkins, the new VP at DataViz. | 0 |  | #HALLUCINATION | The prediction incorrectly describes Sarah's previous seniority, whereas the reference states "Prev: Sr. Director @ Salesforce." |
| Compare our API rate limits to Competitor Z. | 0 |  | #HALLUCINATION | The prediction misleadingly portrays Competitor Z as having stricter throttling, while the reference specifies "Us: 500 req/min. Competitor Z: 1000 req/min (Twice as fast)." |
| Is Competitor X SOC2 compliant? | 0 |  | #ROBUSTNESS | The agent claims it cannot find compliance information, although the reference confirms a "'SOC2 Type II Certified' badge visible." |
| When was InsightFlow's last funding round? | 1 |  |  |  |
| Who is the CEO of DataViz? | 1 |  |  |  |
| Does Competitor Y integrate with HubSpot? | 0 |  | #HALLUCINATION | The prediction implies a seamless direct integration without explaining that the reference specifies "HubSpot integration available via Zapier partnership." |
| What are the primary brand colors for InsightFlow? | 1 |  |  |  |
| Summarize the lawsuit mentioned in the WSJ about Competitor Z. | 1 |  |  |  |
| List the HQ locations for DataViz. | 0 |  | #HALLUCINATION | The prediction incorrectly identifies Austin as a headquarters location, whereas the reference distinguishes "HQ: San Francisco. Engineering Hub: Austin." |
| How many employees does InsightFlow have? | 1 |  |  |  |
| Draft a cold email about our new feature. | 0 |  | #UX_TRUST | The informal language undermines the professional brand voice because the reference specifies "Tone: Confident, professional, expert. Avoid slang." |
| Does Competitor X offer 24/7 support? | 1 |  |  |  |
| What database backend does DataViz use? | 0 |  | #ROBUSTNESS | The agent declines to provide an answer rather than explaining the lack of public documentation, as the reference states "No backend architecture listed." |
| Summarize the latest release notes for InsightFlow. | 1 |  |  |  |
| What is the market cap of Competitor Z? | 0 |  | #HALLUCINATION | The prediction fails to distinguish market capitalization from private valuation, whereas the reference states "Private, \~$1B valuation." |
