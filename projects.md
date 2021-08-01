---
layout: page
permalink: /projects/
---

## VFPX 项目

<table>
<thead>
<tr>
<td><strong>项目</strong></td>
<td><strong>描述</strong></td>
<td><strong>类别</strong></td>
<td><strong>状态</strong></td>
</tr>
</thead>
<tbody>
{% assign projlist = site.data.projects %}
{% for project in projlist %}
<tr>
	<td><a target="_blank" href="{{ project.url }}">{{ project.project }}</a></td>
	<td>{{ project.description }}</td>
	<td>{{ project.category }}</td>
	<td>{{ project.state }}</td>
</tr>
{% endfor %}
</tbody>
</table>

### 其他开源的 VFP 项目

下表中是其他开源的 VFP 项目，它们并不是 VFPX 的组成部分。

<table>
<thead>
<tr>
<td><strong>项目</strong></td>
<td><strong>描述</strong></td>
<td><strong>简体中文地址</strong></td>
</tr>
</thead>
<tbody>
{% assign projlist = site.data.nonvfpx %}
{% for project in projlist %}
<tr>
	<td><a target="_blank" href="{{ project.url }}">{{ project.project }}</a></td>
	<td>{{ project.description }}</td>
	<td><b target="_blank" href="{{ project.url2}}">{{ project.project }}</b></td>
</tr>
{% endfor %}
</tbody>
</table>
