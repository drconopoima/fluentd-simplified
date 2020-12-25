# Fluentd Simplified

## Clone project
```bash
git clone https://github.com/drconopoima/fluentd-simplified
```

### Generate image with plugins
The fluentd configuration uses the following plugins
* rewrite-tag-filter
* geoip

You would need to modify the standard image by using the Dockerfile provided

```bash
cd fluentd-simplified
docker build --rm --pull \
-f "./Dockerfile" \
-t "fluentd-simplified:1.11-debian-1" "./"
```

## Run Fluentd

### With plugins
```bash
docker run -ti --rm \
-v $(pwd)/etc:/fluentd/etc \
-v $(pwd)/log:/var/log/ \
-v $(pwd)/output:/output \
fluentd-simplified:1.11-debian-1 \
-c /fluentd/etc/fluentd.conf -v
```

If you would want to skip the geoip functionality, comment the appropriate section
`@type geoip` from `etc/fluentd.conf`, and then you could run official image
and install the rewrite-tag-filter the following way:

## Run Fluentd with plugin
```bash
docker run -u root -ti --rm \
-v $(pwd)/etc:/fluentd/etc \
-v $(pwd)/log:/var/log/ \
-v $(pwd)/output:/output \
fluent/fluentd:v1.11-debian-1 \
bash -c "gem install fluent-plugin-rewrite-tag-filter && fluentd -c /fluentd/etc/fluentd.conf -v"
```

## Acknowledgements

This repo is a fork from [this project from r1ckr](https://github.com/r1ckr/fluentd-simplified), and it is used as the source code of [this](https://scaleout.ninja/post/fluentd-simplified/) post.

