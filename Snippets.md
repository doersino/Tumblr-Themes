# Snippets

Some HTML5 code snippets that may prove useful for rapid Tumblr theme development.

Comments like `<!-- ... -->` or `/* ... */` denote placeholders for your own code.

### Table of Contents
- [Basic Structure](#user-content-basic-structure)
- [Pagination](#user-content-pagination)
	- [Index Pagination](#user-content-index-pagination)
	- [Permalink Pagination](#user-content-permalink-pagination)
	- [Day Pagination](#user-content-day-pagination)
- [Posts Wrapper](#user-content-posts-wrapper)
- [Day Page Link](#user-content-day-page-link)

## Basic Structure
Containing all required `<head>` metadata.

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>
		{block:DayPage}
			{lang:Viewing everything posted on Month DayOfMonth Year} -
		{/block:DayPage}
		{block:TagPage}
			{lang:Showing TagResultCount posts tagged Tag} -
		{/block:TagPage}
		{block:SearchPage}
			{lang:Found SearchResultCount results for SearchQuery}
			{lang:Sorry no results for SearchQuery} -
		{/block:SearchPage}
		{block:PostSummary}
			{PostSummary} -
		{/block:PostSummary}
		{Title}
	</title>
	{block:Description}
		<meta name="description" content="{MetaDescription}">
	{/block:Description}
	<link rel="shortcut icon" href="{Favicon}">
	<link rel="apple-touch-icon" href="{PortraitURL-128}">
	<link rel="alternate" type="application/rss+xml" href="{RSS}">

	<!-- theme options -->
	<!-- ... -->

	<!-- external scripts and stylesheets -->
	<!-- ... -->

	<style>
	/* theme styles */
	/* ... */

	{CustomCSS}
	</style>
</head>
<body>
	<!-- ... -->
</body>

```

## Pagination

### Index Pagination
On index pages, this snippet shows links to some previous and next pages, as well as the first and last page available (e.g. « ‹ 4 5 *6* 7 8 › »).

```html
{block:Pagination}
	<nav class="pagination">
		<ol>
			{block:PreviousPage}
				<li><a href="/page/1">&laquo;</a></li>
				<li><a href="{PreviousPage}" title="{lang:Newer posts}">&lsaquo;</a></li>
			{/block:PreviousPage}
			{block:JumpPagination length="5"}
				{block:CurrentPage}
					<li><em>{PageNumber}</em></li>
				{/block:CurrentPage}
				{block:JumpPage}
					<li><a href="{URL}">{PageNumber}</a></li>
				{/block:JumpPage}
			{/block:JumpPagination}
			{block:NextPage}
				<li><a href="{NextPage}" title="{lang:Older posts}">&rsaquo;</a></li>
				<li><a href="/page/{TotalPages}">&raquo;</a></li>
			{/block:NextPage}
		</ol>
	</nav>
{/block:Pagination}
```

### Permalink Pagination
On permalink pages, this shows links to the previous and next post.

```html
{block:PermalinkPagination}
	<nav class="permalink-pagination">
		<ol>
			{block:NextPost}
				<li><a href="{NextPost}">&lsaquo; {lang:Newer}</a></li>
			{/block:NextPost}
			{block:PreviousPost}
				<li><a href="{PreviousPost}">{lang:Older} &rsaquo;</a></li>
			{/block:PreviousPost}
		</ol>
	</nav>
{/block:PermalinkPagination}
```

### Day Pagination
On day pages (e.g. `/day/2014/08/30/`), this shows links to the previous and next day page.

```html
{block:DayPagination}
	<nav class="day-pagination">
		<ol>
			{block:NextDayPage}
				<li><a href="{NextDayPage}">&lsaquo; {lang:Newer}</a></li>
			{/block:NextDayPage}
			{block:PreviousDayPage}
				<li><a href="{PreviousDayPage}">{lang:Older} &rsaquo;</a></li>
			{/block:PreviousDayPage}
		</ol>
	</nav>
{/block:DayPagination}
```

## Posts Wrapper
The advantage of using `{block:HasTags}{block:Tags} tag-{URLSafeTag}{/block:Tags}{/block:HasTags}` instead of `{TagsAsClasses}` is that this will prevent any conflicts when using tags that equal classes used in your theme. However, this solution does not include some of the useful features `{TagsAsClasses}` provides, e.g. adding the class "reblog" if the post was reblogged from another post.

```html
{block:Posts}
	<article id="post-{PostID}" class="{PostType}{block:HasTags}{block:Tags} tag-{URLSafeTag}{/block:Tags}{/block:HasTags}">
		{block:Text}
			<!-- ... -->
		{/block:Text}
		<!-- ... -->
	</article>
{/block:Posts}
```

## Day Page Link
On permalink pages, this shows a link to the corresponding day page.

```html
<a href="/day/{Year}/{MonthNumberWithZero}/{DayOfMonthWithZero}/">{lang:Show all posts made on this day}</a></p>
```
