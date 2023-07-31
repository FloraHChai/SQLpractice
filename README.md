# SQLpractice
An SQL exercise with the sample of 10,000 public Facebook posts by members of the US congress from 2017

Using the file `posts.csv` in the data folder of this repo, solve the following with With __only a single__ (which is the main challenge in this exercise) __SQL query__ through `DBI`:
- Do not consider posts with zero likes
- Compute the comment to like ratio (i.e.  comments_count / likes_count) for each post and store it in a column `clr`
- For each `screen_name`, compute a `normaliser_based_on_even_months = max(clr) - min(clr)`, i.e. the maximum minus the minimum `clr` value of posts by that `screen_name`, however, only taking into account __the posts made in even months, i.e. posts made in in February, April, June, August, October, December__ when computing `max(clr) - min(clr)` for each `screen_name`
- Set all `normaliser_based_on_even_months` that have a value of zero to NA or delete them
- Afterwards create a column `normalised_clr` which stores the `clr` of all posts from the original data frame (other than those with zero likes which were deleted in the first step) divided by the `normaliser_based_on_even_months` of the associated screen name. The only exception are posts from screen names that had a `normaliser_based_on_even_months` value of zero and were deleted/set to NA before -- for these posts just set the value in `normalised_clr` to NA as well or drop the post from the final data frame. In other words, the value of a single post/line $i$ (written by a politician $p$) in that `normalised_clr` column can be computed as: $normalised\_clr_{i,p} = clr_{i} \; / \; normaliser\_based\_on\_even\_months_{p}$ for all observations for which there is a non-NA `normaliser_based_on_even_months` 
- Keep only those rows with `normalised_clr` > 0
- Arrange the data frame according to `normalised_clr` in ascending order
- Print out only `screen_name` and `normalised_clr` for the first 10 rows, i.e. the posts with the 10 lowest `normalised_clr`
