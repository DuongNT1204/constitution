# Bittensor Posts Quality Analysis

## Data Collection Pipeline
Using two AI services to analyze Bittensor-related social posts:
- **Desearch.ai**: Fetches recent posts from X (Twitter)
- **Nineteen.ai**: Evaluates content quality

Link to jpynb: [Get_top_post](https://github.com/NuanceNetwork/constitution/blob/new-list-august/verified_users/twitt)

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
Posts are fetched using the Desearch.ai API with the following parameters for each verified user:
```python
params = {
    "query": "Bittensor",                  # Search keyword
    "user": username,                      # Target account
    "sort": "Latest",                      # Sort by most recent
    "start_date": start_date.strftime("%Y-%m-%d"),  # Start of 7-day window
    "end_date": end_date.strftime("%Y-%m-%d"),      # End of 7-day window
    "count": max_posts                     # Max posts per user
}
```
#### Configuration
```python
CONFIG = {
    "days_back": 7,                        # Last 7 days
    "max_posts_per_user": 20,              # Cap per user
    "sn19_delay": 5.0,                     # Delay for Nineteen.ai requests
    "sn22_delay": 1.0,                     # Delay for Desearch.ai requests
    "sn19_model": "deepseek-ai/DeepSeek-R1-0528-Qwen3-8B",  # Model for scoring
    "use_full_dataset": True               # Use all verified accounts
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