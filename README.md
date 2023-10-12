# Harry-Potter-Books
Turn a Harry Potter Book into a Knowledge Graph


Most likely, you have already seen the Game of Thrones network created by Andrew Beveridge.
Andrew constructed a co-occurrence network of book characters. If two characters appear within some distance of text between each other, we can assume that they are somehow related or they interact in the book.
I decided to create a similar project but choose a popular book with no known (at least to me) network extraction. So, the project to extract a network of characters from the Harry Potter and the Philosopher’s Stone book was born.
I did a lot of experiments to decide the best way to go about it. I’ve tried most of the open-source named entity recognition models to compare which worked best, but in the end, I decided that none were good enough.
Luckily for us, the Harry Potter fandom page contains a list of characters in the first book. We also know in which chapter they first appeared, which will help us even further disambiguate the characters.
Armed with this knowledge, we will use SpaCy’s rule-based matcher to find all mentions of a character. Once we have found all the occurrences of entities, the only thing left is to define the co-occurrence
metric and store the results in Neo4j. We will use the same co-occurrence threshold as was used in the Game of Thrones extraction. If two characters appear within 14 words of each other, we will assume they have 
interacted somehow and store the number of those interactions as the relationship weight.

Agenda :
==========
1. Scrape Harry Potter fandom page
2. Preprocess book text (Co-reference resolution)
3. Entity recognition with SpaCy’s rule-based matching
4. Infer relationships between characters
5. Store results to Neo4j graph database
6. I have prepared a Google Colab notebook if you want to follow along.

Harry Potter Fandom Page Scraping :
====================================
We will use Selenium for web scraping. As mentioned, we will begin by scraping the characters in the Harry Potter and the Philosopher’s Stone book. The list of characters by chapter is available under the CC-BY-SA 
license, so we don’t have to worry about any copyright infringement.
