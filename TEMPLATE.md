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
                REPO_URL: url
                REPO_HOMEPAGE_URL: homepageUrl
                REPO_DESCRIPTION: description
              }
            }
          }
        }
      `);
      const nodes = result.organization.repositories.nodes;
      return nodes; // Ensure the result is returned
    }
  }
};
// {{ :TEMPLATE }}
```

| 📦Repo    | ⭐️ WWW | 📚Description |
| --------- | ----------- | -------------- |
{{ loop PUBLIC_REPOS }}
| [{{ REPO_FULL_NAME }}]({{ REPO_URL }}) | [{{ REPO_NAME }}]({{ REPO_HOMEPAGE_URL }}) | {{ REPO_DESCRIPTION }} |
{{ end PUBLIC_REPOS }}

