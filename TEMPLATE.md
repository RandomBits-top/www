```js
// {{ TEMPLATE: }}
module.exports = {
  PUBLIC_REPOS: {
    type: 'customQuery',
    loop: true,
    query: async (octokit, moment, user) => {
      const result = await octokit.graphql(`
        {
          organization(login: "RandomBits-top") {
            repositories(first: 100) {
              nodes {
                REPO_NAME: name
                REPO_FULL_NAME: nameWithOwner
                REPO_GITHUB_URL: url
                REPO_HOMEPAGE_URL: homepageUrl
                REPO_DESCRIPTION: description
              }
            }
          }
        }
      `);
      const nodes = result.organization.repositories.nodes;
      const repos=[]
      //loop nodes, populate repos, editing along the way
      for (const repo of nodes) {
        if(repo.REPO_HOMEPAGE_URL) {
          repo.REPO_URL = repo.REPO_HOMEPAGE_URL
        }
        else {
          repo.REPO_URL = repo.REPO_GITHUB_URL
        }
        if(repo.REPO_DESCRIPTION === null) {
          repo.REPO_DESCRIPTION=" ";
        }
        if(repo.REPO_NAME != "www") {        
          repos.push(repo)
        }
      }
      return repos
    }
  }
};
// {{ :TEMPLATE }}
```

| 📦Project    | 📚Description |
| ---------  | -------------- |
{{ loop PUBLIC_REPOS }}
| [{{ REPO_NAME }}]({{ REPO_URL }}) | {{ REPO_DESCRIPTION }} |
{{ end PUBLIC_REPOS }}

