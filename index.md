---
layout: home
title: Home
landing-title: yuichi0301 blog
description:
image:
author:
nav-menu:
---

<!-- Banner -->
<section id="banner" class="major">
	<div class="inner">
		<header class="major">
			<h1>{{ page.landing-title }}</h1>
		</header>
		<div class="content">
			<p style="text-transform: uppercase;">{{ site.description }}</p>
			<ul class="actions">
				<li><a href="#one" class="button next scrolly">Get Started</a></li>
			</ul>
		</div>
	</div>
</section>

<!-- Main -->
<div id="main">

<!-- One -->
{% include tiles.html %}

<!-- Two -->
<section id="two">
	<div class="inner">
		<header class="major">
			<h2>Diet Viewer</h2>
		</header>
		<p>"Diet Viewer"というAndroid用のダイエットアプリを作っています。様々なグラフを表示できて、体重の他にカロリーや運動などを登録できます。</p>
		<ul class="actions">
			<li><a href="https://play.google.com/store/apps/details?id=com.appspot.nagasaki.yuichi.dietviewer&hl=ja" class="button next">Show Google Play</a></li>
		</ul>
	</div>
</section>

</div>
