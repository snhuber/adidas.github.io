# adidas GitHub Portal

Website to display adidas Open Source projects.

# How To

## Show a REPOSITORY in adidas GitHub Portal

A repository must comply with the following:

1. Belongs to https://github.com/adidas
1. `.meta.yml` file exists

### .meta.yml definition

| Key | Defaults | Description |
| --- | --- | --- |
| `imageUrl` | `'/img/source.jpg'` | A representative image of the project |
| `backgroundColor` | N/A | Background color for the card |
| `display.name` | `""` | Overrides the repository name from GitHub |
| `display.description` | `""` | Overrides the repository description from GitHub |
| `keywords` | `[]` | A list of keywords to search for this repo |

## Show a PROJECT in adidas GitHub Portal

To show a project in the GitHub portal, go to adidas GitHub portal CMS.

### Project configuration

| Key | Required | Defaults | Description |
| --- | --- | --- | --- |
| `id` | Yes | N/A | A unique identifier for the project |
| `name` | Yes | N/A | The name of the project |
| `description` | Yes | N/A | A brief description of the project |
| `url` | Yes | N/A | The link to the public website of the project |
| `config.imageUrl` | Yes | N/A | A representative image of the project |
| `config.backgroundColor` | No | N/A | Background color for the card |
| `config.keywords` | No | `[]` | A list of keywords to search for this project |

# Development

## Requirements

- node >= 8
- npm >= 5

## npm scripts

```npm start```

Runs a development server on `localhost:3000`. Runs `nuxt` under the hood.

```npm run build```

Builds the project distributables. Runs `nuxt generate --spa` under the hood so the website is ready to be deployed as a Single Page Application.

```npm run serve```

Runs the site on a server with SSR capabilities. Runs `nuxt build && nuxt start` under the hood.

```npm run lint```

Runs `eslint` to check that all the source JS and Vue files are compliant.


# Deployment

## GitHub Pages

```
git checkout develop
npm install
npm run build
git add -f ./dist
git commit -m "UPDATE gh-pages"
git subtree split --prefix dist -b gh-pages
git push -f origin gh-pages:master
```

## Dockerize

```
npm install
npm run build
npm prune --production
docker build -t adidas-github-io .

docker run -dit \
           --name adidas-github-io \
           -p 1337:80 \
           adidas-github-io
```

## Deploy to k8s

- Make sure there is a docker-config secret `tools.adidas-group.com` in the cluster.

```
npm install
npm run build
npm prune --production
docker build -t tools.adidas-group.com:5000/pabb/adidas-github-io .
docker push tools.adidas-group.com:5000/pabb/adidas-github-io
envsubst < deploy/all.yml > deploy.yml
kubectl apply -f deploy.yml
```
