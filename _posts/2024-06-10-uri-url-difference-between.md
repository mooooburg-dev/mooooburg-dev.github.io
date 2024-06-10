---
layout: post
title: URI와 URL
description: 미묘하지만 중요한 차이점을 가진 URI와 URL
date: 2024-06-10
published : true
categories: network
---

URI(Uniform Resource Identifier)와 URL(Uniform Resource Locator)의 차이점은 기술적인 측면에서 다소 미묘하지만 중요한 차이입니다. 이 둘을 이해하기 위해서는 각 개념의 정의를 아는 것이 중요합니다.

### URI (Uniform Resource Identifier)
URI는 인터넷에서 자원을 식별하는 문자열입니다. URI는 두 가지 주요 형태로 나눌 수 있습니다:
1. **URL (Uniform Resource Locator)**: 자원의 위치를 나타내는 URI입니다.
2. **URN (Uniform Resource Name)**: 자원의 이름을 나타내며, 위치에 독립적입니다.

URI는 자원의 식별을 위한 일반적인 개념을 포함하며, 특정한 리소스를 가리키기 위한 다양한 방법을 허용합니다.

예:
- URL: `https://www.example.com`
- URN: `urn:isbn:0451450523`

### URL (Uniform Resource Locator)
URL은 자원의 위치를 지정하는 URI의 한 형태입니다. URL은 자원의 접근 방법(스킴)과 자원이 위치한 네트워크 상의 위치를 포함합니다.

URL의 구성 요소:
- **스킴(scheme)**: `http`, `https`, `ftp` 등 자원에 접근하는 방법을 정의합니다.
- **호스트(host)**: 자원이 위치한 서버의 주소입니다 (예: `www.example.com`).
- **경로(path)**: 서버 내 자원의 위치를 지정합니다 (예: `/path/to/resource`).
- **쿼리 문자열(query string)**: 추가적인 매개변수를 포함합니다 (예: `?id=123`).

예:
- `https://www.example.com/path/to/resource?id=123`

### 주요 차이점
- **포괄성**: URI는 자원을 식별하는 모든 것을 포함하는 반면, URL은 자원의 위치를 구체적으로 나타냅니다. 모든 URL은 URI이지만, 모든 URI가 URL은 아닙니다.
- **사용 목적**: URL은 주로 웹 브라우저가 특정 자원을 찾고 접근하는 데 사용됩니다. 반면에 URI는 자원을 고유하게 식별하는 데 사용됩니다.

### 요약
- **URI**: 자원을 식별하는 모든 문자열.
- **URL**: 자원의 위치를 지정하는 URI의 한 형태.

이러한 차이를 이해하면 웹 개발이나 인터넷 기술을 사용할 때 더 정확한 용어를 사용할 수 있습니다. 


