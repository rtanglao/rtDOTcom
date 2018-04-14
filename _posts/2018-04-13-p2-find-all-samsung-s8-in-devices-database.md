---
layout: post
title: "MongoDB query to find all Samsung S8s in the devices MongoDB collection"
---

## Pontifications

* The devices collection (see [previous post about Google Play supported devices](http://rolandtanglao.com/2018/04/09/p1-no-unique-identifier-in-google-play-supported-devices-csv-file/) ) is created as follows using [synthetic\_add\_device\_branding\_marketing\_model.rb](https://github.com/rtanglao/rt-fennec-gplay/blob/master/synthetic_add_device_branding_marketing_model.rb)  and [utf8\_supported\_devices.csv](https://github.com/rtanglao/rt-fennec-gplay/blob/master/utf_8_reviews_reviews_org.mozilla.firefox_201801.csv)  :

### How To make the devices collection
```bash
 ./synthetic_add_device_branding_marketing_model.rb utf8_supported_devices.csv
```

### How to query for Samung S8
```js
{
  "Retail Branding" : "Samsung",
  "Marketing Name" : /.*S8.*/
}
```

* The above query returns 19 rows:

```js
/* 1 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d58"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8",
  "Device" : "SC-02J",
  "Model" : "SC-02J",
  "id" : "36a69c3ac08ae64aeac8f17562b6a6cb651e91b26cf67c70078e45adf4c01c3e",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8"
}

/* 2 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d5a"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8",
  "Device" : "SCV36",
  "Model" : "SCV36",
  "id" : "da81608366c90de4694996550d75822f32b60b25617798c89c68a131a50e09c7",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8"
}

/* 3 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d5c"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8",
  "Device" : "dreamlte",
  "Model" : "SM-G950F",
  "id" : "f6ae0b8609c8b356132ed412db24e39f811a79e84a23abc599dbb8fe20049a17",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8"
}

/* 4 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d5e"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8",
  "Device" : "dreamlteks",
  "Model" : "SM-G950N",
  "id" : "7623724acfa70804ebc209cdaa9cdb280f40f74a8e19cdc0162ad2c68c06170d",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8"
}

/* 5 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d60"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8",
  "Device" : "dreamqltecan",
  "Model" : "SM-G950W",
  "id" : "d64e8803fe9049476cb4274a2005425e8e5da01e8d2616d2ad57300de1c3fa5d",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8"
}

/* 6 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d62"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8",
  "Device" : "dreamqltechn",
  "Model" : "SM-G9500",
  "id" : "e968a7e35f41500d03ff0e5e33ac4aa141fad4785402c9a3aad0534cc2b85917",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8"
}

/* 7 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d64"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8",
  "Device" : "dreamqltecmcc",
  "Model" : "SM-G9508",
  "id" : "92df1ebcbc8ee1144b8c558aae27e073f4181605b80b74b694f7daeff150f099",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8"
}

/* 8 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d66"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8",
  "Device" : "dreamqltesq",
  "Model" : "SM-G950U",
  "id" : "e780ca4a6917caad4c9f05cd61536ef32ff29c1064278503c77db0804078f108",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8"
}

/* 9 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d68"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8",
  "Device" : "dreamqlteue",
  "Model" : "SM-G950U1",
  "id" : "0633f20073a12fcbfcf4e8dc5f7772885a7429e216ac25a6c74c3f71d96371fe",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8"
}

/* 10 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d6a"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8 Active",
  "Device" : "cruiserlteatt",
  "Model" : "SM-G892A",
  "id" : "e87439102c52f67ba059e6c28fcf7ab71f4d2402ce5e57753665f9d865a1e8b9",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8 Active"
}

/* 11 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d6c"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8 Active",
  "Device" : "cruiserltesq",
  "Model" : "SM-G892U",
  "id" : "fc7a836fda56c519f6a16023c0c9c1824229a809661ed6e36dc2fcb9ec3dfe43",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8 Active"
}

/* 12 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d6e"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8+",
  "Device" : "SC-03J",
  "Model" : "SC-03J",
  "id" : "0e6afea01a7b1b422fe8288ce9b3f94221da20a88d68c70e1f040c8d89f6311e",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8+"
}

/* 13 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d70"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8+",
  "Device" : "SCV35",
  "Model" : "SCV35",
  "id" : "69fe32bb686caf9f3839e1b49a12d98106acc4762eb999b8a8df67f903f2ff4e",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8+"
}

/* 14 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d72"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8+",
  "Device" : "dream2lte",
  "Model" : "SM-G955F",
  "id" : "86901934c29f144d82bb137164338a701432c6200ea66d80c7e6d0eb9f699c67",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8+"
}

/* 15 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d74"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8+",
  "Device" : "dream2lteks",
  "Model" : "SM-G955N",
  "id" : "3728e521a686e2cc0c8f9f855d1a93d54383e99b403f907f0f00adf0782d59f7",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8+"
}

/* 16 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d76"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8+",
  "Device" : "dream2qltecan",
  "Model" : "SM-G955W",
  "id" : "c6288b00189ce68c80a3a8debefeae997aae96c1b53f78b72c42702d6ad7d4d4",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8+"
}

/* 17 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d78"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8+",
  "Device" : "dream2qltechn",
  "Model" : "SM-G9550",
  "id" : "3a7043894a443874ef824625214b18f611d80012a2becdcaa99eff94d05d22ba",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8+"
}

/* 18 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d7a"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8+",
  "Device" : "dream2qltesq",
  "Model" : "SM-G955U",
  "id" : "f63426e519ef3cb44d4968f97d765da78effaf4f2b8c9726ce7987b8f12229de",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8+"
}

/* 19 */
{
  "_id" : ObjectId("5acbc5561115a9a462b64d7c"),
  "Retail Branding" : "Samsung",
  "Marketing Name" : "Galaxy S8+",
  "Device" : "dream2qlteue",
  "Model" : "SM-G955U1",
  "id" : "6aa9b5c9fcb85dd84caf90141b2f75fc64575b59c0e6962e460fdb745169d0b7",
  "synthetic_branding_plus_marketing_name" : "Samsung Galaxy S8+"
}


```


