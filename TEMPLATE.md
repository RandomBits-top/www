```js
// {{ TEMPLATE: }}
module.exports = {
  "PUBLIC_REPOS": {
    type: 'customQuery',
    loop: true,
    query: async (octokit, moment, user) => {
      const result = await octokit.graphql(`
        query {
          repositories(first: 100) {
            nodes {
              name
              url
              homepageUrl
              description
            }
          }
        }
     ')
  }
}
// {{ :TEMPLATE }}
```

| 📦Repo    | ⭐️ WWW | 📚Description |
| --------- | ----------- | -------------- |
{{ loop PUBLIC_REPOS }}
| [{{ REPO_FULL_NAME }}]({{ REPO_URL }}) | [{{ REPO_NAME }}]({{ REPO_HOMEPAGE_URL }}) | {{ REPO_DESCRIPTION }} |
{{ end PUBLIC_REPOS }}

