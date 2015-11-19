data-science-docker-notebook
============================

An ipython notebook server for data science development

## Philosophy

The notebook is intended to contain the environment to perform development and anaysis. The data-only containers provide the source code (notebooks) and the data sources (data files, output, persistent caches, databases etc.. The notebook should therefore be **stateless**.

## Guide for use

Create data-only containers for sprint notebooks and data folders:

``` bash
docker run -d -v ~/notebooks:/notebooks --name notebooks ubuntu echo notebooks
docker run -d -v ~/data:/data --name sprint_data ubuntu echo data
```

Fork the repo and clone.

Modify requirements in to your needs `requirements.txt`.

Build the image from the root of the repo, for example:

```
docker build -t calvingiles/ds-notebook .
```

then start a container from the image:

```bash
docker run \
	-d \
	-e "PASSWORD=Password" \
	--name data-science-docker-notebook \
	-p 443:8888 \
	--volumes-from data \
	--volumes-from notebooks \
	calvingiles/ds-notebook
```

### Starting the notebook

Find the right ip address by typing in the terminal:

```
docker-machine ip default
```

### Automated docker builds

Add an automated build on docker pointing at your forked repo to keep the docker hub images up to date. Then you can skip the build stage above and the latest version will be pulled from docker hub.

