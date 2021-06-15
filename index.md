<!-- {"Title": "Federico Ruggi"} -->

I am a software engineer focused on distributed systems and cloud computing.

I live in Amsterdam, working at [Docker](https://docker.com).

You can find me on [GitHub](https://github.com/ruggi) and [Twitter](https://twitter.com/ruggif).

## Posts
<ul class="posts">
{{ range $index, $page := reverse ( byDate .Pages.blog ) }}
<li>
<span class="date">{{ $page.Date.Format "2006-01-02" }}</span>
<a href="{{ $page.Path }}">{{ $page.Title }}</a>
</li>
{{end}}
</ul>
