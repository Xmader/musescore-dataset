
# musescore-dataset

The unofficial dataset of all music sheets and users on musescore.com, dedicated to big data analytics / data science / machine learning.

> All data is collected by iterating through [musecore.com's *public* API](https://developers.musescore.com/).

> The `jsonl` files are in the [Newline-delimited JSON](https://en.wikipedia.org/wiki/JSON_streaming#Line-delimited_JSON) ([JSON Lines](http://jsonlines.org/)) format.

**Only need the sheet files to learn music? try [musescore-downloader](https://github.com/Xmader/musescore-downloader).**

### [View/Query](https://console.cloud.google.com/bigquery?project=xmader&p=xmader&d=musescore&page=dataset) in Google BigQuery

### User Data

> Update Manually,  
> Last Updated: Nov 9, 2020

https://musescore-dataset.xmader.com/user.jsonl

### Music Sheet Metadata

> Update daily at 7:10 am ET (UTC-5 / UTC-4 Daylight Saving Time)

https://musescore-dataset.xmader.com/score.jsonl

### All `mscz` files

> Update daily at 7:10 am ET (UTC-5 / UTC-4 Daylight Saving Time)

https://musescore-dataset.xmader.com/mscz-files.csv

```sh
# The CSV file itself is on IPFS
# ipns://QmSdXtvzC8v8iTTZuj5cVmiugnzbR1QATYRcGix4bBsioP
cid=$(curl https://musescore-dataset.xmader.com/csv-ipfs-ref | grep -o "\\w\{46\}")
wget -O mscz-files.csv https://ipfs.io/ipfs/${cid}/mscz-files.csv
```

This is a csv file, which contains score id (`id`) and the corresponding IPFS reference (`ref`) to each mscz file.

All files are available on [IPFS](https://ipfs.io/).  
NO ONE CAN TAKE IT DOWN NOW!

#### Bulk Download

See <https://discord.com/channels/774491656643674122/774491656643674128/784661028310220820>

(You must join the [LibreScore Community Discord](https://discord.gg/DKu7cUZ4XQ) first to see the message.)  
[![Discord](https://img.shields.io/discord/774491656643674122?color=7289da&label=Discord&logo=discord)](https://discord.gg/DKu7cUZ4XQ)

#### Download mscz files via [IPFS HTTP Gateways](https://docs.ipfs.io/how-to/address-ipfs-on-web/#http-gateways)

* https://ipfs.io/{ref}
* https://cloudflare-ipfs.com/{ref}
* [more](https://ipfs.github.io/public-gateway-checker/)

```sh
#!/bin/bash
while IFS=, read -r id ref
do
    if [ -f "$id.mscz" ]; then
        echo "$id.mscz exists."
    else
        echo "$id.mscz does not exist."
        wget -nv --read-timeout=20 https://ipfs.io$ref -O $id.mscz
    fi
done < <(sed '1d' mscz-files.csv)
```

#### Using CURL

```bash
#!/bin/bash
while IFS=, read -r id ref
do
    if [ -f "$id.mscz" ]; then
        echo "$id.mscz exists."
    else
        echo "$id.mscz does not exist."
        curl -\# https://ipfs.io$ref -o $id.mscz -m 20
    fi
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
