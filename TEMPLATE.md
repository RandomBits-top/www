```js
// {{ TEMPLATE: }}
module.exports = {
  "PUBLIC_REPOS": {
    type: 'customQuery',
    loop: true,
    query: async (octokit, moment, user) => {
      const result = await octokit.graphql(`
        query {
          search(query: "is:public", type: REPOSITORY, first: 50) {
            repositoryCount
            pageInfo {
              endCursor
              startCursor
              hasNextPage
            }
            edges {
              node {
                ... on Repository {
                  name
                  url
                  createdAt
                  updatedAt
                  description
                  owner {
                    login
                  }
                }
              }
            }
          }
        }
      `)
      const repoEdges = result.repositories.edges
      const repos = []
#      for (const repoEdge of repoEdges) {
#        let repo = repoEdge.node
#        repo = fixRepoValues(repo)
#        repos.push(repo)
#      }
      return repos
    }
  }
}
// {{ :TEMPLATE }}
```

| 📦Repo    | ⭐️ WWW | 📚Description |
| --------- | ----------- | -------------- |
{{ loop PUBLIC_REPOS }}
| [{{ REPO_FULL_NAME }}]({{ REPO_URL }}) | [{{ REPO_NAME }}]({{ REPO_HOMEPAGE_URL }}) | {{ REPO_DESCRIPTION }} |
{{ end PUBLIC_REPOS }}

