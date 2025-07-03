# Top Bittensor Accounts

The top Bittensor accounts was created by fetching the top Bittensor posts using the following settings:
```
{
    "minimumRetweets": 1,
    "minimumFavorites": 10,
    "minimumReplies": 1,
    "includeSearchTerms": True,
    "maxItems": 20000,
    "searchTerms": [
        "bittensor"
    ],
    "result_type": "popular",
    "start": "2025-05-1",
    "end": "2025-06-30",
    "sort": "Top",

}
```

The weight of each account was then calculated based on two criterea:

1. The number of posts they had in the top Bittensor posts.
2. Their total engagement on those posts.

 [Check this notebook for the exact code used.](./get_top_bittensor_accounts.ipynb)

# Top Crypto Accounts

The top crypto accounts were determined by using Kaito's leaderboard: https://yaps.kaito.ai/crypto-ai

The list of 2025-07-03 was merged with the previous list, summing weights when a user appeared in both lists.
