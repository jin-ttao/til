# 브라우저



### 구글에서 Puppeter, Angular를 왜 개발했을까.

* 이번 프로젝트에서 Puppeter를 사용했는데 단순 크롤링을 위해 만든줄 알았다. 알고 보니 크롬 브라우저를 제어하기 위해 만든 것으로 보인다.
*   찾아보니 Puppeteer는 크롬 브라우저를 코드로 조작하려고 만든 도구였음. 크롤링은 그저 부가기능이었고, 실제로는 브라우저에서 일어나는 모든 동작을 자동화하는게 목적이었다. 테스트 자동화, PDF 생성 작업 등 유용하게 쓰임.

    > Puppeteer is a JavaScript library which provides a high-level API to control Chrome or Firefox over the [DevTools Protocol](https://chromedevtools.github.io/devtools-protocol/) or [WebDriver BiDi](https://pptr.dev/webdriver-bidi). Puppeteer runs in the headless (no visible UI) by default but can be configured to run in a visible ("headful") browser.

> "Most things that you can do manually in the browser can be done using Puppeteer" ![daily-puppeteer-feature](../assets/daily-puppeteer-feature.png)

* Puppeteer 공식 문서: https://pptr.dev/guides/what-is-puppeteer
* Chrome DevTools 프로토콜: https://chromedevtools.github.io/devtools-protocol/
