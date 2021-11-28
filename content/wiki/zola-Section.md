+++
+++

セクションは`content`内のディレクトリが`_index.md`ファイルを含むときに常に作られる。ディレクトリが`_index.md`ファイルを含まない場合、セクションは作られないが、そのディレクトリ内のmarkdownファイルはページを生成する。このページはorpahn pageと呼ばれる。

目次ページ(`base_url`をブラウズしたときに表示されるページ）はセクションであり、それは`_index.md`ファイルを`content`ディレクトリのルートに加えたかに関係なく生成される。`content`ディレクトリのルートに`_index.md`を作らない場合、このメインセクションはcontentとメタデータを全く持たない。contentやメタデータを加えたい場合、`_index.md`ファイルを`content`ディレクトリのルートに加え、他の`_index.md`ファイルと同様に編集できる。`index.html`テンプレートがcontentとメタデータにアクセスできるようになる。

markdown以外のファイルは`assets`コレクションに加えられる。これらのファイルはmarkdownファイルから相対リンクで利用できる。

## Drafting

pageがfront matterで`draft`を設定することで下書きできるように、sectionも下書きできる。デフォルトでは下書きにはされていない。セクションが下書きにされたとき、その配下のページやサブセクションやアセットは`--drafts`フラグを渡されない限り処理されない。親セクションが下書きになっている限り、`draft`の指定されていないページも処理されないことに注意しよう。

## Front matter

ディレクトリ内の`_index.md`がそのセクションのcontentとメタデータを決める。メタデータを設定するには、fronto matterをそのファイルに加える。

TOML front matterはファイルの最初に`+++`で囲まれて書かれているメタデータのセットである。

終了`+++`の後にcontentを書ける。それはmarkdownとしてパースされ、`section.content`変数を通じてテンプレートとして利用できる。

front matterに変数を指定しない場合も開始と終了分の`+++`が要求される。

TOMLが推奨されるがYAMLもサポートされている。この場合囲み文字は`---`になる。

全ての変数をデフォルトと同じように指定した例：

```toml
title = ""

description = ""

# A draft section is only loaded if the `--drafts` flag is passed to `zola build`, `zola serve` or `zola check`.
draft = false

# Used to sort pages by "date", "weight" or "none". See below for more information.
sort_by = "none"

# Used by the parent section to order its subsections.
# Lower values have higher priority.
weight = 0

# Template to use to render this section page.
template = "section.html"

# 与えられたtemplateはセクション配下の「全ての」ページに再帰的に適用される。もしネストされたセクションの下にページがあれば、一番近いpage_templateが使用される。
# ただし、ページ自身のtempletaが優先される。
# デフォルトでは設定されていない。
page_template =

# paginatedされたページに一度に表示されるページ数を設定する。
# この変数が設定されないか0の場合、paginationされない。
paginate_by = 0

# 設定された場合、paginated pageに使われるパスになる。ページ番号がこのパスの後に続く。
# The default is page/1.
paginate_path = "page"

# This determines whether to insert a link for each header like the ones you can see on this site if you hover over
# a header.
# The default template can be overridden by creating an `anchor-link.html` file in the `templates` directory.
# This value can be "left", "right" or "none".
insert_anchor_links = "none"

# If set to "true", the section pages will be in the search index. This is only used if
# `build_search_index` is set to "true" in the Zola configuration file.
in_search_index = true

# If set to "true", the section homepage is rendered.
# Useful when the section is used to organize pages (not used directly).
render = true

# This determines whether to redirect when a user lands on the section. Defaults to not being set.
# Useful for the same reason as `render` but when you don't want a 404 when
# landing on the root section page.
# Example: redirect_to = "documentation/content/overview"
redirect_to = 

# If set to "true", the section will pass its pages on to the parent section. Defaults to `false`.
# Useful when the section shouldn't split up the parent section, like
# sections for each year under a posts section.
transparent = false

# Use aliases if you are moving content but want to redirect previous URLs to the
# current one. This takes an array of paths, not URLs.
aliases = []

# If set to "true", a feed file will be generated for this section at the
# section's root path. This is independent of the site-wide variable of the same
# name. The section feed will only include posts from that respective feed, and
# not from any other sections, including sub-sections under that section.
generate_feed = false

# Your own data.
[extra]
```

## Pagination

セクションのページのPaginationを有効にするには`paginate_by`を正の数に設定する。pagination template documentationにはより多くの情報が書いてある。どんな変数がテンプレートに使えるか知りたい場合は参照すること。

## Sorting

Zola templatesではディスプレイするためにページやセクションを反復(iterate)することが多い。例：`blog/Post_1.md`, `blog/Post_2.md`, `blog_Post_3.md`を持つ`blog`ディレクトリ。この３つのポストを反復してポストへのリンクのリストを作るにはシンプルなtemplateを使う:

```html
{% for post in section.pages %}
  <h1><a href="{{ post.permalink }}">{{ post.title }}</a></h1>
{% endfor %}
```

これは`sort_by`で指定された順序でポストをiterateする。`sort_by`変数は`date`, `weight`, `none`の3つの値をとる。`sort_by`が設定されていない場合、ページは`none`でソートされ、ソートされたコンテンツになるよう意図されていない順序になる。

ソートに必要な情報がないページは無視される。例えば`sort_by="date"`の場合、そのページ（メタデータにdataがないページ）は無視される。これが起こったときはターミナルが警告する。

## Sorting pages

`sort_by`fromt matter 変数は次の値を持つことができる

- `date`
- `weight`
- Reversed sorting

## Sorting subsections

- 

