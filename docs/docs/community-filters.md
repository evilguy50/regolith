---
title: Community Filters
---

<!-- This page is auto-generated. If your filters are not on this list,
 make a pull request to add your repo link to the filter resolver -->
<script>
  // Official resolver
  // const rawResolver = "https://raw.githubusercontent.com/Bedrock-OSS/regolith-filter-resolver/main/resolver.json"
  // Dev test resolver
  const rawResolver = "https://raw.githubusercontent.com/evilguy50/regolith-filter-resolver/main/resolver.json"

  const createEntry = (name, url, author, lang, description) => {
    let newEntry = document.createElement("tr")

    let nameElm = document.createElement("td")
    let nameLink = document.createElement("a")
    nameLink.innerText = name
    nameLink.href = "http://" + url
    nameElm.appendChild(nameLink)

    let authorElm = document.createElement("td")
    authorElm.innerText = author

    let langElm = document.createElement("td")
    langElm.innerText = lang

    let descElm = document.createElement("td")
    descElm.innerText = description

    const cells = [nameElm, authorElm, langElm, descElm]
    cells.forEach((cell) => {
      newEntry.appendChild(cell)
    })

    return newEntry
  }

  fetch(rawResolver, {cache: "no-store"}).then((res) => {
    const filterList = document.getElementById("filterList")
    res.text().then((textRes) => {
      const jres = JSON.parse(textRes)
      Object.keys(jres.filters).forEach((key) => {
        const newFilter = {
          name: key,
          url: `${jres.filters[key].url}/tree/${jres.filters[key].main_branch}/${key}`,
          author: jres.filters[key].url.split("/")[1],
          lang: jres.filters[key].lang,
          description: jres.filters[key].description
        }
        filterList.appendChild(createEntry(...Object.values(newFilter)))
      })
    })
  })
</script>

# Community Filters

The beauty of Regolith is that filters can be written and shared by anyone! This page contains an uncurated list of community filters. If your filter doesn't appear here, [let us know](https://discord.com/invite/XjV87YN)!

## Installing Community Filters
Community filters are installed via a URL-like resource definition: `github.com/<username>/<repository>/<folder>`.

For example `github.com/SirLich/echo-npc-regolith/echo`.

::: warning
Please use extreme caution when running unknown code. Regolith and its maintainers take no responsibility for any damages incurred by using the filters on this page. To learn more, please read our [safety page](/guide/safety).
:::

::: tip
Having trouble? You can learn more about online filters [here](/guide/online-filters).
:::

## Filters

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Author</th>
      <th>Language</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody id="filterList">
  </tbody>
</table>