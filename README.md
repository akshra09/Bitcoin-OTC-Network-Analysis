# Bitcoin-OTC-Network-Analysis

This is who-trusts-whom network of people who trade using Bitcoin on a platform called Bitcoin OTC. Since Bitcoin users are anonymous, there is a need to maintain a record of users' reputation to prevent transactions with fraudulent and risky users. Members of Bitcoin OTC rate other members in a scale of -10 (total distrust) to +10 (total trust) in steps of 1. This is the first explicit weighted signed directed network available for research.

Each line has one rating, sorted by time, with the following format:

SOURCE, TARGET, RATING, TIME where

> SOURCE: node id of source, i.e., rater
> TARGET: node id of target, i.e., ratee
> RATING: the source's rating for the target, ranging from -10 to +10 in steps of 1
> TIME: the time of the rating, measured as seconds since Epoch.
Dataset statistics

> Nodes                                5,881
>Edges                                35,592
> Range of edge weight            -10 to +10
> Percentage of positive edges           89%
