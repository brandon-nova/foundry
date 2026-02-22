# Finding Variable Disclosures Accross Funds 

> [!NOTE]
> ## Situation Overview
> The next assignment was to find what funds did or didnt disclose variable wise, and to use one year (chose 2024)

Task: 
 - For the following schema see whether it is true (1) or false (leave blank)
## ALLOCATIONS
| Field | Description |
|------|------------|
| EQ | Total Equity |
| EQ_D | Domestic Equity |
| EQ_F | Foreign Equity |
| FI | Total Fixed Income |
| FI_D | Domestic Fixed Income |
| FI_F | Foreign Fixed Income |
| CASH | Cash |
| ALT | Alternative Investments |
| p. | Page Number |

## RETURNS
| Field | Description |
|------|------------|
| EQ | Target Equity |
| EQ_D | Target Domestic Equity |
| EQ_F | Target Foreign Equity |
| FI | Target Fixed Income |
| FI_D | Target Domestic Fixed Income |
| FI_F | Target Foreign Fixed Income |
| TgtAlloc | Target Allocation |
| p. | Page Number |

## BENCHMARKS
| Field | Description |
|------|------------|
| EQ | Equity Active Difference |
| EQ_D | Domestic Equity Active Difference |
| EQ_F | Foreign Equity Active Difference |
| FI | Fixed Income Active Difference |
| FI_D | Domestic FI Active Difference |
| FI_F | Foreign FI Active Difference |
| %Active | Total Active Difference |
| p. | Page Number |


# Thought Process 

At first I was going to try to build a pipeline to find all the variables statuses at once. 
 - Actually I still can why not, sinc eit will have page numbers reagrdless/ 