```js
// {{ TEMPLATE: }}
module.exports = {
  "PUBLIC_REPOS": {
    type: 'repos',
    params: `
      first: 10,
      privacy: PUBLIC,
      ownerAffiliations:[ORGANIZATION_MEMBER],
      orderBy: { field:UPDATED_AT, direction: DESC },
    `,
  }
}
// {{ :TEMPLATE }}
```

| 📦Repo    | ⭐️ WWW | 📚Description |
| --------- | ----------- | -------------- |
{{ loop PUBLIC_REPOS }}
| [{{ REPO_FULL_NAME }}]({{ REPO_URL }}) | [{{ REPO_NAME }}]({{ REPO_HOMEPAGE_URL }}) | {{ REPO_DESCRIPTION }} |
{{ end PUBLIC_REPOS }}
