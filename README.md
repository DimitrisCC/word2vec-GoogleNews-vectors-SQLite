# word2vec-GoogleNews-vectors-SQLite
SQLite version of mmihaltz's word2vec trained on GoogleNews https://github.com/mmihaltz/word2vec-GoogleNews-vectors
compressed.

The schema is an `Embeddings` table with columns `word` as TEXT and `embedding` as TEXT as well in a list format.

A general selection example in Python 3.
----------------------------
``` Python
# words is a list of the vocabulary
def select(words=None):
    con = sql.connect('~/word2vec.db')
    with con:
        cur = con.cursor()
        query = "SELECT word, embedding FROM Embeddings"
        if words is not None:
            query += " WHERE word IN %s " % str(tuple(words))
        cur.execute(query)
        data = cur.fetchall()
        model = {}
        for row in data:
            model[row[0]] = list(map(float, row[1].split(',')))
        return model
```
