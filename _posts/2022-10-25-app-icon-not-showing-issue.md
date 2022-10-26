---
title: 서버에서 앱 아이콘이 보이지 않는 경우
author:
  name: Park Jihee
  link: https://github.com/park-jihee
date: 2022-10-25 11:00:00 +0900
categories: [Odoo, issue]
tags: [odoo, issue, server]
---

# 이슈

서버 메인페이지에서 앱 아이콘들이 보이지 않는 경우에 대한 해결 방안입니다.

![서버에서 앱 아이콘이 보이지 않는 경우 1](/assets/img/2022-10-25-app-icon-not-showing-issue/01.png)

# 해결 방안

## #1

정상적으로 앱 아이콘 보이는 동일한 버전의 데이터베이스로 이동합니다.

*설정 > 기술 > 사용자 인터페이스 > 메뉴 항목* 을 클릭합니다.

⚠️  기술 메뉴가 보이지 않을시 odoo debug 모드를 활성화합니다.

![서버에서 앱 아이콘이 보이지 않는 경우 2](/assets/img/2022-10-25-app-icon-not-showing-issue/02.png)

## #2

앱 아이콘이 보이지 않는 모듈명(판매)을 검색한 후 해당 메뉴 정보를 클릭합니다.

정상적으로 앱 아이콘이 보이는 데이터베이스라면 웹 아이콘 이미지를 다운받을 수 있습니다.

다운로드 버튼을 클릭하여 앱 아이콘을 다운받습니다.

![서버에서 앱 아이콘이 보이지 않는 경우 3](/assets/img/2022-10-25-app-icon-not-showing-issue/03.png)

## #3

다운받은 파일을 확인해보면 판매 앱의 아이콘이 다운로드된 것을 확인할 수 있습니다.

![서버에서 앱 아이콘이 보이지 않는 경우 4](/assets/img/2022-10-25-app-icon-not-showing-issue/04.png)

## #4

이제 다시 앱 아이콘이 보이지 않는 데이터베이스로 돌아와서 판매 메뉴 정보로 이동합니다.

여기서는 웹 아이콘 이미지가 없는 걸 알 수 있는데 파일 업로드를 통해 아까 다운받은 이미지를 업로드합니다.

![서버에서 앱 아이콘이 보이지 않는 경우 5](/assets/img/2022-10-25-app-icon-not-showing-issue/05.png)

## #5

메인화면으로 돌아와 새로고침을 해보면 정상적으로 앱 아이콘이 보이게 됩니다.

![서버에서 앱 아이콘이 보이지 않는 경우 6](/assets/img/2022-10-25-app-icon-not-showing-issue/06.png)

# 마치며, 🙇🏻

## 참고한 사이트

[https://probuse.com/blog/probuse-odoo-apps-25/post/odoo-menu-icons-not-showing-issue-1003](https://probuse.com/blog/probuse-odoo-apps-25/post/odoo-menu-icons-not-showing-issue-1003){:target="_blank"}
