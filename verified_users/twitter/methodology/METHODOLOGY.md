# Bittensor Posts Quality Analysis

## Data Collection Pipeline
Using two AI services to analyze Bittensor-related social posts:
- **Desearch.ai**: Fetches recent posts from X (Twitter)
- **Nineteen.ai**: Evaluates content quality

## Data Sources

### Target Accounts
The script fetches verified Bittensor community accounts from:
```
https://raw.githubusercontent.com/NuanceNetwork/constitution/main/verified_users/twitter/bittensor_target_accounts_august_followers.csv
```
This CSV contains:
- Active community members
- Sorted by followers on previous list count

## How It Works

### Step 1: Data Collection
Using Desearch.ai API with these parameters:
```python
{
    "days_back": 7,                # Last 7 days of posts
    "max_posts_per_user": 20,      # Cap per user
    "use_full_dataset": True       # Uses full verified accounts list
}
```

### Step 2: Quality Scoring
Each post is evaluated by Nineteen.ai on 3 metrics (1-10 scale):

| Metric | Description |
|--------|-------------|
| Nuanced | How well it shows depth and sophisticated understanding |
| Valuable | Contribution to community knowledge and discourse |
| Unbiased | Objectivity and fairness of content |

Final score = Average of all 3 metrics

### Step 3: Output Generation
The script produces 3 CSV files:
1. `posts_raw_{timestamp}.csv`: Raw collected posts
2. `posts_evaluated_{timestamp}.csv`: Posts with quality scores  
3. `top_posts_{timestamp}.csv`: Highest scoring content

## Setup Requirements

### Dependencies
```python
desearch-py
requests  
pandas
tenacity
tqdm
python-dateutil
openai
```

### API Keys Needed
- Desearch.ai API key
- Nineteen.ai API key

## Usage
1. Set API keys in notebook
2. Run all cells
3. Check output files for results

Note: This analysis script is used to get the top Bittensor posts from the last 7 days.