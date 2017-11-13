---
layout: post
title: Curly Bracket inconsistency in Mongod DB aggregation?!?
---
Why is a curly bracket required before the "$divide” in the following? Is it because of the square bracket? Is it because of a mongodb bug?

``` ruby
red_green_blue_divide_by_100_and_pow = { 
	'$project' =>
	{
		"red_pow" => { "$pow" =>
		[{"$divide" => ["$top_colour.red", 255.0]}, 2.2]},
		"green_pow" => { "$pow" => [
			{"$divide" => ["$top_colour.green", 255.0]}, 2.2]},
		"blue_pow" => { "$pow" => [
			{"$divide" => ["$top_colour.blue", 255.0]}, 2.2]}
      }
    }
```

But not before the "$pow" in the following:

``` ruby
red_green_blue_float_avg = { 
	'$project' =>
  {
		"_id" => 0,
    "red_float_avg" => {
		  "$multiply" =>
	      [255.0, "$pow" => ["$red_linear_avg", 1.0/2.2]]},
    "green_float_avg" => {
      "$multiply" =>
	      [255.0, "$pow" => ["$green_linear_avg", 1.0/2.2]]},
    "blue_float_avg" => {
		  "$multiply" =>
	      [255.0, "$pow" => ["$blue_linear_avg", 1.0/2.2]]}
  }
    }
```
                                                                                                                                                                          