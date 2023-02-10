## Create a new github repository

## Clone the repository
```shell
git clone git@github.com:chris-addo/helm-charts.git
cd helm-charts
```

## Create robots.txt
### To avoid bot crawling
```shell
echo -e "User-Agent: *\nDisallow: /" > robots.txt
```

## Create a helm chart from scratch
```shell
mkdir -p chart-sources
cd chart-sources
helm create nginx-demo
```

## lint the chart
```shell
helm lint chart-sources/*
```

## Create helm chart package
```shell
helm package chart-sources/nginx-demo
```
## Configure the “helm-chart” repository as a GitHub pages site
Go to GitHub repository -> settings -> GitHub Pages

## Create the helm chart repository index
> A repository is characterized primarily by the presence of a special file called index.yaml that has a list of all of the packages supplied by the repository, together with metadata that allows retrieving and verifying those packages.
```shell
# The URL is your github page URL, is not github repo URL
helm repo index --url https://chris-addo.github.io/helm-charts/ .
```

## Push your charts to Github
```shell
git add . && git commit -m "Initial commit" && git push origin master
```

## Add new charts to an existing repository
> Whenever you need to add a new chart to the Helm chart repository, it’s mandatory for you to regenerate the index.yaml file. The $ helm repo index command will completely rebuild the index.yaml file from scratch, including only the charts that it finds locally, which very likely is our case. However, it worth notice that you can use the --merge flag to incrementally add new charts to an existing index.yaml
```shell
helm repo index --url https://chris-addo.github.io/helm-charts/ --merge index.html .
```