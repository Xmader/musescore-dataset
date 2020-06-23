
# musescore-dataset

The unofficial dataset of all music sheets and users on musescore.com, dedicated to big data analytics / data science / machine learning.

> All data is collected by iterating through [musecore.com's *public* API](https://developers.musescore.com/).

> The `jsonl` files are in the [Newline-delimited JSON](https://en.wikipedia.org/wiki/JSON_streaming#Line-delimited_JSON) ([JSON Lines](http://jsonlines.org/)) format.

**Only need the sheet files to learn music? try [musescore-downloader](https://github.com/Xmader/musescore-downloader).**

### [View/Query](https://console.cloud.google.com/bigquery?project=xmader&p=xmader&d=musescore&page=dataset) in Google BigQuery

### User Data

> Update Manually,  
> Last Updated: Mar 16, 2020

https://musescore-dataset.xmader.com/user.jsonl

### Music Sheet Metadata

> Update daily at 7:10 am ET (UTC-5 / UTC-4 Daylight Saving Time)

https://musescore-dataset.xmader.com/score.jsonl

### All `mscz` files

> Update daily at 7:10 am ET (UTC-5 / UTC-4 Daylight Saving Time)

https://musescore-dataset.xmader.com/mscz-files.csv

```sh
# The CSV file itself is on IPFS
wget -O mscz-files.csv https://ipfs.io/ipns/QmSdXtvzC8v8iTTZuj5cVmiugnzbR1QATYRcGix4bBsioP/mscz-files.csv.part{0..15}
```

This is a csv file, which contains score id (`id`) and the corresponding IPFS reference (`ref`).

All files are available on [IPFS](https://ipfs.io/).  
NO ONE CAN TAKE IT DOWN NOW!

#### Via [IPFS HTTP Gateways](https://docs.ipfs.io/how-to/address-ipfs-on-web/#http-gateways)

* https://ipfs.infura.io/{ref}
* https://ipfs.eternum.io/{ref}
* https://ipfs.io/{ref}
* https://cloudflare-ipfs.com/{ref}
* [more](https://ipfs.github.io/public-gateway-checker/)

```sh
#!/bin/bash
while IFS=, read -r id ref
do
    wget -nv https://ipfs.infura.io$ref -O $id.mscz
done < <(sed '1d' mscz-files.csv)
```

#### Or using local IPFS daemon

```bash
#!/bin/bash

# Install IPFS https://docs.ipfs.io/how-to/command-line-quick-start/#install-ipfs

ipfs daemon --init &

while IFS=, read -r id ref
do
    ipfs get $ref -o $id.mscz
done < <(sed '1d' mscz-files.csv)
```

[Contact me](mailto:i@xmader.com) if you have any questions.

> The purpose of the project is to make the data of musescore.com accessible to anyone in need, and bring a clean and high-quality music dataset to the world of computer science, but **not for individuals who only want to keep the data pointlessly**.

## Special Thanks

I would like to thank Luca B., 
telling me that what I am doing is meaningful.
