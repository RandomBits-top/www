```js
// {{ TEMPLATE: }}
module.exports = {
  "PUBLIC_REPOS": {
    type: 'repos',
    params: `
      first: 2,
      privacy: PUBLIC,
      ownerAffiliations:["RandomBits-top",
      orderBy: { field:REPO_PUSHED_DATE, direction: DESC },
    `,
  }
```

| 📦Repo    | ⭐️ WWW | 📚Description |
| --------- | ----------- | -------------- |
{{ loop PUBLIC_REPOS }}
| {{ REPO_STARS }} | [{{ REPO_NAME }}]({{ REPO_URL }}) | [{{ REPO_FULL_NAME }}]({{ REPO_HOMEPAGE_URL }}) | {{ REPO_DESCRIPTION }} |
{{ end PUBLIC_REPOSS }}
// {{ :TEMPLATE }}
