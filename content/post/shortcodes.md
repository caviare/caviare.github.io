---
title: "Hugo自动化部署"
date: 2022-05-10T17:31:09+08:00
lastmod: 2022-05-10T17:31:09+08:00
draft: true
keywords: ["Hugo", "Github Action", "GitHub Pages"]
description: "使用 Github Action 持续集成工具，自动将博客部署至 GitHub Pages 或 云服务中。"
categories: ["技术"]
author: "caviare"
weight: 998
---

# Admonition

{{% admonition abstract abstract %}}
biu biu biu.
{{% /admonition %}}

```markdown
{{%/* admonition abstract abstract */%}}
biu biu biu.
{{%/* /admonition */%}}
```

<!--more-->

{{% admonition note "I'm title!" false %}}
biu biu biu.

{{% admonition type="note" title="note" details="true" %}}
biu biu biu.
{{% /admonition %}}

{{% admonition example %}}
Without title.
{{% /admonition %}}

{{% /admonition %}}

```markdown
{{%/* admonition note "I'm title!" false */%}}
biu biu biu.

{{%/* admonition type="note" title="note" details="true" */%}}
biu biu biu.
{{%/* /admonition */%}}

{{%/* admonition example */%}}
Without title.
{{%/* /admonition */%}}

{{%/* /admonition */%}}
```

{{% admonition info "info" %}}
biu biu biu.
{{% /admonition %}}

{{% admonition tip "tip" %}}
biu biu biu.
{{% /admonition %}}

{{% admonition success "success" %}}
biu biu biu.
{{% /admonition %}}

{{% admonition question "question" %}}
biu biu biu.
{{% /admonition %}}

{{% admonition warning "warning" %}}
biu biu biu.
{{% /admonition %}}

{{% admonition failure "failure" %}}
biu biu biu.
{{% /admonition %}}

{{% admonition danger "danger" %}}
biu biu biu.
{{% /admonition %}}

{{% admonition bug "bug" %}}
biu biu biu.
{{% /admonition %}}

{{% admonition example "example" %}}
biu biu biu.
{{% /admonition %}}

{{% admonition quote "quote" %}}
biu biu biu.
{{% /admonition %}}

# center, right, left

```markdown
## default

![img](/path/to/img.gif "img")

{{%/* center */%}}

## center

![img](/path/to/img.gif "img")
{{%/* /center */%}}

{{%/* right */%}}

## right

![img](/path/to/img.gif "img")
{{%/* /right */%}}

{{%/* left */%}}

## left

![img](/path/to/img.gif "img")
{{%/* /left */%}}
```

## default

![img](https://tva1.sinaimg.cn/large/005M2kKhly1gwqaq491wuj30p00p0wf0.jpg "img")

{{% center %}}

## center

![img](https://tva1.sinaimg.cn/large/005M2kKhly1gwqaq491wuj30p00p0wf0.jpg "img")
{{% /center %}}

{{% right %}}

## right

![img](https://tva1.sinaimg.cn/large/005M2kKhly1gwqaq491wuj30p00p0wf0.jpg "img")
{{% /right %}}

{{% left %}}

## left

![img](https://tva1.sinaimg.cn/large/005M2kKhly1gwqaq491wuj30p00p0wf0.jpg "img")
{{% /left %}}

---

## figure with class

```
{{%/* figure src="/path/to/img.gif" title="default" alt="img" */%}}
{{%/* figure class="center" src="/path/to/img.gif" title="center" alt="img" */%}}
{{%/* figure class="right" src="/path/to/img.gif" title="right" alt="img" */%}}
{{%/* figure class="left" src="/path/to/img.gif" title="left" alt="img" */%}}
```

{{% figure src="https://tva1.sinaimg.cn/large/005M2kKhly1gwqaq491wuj30p00p0wf0.jpg" title="default" alt="img" %}}
{{% figure class="center" src="https://tva1.sinaimg.cn/large/005M2kKhly1gwqaq491wuj30p00p0wf0.jpg" title="center" alt="img" %}}
{{% figure class="right" src="https://tva1.sinaimg.cn/large/005M2kKhly1gwqaq491wuj30p00p0wf0.jpg" title="right" alt="img" %}}
{{% figure class="left" src="https://tva1.sinaimg.cn/large/005M2kKhly1gwqaq491wuj30p00p0wf0.jpg" title="left" alt="img" %}}

---

```
{{%/* center */%}}

## hybrid in center
{{%/* figure src="/path/to/img.gif" title="default" alt="img" */%}}
{{%/* figure class="right" src="/path/to/img.gif" title="right" alt="img" */%}}

{{%/* left */%}}
{{%/* figure src="/path/to/img.gif" title="default in left" alt="img" */%}}
{{%/* /left */%}}

{{%/* /center */%}}
```

{{% center %}}

## hybrid in center

{{% figure src="https://tva1.sinaimg.cn/large/005M2kKhly1gwqaq491wuj30p00p0wf0.jpg" title="default" alt="img" %}}
{{% figure class="right" src="https://tva1.sinaimg.cn/large/005M2kKhly1gwqaq491wuj30p00p0wf0.jpg" title="right" alt="img" %}}
{{% left %}}
{{% figure src="https://tva1.sinaimg.cn/large/005M2kKhly1gwqaq491wuj30p00p0wf0.jpg" title="default in left" alt="img" %}}
{{% /left %}}
{{% /center %}}

---

# Music 163

## Params

- `id`

  - required param
  - you can extract from music url
  - url format http://music.163.com/#/song?id=28196554

- Fiddle `auto`
  - optional param
  - default value 0
  - you can overwrite it with 1

## Examples

- Simple

```
{{%/* music "28196554" */%}}
{{%/* music "28196554" "1" */%}}
```

- Named Params

```
{{%/* music id="28196554" */%}}
{{%/* music id="28196554" "1" */%}}
```

- Example

```
  {{%/* music "28196554" */%}}
```

{{% music id="28196554" %}}

<style>
  .post img {
    height: 64px
  }
</style>
