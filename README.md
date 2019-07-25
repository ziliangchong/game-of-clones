# Game of Clones: telling rival Game of Thrones subreddits apart

Can Natural Language Processing combined with predictive models accurately distinguish between posts on <a href='https://www.reddit.com/r/pureasoiaf/'>`r/pureasoiaf/`</a> and <a href='https://www.reddit.com/r/freefolk/'>`r/freefolk/`</a>?

### ...Game of what? (Skip if you are familiar with GOT)

Game of Thrones, as in the multi-season, award-winning, fantasy <a href='https://www.hbo.com/game-of-thrones'>HBO series</a> based on the "A Song of Ice and Fire" novels by <a href='http://www.georgerrmartin.com'>George R. R. Martin</a>. Over 73 episodes of clashing armies, medieval politics, and fire-spewing dragons, noble houses with generations of enmity duke it out for the right to sit on the iron throne - the metaphorical and literal seat of power. Meanwhile, a large band of so-called Wildlings live outside the jurisdiction of the warring kingdoms, where the self-proclaimed freefolk contend with an ancient evil that will eventually threaten the existence of all living beings...  

### OK, what have we got?

Right, back to your regular programming. We will look at two main subreddits dedicated to the TV series and books. <a href='https://www.reddit.com/r/pureasoiaf/'>`r/pureasoiaf/`</a> (a.k.a. Pure A Song of Ice and Fire) is dedicated solely to the novels and "does not allow content from the popular HBO series. Game of Thrones". As the TV series' plot development has overtaken that of the books and revealed the story's conclusion, book fans in `pureasoiaf` are exacting in ensuring they aren't contaminated by spoilers from the outside world.

<a href='https://www.reddit.com/r/freefolk/'>`r/freefolk/`</a> live outside the jurisdiction of spoiler rules and declares that "we believe people are mature enough to decide for themselves what content to view".

### Goal

Let's see if a machine can identify the purists among the wider fan community.

## The process:
- Data gathering from subreddits using Reddit API.
- Data cleaning and exploration.
  - Get rid of capitalization, punctuation, and stop words.
  - Find most common words in each subreddit.
- Modelling
  - Using loops, test every combination of selected vectorizers (`CountVectorizer`, `TfidfVectorizer`) and models (`MultiNomialNB`, `KNeighborsClassifier`, `RandomForestClassifier`, `LogisticRegression`).
- Logistic model analysis
  - Although `MultiNomialNB` performed slightly better, `LogisticRegression` was chosen for its interpretability. We were able to analyze the words that contributed most to the model predicting either `pureasoiaf` or `freefolk`.

## Conclusion

### Findings

- After experimenting with several models, we achieved 84.5% accuracy in predicting which subreddit a post came from using the `LogisticRegression`-`TfidfVectorizer` combination.
- This model was chosen for its interpretability and we found that the model was intelligent enough to pick certain words that had high predictive power even though they are not the most common words in their subreddits.

### Limitations

- Many of the posts, especially in `freefolk`, were memes and did not contain text in the post's body for analysis. We could rely only on the titles of the posts.

### Further exploration

- Move beyond the Reddit API, which allows just 1,000 posts, and collect larger datasets to see if that can improve performance.
- Compare more Game of Thrones-related subreddits to see if results hold up across different fanbases.
- Collect another 1,000 posts each from subreddits during a different time period to see if results differ. This is particularly the case for `freefolk`, which was very much influenced by the San Diego Comic Convention and Emmy Awards nomination during the time of data collection.
