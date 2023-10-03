---
title: "認識一下 GitLab CI"
date: 2023-10-03T23:29:49+08:00
draft: true
tags: ["note"]
---

## Before
其實之前有嘗試過，但在本地測試遇到一些問題，  
僅止於建好 runner 但 hook 失敗就先暫緩。  

## 概念
簡單說就是把你測試部署等的動作都自動化，  
又，剛好你是使用 GitaLab 那還不試試看？

## GitLab runner
就像幫你做事的工頭，你在 GitLab 觸發流程，發包給他們工作。  

## .gitlab-ci.yml
給剛剛上面那個工頭的計畫書，說明該用什麼做什麼。

## 所以可以先從哪開始？
個人第一步是：先建立 runner  
依照官方文件，在 docker 跑 runner 本體  
```
docker run -d --name gitlab-runner --restart always \
  -v /srv/gitlab-runner/config:/etc/gitlab-runner \
  -v /var/run/docker.sock:/var/run/docker.sock \
  gitlab/gitlab-runner:latest
```


註冊新的 runner 用以和你的專案 hook  
```
docker run --rm -it -v gitlab-runner-config:/etc/gitlab-runner gitlab/gitlab-runner:latest register
```


