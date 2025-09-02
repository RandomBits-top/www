```js
// {{ TEMPLATE: }}
module.exports = {
  "PUBLIC_REPOS": {
    type: 'customQuery',
    loop: true,
    query: async (octokit, moment, user) => {
      const result = await octokit.graphql(`
        query {
            repositories() {
              edges {
                node {
                  REPO_NAME: name
                  owner {
                    login
                  }
                  REPO_FULL_NAME: nameWithOwner
                  REPO_DESCRIPTION: description
                  REPO_URL: url
                  REPO_HOMEPAGE_URL: homepageUrl || "#"
                  REPO_CREATED_TIMESTAMP: createdAt
                  REPO_PUSHED_TIMESTAMP: pushedAt
                  diskUsage
                  REPO_FORK_COUNT: forkCount
                  REPO_ID: id
                  stargazers {
                    totalCount
                  }
                  primaryLanguage {
                    name
                  }
                }
              }
            }
          }
      `)
      const repoEdges = queryResult.viewer.repositories.edges
      const repos = []
      for (const repoEdge of repoEdges) {
        let repo = repoEdge.node
        repo = fixRepoValues(repo)
        repos.push(repo)
      }
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

{{ loop REPOTEST }}
{{ REPO_FULL_NAME }}
{{ end REPOTEST }}
