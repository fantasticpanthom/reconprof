Here I put random one liners that I use.

### certspotter

```
curl -s https://certspotter.com/api/v0/certs\?domain\=$domain | grep dns_names | cut -d ':' -f2 | tr , '\n' | sed "s/\"//g" | sed "s/\[//g" | sed "s/\]//g" | sed '/^$/d' | sort -u
```

### crtsh

```
curl -s https://crt.sh/\?q\=%.$domain\&output\=json | tr , '\n' | grep name_value | cut -d ":" -f2 | sed "s/\"//g" | grep -Eo "[a-zA-Z0-9./?=_-]*" | sed '/^$/d' | sort -u
```

### shodan

```
curl "https://api.shodan.io/dns/domain/$1?key={APIKEY}" | awk -F "subdomains" '{print $2}' | tr , '\n' | sed "s/\"//g" | sed "s/\[//g" | sed "s/\]//g" | sed "s/://g" | sed "s/}//g" | sed "s/ //g" | xargs -n1 -I{} sh -c "echo {}.$1"
```

### Get Google Analytics Id

```
nohup curl $url | grep 'ga("create"' | cut -b 15-27
```
