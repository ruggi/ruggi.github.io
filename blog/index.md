# Blog

> Bits.

<div class="posts">
{{ range $index, $page := reverse ( byDate .Pages.blog ) }}
    {{ if ne "index.md" $page.Base }}
- <span class="date">{{ $page.Date.Format "2006-01-02" }}</span> [{{.Title}}]({{.Path}})
    {{ end }}
{{end}}
</div>
