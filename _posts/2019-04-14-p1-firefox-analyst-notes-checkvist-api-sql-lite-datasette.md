---
layout: post
title: "Checkvist Firefox analyst notes and tags -> API -> SQLite -> Datasette -> allow people to do sql queries?"
---

# Pontifications

* Using Checkvist, I'm tagging and taking Firefox desktop user feedback with notes and notes (e.g. see [Checkvist SUMO notes and tags for Firefox 66](https://checkvist.com/p/Z6DzuEp5M8FvHr87DRij1w))
* Checkvist is great but it's not a searchable database and it's not something others can query.
* So my idea is to use the Checkvist API, and some software (hah! but easy since I've done this countless times with MongoDB) and convert to JSON, store the JSON in SQLite and host the SQLite via datasette (see [How to turn a list of JSON objects into a Datasette](https://gist.github.com/simonw/eb5ad8e55d75bbc3003dd9e5d6eb438b)) in the cloud. That way other folks who don't want to work with outlines and don't know to work with outlines but do know SQL can easily query using SQL or [JSON API](https://datasette.readthedocs.io/en/stable/json_api.html).
* Previously relevant: 
    * [checkvist has a nice open api for making expandible/collapsible html from checkvist outlines](http://rolandtanglao.com/2018/11/29/p1-checkvist-api-for-collapsible-html/)
    * [cvss-to-sqlite Prequel to blog post about Datasette: Convert CSV files into a SQLite database. Browse and publish that SQLite database with Datasette](http://rolandtanglao.com/2017/12/08/p1-Convert-CSV-files-into-a-SQLite-database-prequel-to-datasette/)