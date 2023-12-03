---
layout: '../../layouts/ProseLayout.astro'
title: "How I Fixed GitHub's Repo Traffic Insights"
---

## Start of the journey

If you are a developer sharing projects on GitHub, you are probably familiar with Github's repository traffic insights that looks like this:

![chart1](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/46sly49h18ls281xy6gb.png)

This feature, while useful, has its limitations. The most notable issues include a 14-day limit on data retention and a chart that can be confusing due to varying scales for each type of data.

While looking for solutions, I realized that many developers face similar challenges. This issue is widely discussed, particularly in a GitHub thread: [Track traffic to GitHub repo longer than 14 days #399](https://github.com/isaacs/github/issues/399).

## Exploring alternatives

Within the discussion, I came across a [GitHub action tool](https://github.com/jgehrcke/github-repo-stats) that fetches traffic data and stores it in a CSV file, also generating a PDF report:
![image](https://github.com/m4xshen/img-host/assets/74842863/e2b7655d-6be5-491c-998f-50f919847da2)

Now the first problem is solved! I can view my traffic data more than 14 days, which is a significant improvement.

However, it doesn't solve the issues of chart clarity and user interface at all, and it adds the complexity of setup and accessibility.

This is because, as a GitHub action, it required me to configure the workflow file manually. Also, the output being in PDF format made it less accessible and harder to interact with.

## Crafting my own solution

After reflecting on these experiences, I listed out what my ideal tool would look like:
1. Data access extending beyond 14 days
2. Intuitive chart design
3. Enhanced user interface
4. Simple setup and accessibility

I keep searching tools like this but none of them meets all the requirements. So I decided to build my own!

After few months of working, I finally finished my own tool called [Repohistory](https://github.com/repohistory/repohistory):

![screenshot of Repohistory](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/q0seycrd9uapb842x314.png)

Here's the approach I took to fulfill all the 4 requirements.

### Showing data more than 14 days

It fetches traffic data with GitHub API and stores them in Supabase. This is run on the first intsallation and also twice a day with cron job to keep the data up to date.

### Intuitive chart design

I replace the line chart with stacked bar chart that make more sense for data because unique views is a part of the total views.

### Enhanced UI

I redesign the whole UI in a modern way and built them with chart.js, NextUI and Tailwind CSS.

### Easy to setup and access

I integrates GitHub Apps into [Repohistory](https://github.com/repohistory/repohistory), so that user only need to login, install and select the repo they want to track, then it is good to go.

Thanks for watching to the end! That's pretty much my journey of building my own tool to fix the GitHub's repo traffic insights! If you find this tool useful, feel free to check it out on [GitHub](https://github.com/repohistory/repohistory)!
