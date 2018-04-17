---
layout: post
title: "MongoDB upsert doesn't return updatedExisting boolean instead it returns nModified: 1 for update, 0 for insert "
---

## Pontifications

```ruby
result = 
  reviewsColl.find({ 'id' => r1["id"] }).update_one(
    r1, :upsert => true ).ai
logger.debug result.ai
```

* The above code for MongoDB 3.6 with latest ruby driver ```upsert``` doesn't return [updatedExisting](https://stackoverflow.com/questions/13955212/check-if-mongodb-upsert-did-an-insert-or-an-update/13955778) boolean instead it returns ```nModified```: ```1``` for update, ```0``` for insert



### update:

```js
documents=[{"n"=>1, "nModified"=>1, "ok"=>1.0}]"
```

### insert:

```js
documents=[{"n"=>1,
    "nModified"=>0, "upserted"=>[{"index"=>0,
    "_id"=>BSON::ObjectId('5ad4dda1e8bdbe30ca37f700')}], 
    "ok"=>1.0}]"
```



