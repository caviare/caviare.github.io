---
title: "特殊短语规则"
date: 2016-08-30T16:01:23+08:00
lastmod: 2018-02-01T18:01:23+08:00
draft: false
categories: [Even示例]
weight: 999
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

![img](https://sm.ms/image/tXbLDioexBEOkVm "img")

{{% center %}}

## center

![img](https://sm.ms/image/tXbLDioexBEOkVm "img")
{{% /center %}}

{{% right %}}

## right

![img](https://sm.ms/image/tXbLDioexBEOkVm "img")
{{% /right %}}

{{% left %}}

## left

![img](https://sm.ms/image/tXbLDioexBEOkVm "img")
{{% /left %}}

---

## figure with class

```
{{%/* figure src="/path/to/img.gif" title="default" alt="img" */%}}
{{%/* figure class="center" src="/path/to/img.gif" title="center" alt="img" */%}}
{{%/* figure class="right" src="/path/to/img.gif" title="right" alt="img" */%}}
{{%/* figure class="left" src="/path/to/img.gif" title="left" alt="img" */%}}
```

{{% figure src="https://sm.ms/image/tXbLDioexBEOkVm" title="default" alt="img" %}}
{{% figure class="center" src="https://sm.ms/image/tXbLDioexBEOkVm" title="center" alt="img" %}}
{{% figure class="right" src="https://sm.ms/image/tXbLDioexBEOkVm" title="right" alt="img" %}}
{{% figure class="left" src="https://sm.ms/image/tXbLDioexBEOkVm" title="left" alt="img" %}}

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

{{% figure src="https://sm.ms/image/tXbLDioexBEOkVm" title="default" alt="img" %}}
{{% figure class="right" src="https://sm.ms/image/tXbLDioexBEOkVm" title="right" alt="img" %}}
{{% left %}}
{{% figure src="https://sm.ms/image/tXbLDioexBEOkVm" title="default in left" alt="img" %}}
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
{{%/* music id="28196554" auto="1" */%}}
```

- Example

```
{{%/* music "28196554" */%}}
```

{{% music "28196554" %}}

<style>
.post-content img {
  height: 64px;
}
</style>