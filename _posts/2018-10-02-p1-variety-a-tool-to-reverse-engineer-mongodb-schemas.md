---
layout: post
title: "Variety, a tool to traverse mongodb i.e. reverse engineer schemas"
---

## Pontifications

* [Variety](https://github.com/variety/variety), is an excellent tool (yay open source developers scratching an itch :-) !) to traverse mongodb i.e. reverse engineer schemas (found via Stack Overflow: [Get names of all keys in the collection](https://stackoverflow.com/questions/2298870/get-names-of-all-keys-in-the-collection) ) 
* Sample usage and output:

```bash
 mongo ff62questions --eval "var collection = 'questions', maxDepth=1, lastValue = true" variety.js
```

### Output

```
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| key                 | types                    | occurrences | percents | lastValue                                                                                                                                               |
| ------------------- | ------------------------ | ----------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _id                 | ObjectId                 |        1866 |    100.0 | 5baf13e01cb741f05c219400                                                                                                                                |
| answers             | Array                    |        1866 |    100.0 | [Array]                                                                                                                                                 |
| content             | String                   |        1866 |    100.0 | <p>Desktop computer.  Now no browser.   ????
</p>                                                                                                       |
| created             | Date                     |        1866 |    100.0 |                                                                                                                                           1537910207000 |
| creator             | Object                   |        1866 |    100.0 | [Object]                                                                                                                                                |
| id                  | Number                   |        1866 |    100.0 |                                                                                                                                                 1235288 |
| involved            | Array                    |        1866 |    100.0 | [Array]                                                                                                                                                 |
| is_archived         | Boolean                  |        1866 |    100.0 | false                                                                                                                                                   |
| is_locked           | Boolean                  |        1866 |    100.0 | false                                                                                                                                                   |
| is_solved           | Boolean                  |        1866 |    100.0 | false                                                                                                                                                   |
| is_spam             | Boolean                  |        1866 |    100.0 | false                                                                                                                                                   |
| is_taken            | Boolean                  |        1866 |    100.0 | false                                                                                                                                                   |
| last_answer         | null (152),Number (1714) |        1866 |    100.0 | [null]                                                                                                                                                  |
| locale              | String                   |        1866 |    100.0 | en-US                                                                                                                                                   |
| metadata            | Array                    |        1866 |    100.0 | [Array]                                                                                                                                                 |
| num_answers         | Number                   |        1866 |    100.0 | [Number]                                                                                                                                                |
| num_votes           | Number                   |        1866 |    100.0 |                                                                                                                                                       1 |
| num_votes_past_week | Number                   |        1866 |    100.0 |                                                                                                                                                       1 |
| product             | String                   |        1866 |    100.0 | firefox                                                                                                                                                 |
| solution            | null (1412),Number (454) |        1866 |    100.0 | [null]                                                                                                                                                  |
| solved_by           | null (1412),Object (454) |        1866 |    100.0 | [null]                                                                                                                                                  |
| tags                | Array                    |        1866 |    100.0 | [Array]                                                                                                                                                 |
| taken_by            | null                     |        1866 |    100.0 | [null]                                                                                                                                                  |
| taken_until         | null                     |        1866 |    100.0 | [null]                                                                                                                                                  |
| title               | String                   |        1866 |    100.0 | Been getting update message for a while now.  I always choose update but apparently its not updating.  Now Firefox won't come up at all.  I need help!! |
| topic               | String                   |        1866 |    100.0 | basic-browsing-firefox                                                                                                                                  |
| updated             | String                   |        1866 |    100.0 | 2018-09-25T21:16:47Z                                                                                                                                    |
| updated_by          | null (1722),Object (144) |        1866 |    100.0 | [null]                                                                                                                                                  |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```



