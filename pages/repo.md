---
title: Repo
layout: repo
permalink: /repo/
---

{% raw %}

<link rel="stylesheet" type="text/css" href="/css/repostyle.css" />
<link rel="stylesheet" type="text/css" href="/css/graphstyle.css" />
<link rel="stylesheet" type="text/css" href="/css/main.css" />

<div id="mainContent">
    <h1 class="page-header text-center">
        <a class="title" href="{{ repo.url }}" alt="View Project on GitHub" title="View Project on GitHub">{{ repo.name }}</a>
        <br />
        <a class="subtitle" href="https://github.com/{{ repo.owner.login }}" alt="View Owner on GitHub" title="View Owner on GitHub"><span class="fa fa-user-circle"></span>{{ repo.owner.login }}</a>
        <span ng-if="repo.primaryLanguage" class="subtitle" alt="Primary Language" title="Primary Language"><span class="fa fa-code"></span>{{ repo.primaryLanguage.name }}</span>
        <a ng-if="repo.licenseInfo && repo.licenseInfo.spdxId!='NOASSERTION'" class="subtitle" href="{{ repo.licenseInfo.url }}" alt="{{ repo.licenseInfo.name }}" title="{{ repo.licenseInfo.name }}"><span class="fa fa-balance-scale"></span>{{ repo.licenseInfo.spdxId }}</a>
    </h1>

    <p class="stats text-center">
        <a href="{{ repo.url }}">
            <span class="fa fa-github"></span>GitHub Page
        </a>

        <a href="{{ repo.url }}/stargazers">
            <span class="fa fa-star"></span>Stargazers : {{ repo.stargazers.totalCount }}
        </a>

        <a href="{{ repo.url }}/network">
            <span class="fa fa-code-fork"></span>Forks : {{ repo.forks.totalCount }}
        </a>

        <a ng-if="repo.homepageUrl" href="{{ repo.homepageUrl }}">
            <span class="fa fa-globe"></span>Project Website
        </a>
    </p>

    <blockquote ng-if="repo.description" cite="{{ repo.url }}">{{ repo.description }}</blockquote>

    <!-- Preset vis display areas -->
    <center>
        <svg class="repoActivityChart"></svg>
        <br /><svg class="pieUsers"></svg>
        <br /><svg ng-if="count.pulls" class="piePulls"></svg><svg ng-if="count.issues" class="pieIssues"></svg>
        <br /><svg class="repoCreationHistory"></svg>
        <br /><svg ng-if="repo.stargazers.totalCount" class="repoStarHistory"></svg>
        <span ng-if="repo.languages.totalCount || repo.repositoryTopics.totalCount">
            <br /><svg ng-if="repo.languages.totalCount" class="languagePie"></svg><svg ng-if="repo.repositoryTopics.totalCount" class="topicCloud"></svg>
        </span>
    </center>
</div>

{% endraw %}

<!-- Load basic D3 and helper scripts -->
<script src="https://ajax.googleapis.com/ajax/libs/d3js/5.16.0/d3.min.js" charset="UTF-8"></script>
<script type="text/javascript" src="../static/d3-tip/1.0/d3-tip.js"></script>
<script type="text/javascript" src="../static/d3-v4-cloud/1.2.2/build/d3.layout.cloud.js"></script>
<script type="text/javascript" src="../js/visualize/helpers.js"></script>

<!-- Load drawing JS -->
<script type="text/javascript" src="../js/visualize/line_repoActivity.js"></script>
<script type="text/javascript" src="../js/visualize/pie_repoUsers.js"></script>
<script type="text/javascript" src="../js/visualize/pie_repoPulls.js"></script>
<script type="text/javascript" src="../js/visualize/pie_repoIssues.js"></script>
<script type="text/javascript" src="../js/visualize/line_repoCreationHistory.js"></script>
<script type="text/javascript" src="../js/visualize/pie_language.js"></script>
<script type="text/javascript" src="../js/visualize/cloud_topics.js"></script>
<script type="text/javascript" src="../js/visualize/line_repoStarHistory.js"></script>

<script>
    // GiHub Data Directory
    var ghDataDir = '../visualize/github-data';
    // Global chart standards
    var stdTotalWidth = 500,
        stdTotalHeight = 400;
    var stdMargin = { top: 40, right: 40, bottom: 40, left: 40 },
        stdWidth = stdTotalWidth - stdMargin.left - stdMargin.right,
        stdHeight = stdTotalHeight - stdMargin.top - stdMargin.bottom,
        stdMaxBuffer = 1.07;
    var stdDotRadius = 4,
        stdLgndDotRadius = 5,
        stdLgndSpacing = 20;
</script>

<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular.min.js"></script>
<script src="../js/repo/repo-dynamic.js"></script>
