# Shallow & Deep

<!-- toc -->

- [맥락](#%EB%A7%A5%EB%9D%BD)

<!-- tocstop -->

# 맥락

- 팀플에서 객체간 비교하는데 알고보니 의도가 있었음. https://github.com/Team-Bloblow/Bloblow-Client/pull/68#discussion_r1899049987
- https://betterprogramming.pub/why-you-shouldnt-use-json-stringify-to-compare-objects-in-javascript-c9a16b7331e
- https://velog.io/@neighborkim/%EC%96%95%EC%9D%80-%EB%B9%84%EA%B5%90Shallow-Compare-%EC%99%80-%EA%B9%8A%EC%9D%80-%EB%B9%84%EA%B5%90Deep-Compare

```js
const items = [];
const DEFAULT_FILTER_LIST = {
  order: "NEWEST",
  includedKeyword: [],
  excludedKeyword: [],
  isAd: "",
};
const filterList = {
  order: "NEWEST",
  includedKeyword: [],
  excludedKeyword: [],
  isAd: "",
};
console.log(DEFAULT_FILTER_LIST === filterList);
$$;

// as-is
const hasNotPostResponseForFirstRequest = filterList === DEFAULT_FILTER_LIST && items?.length === 0;
console.log(hasNotPostResponseForFirstRequest);

// to-be
const hasPostResponseForFirstRequest =
  JSON.stringify(filterList) === JSON.stringify(DEFAULT_FILTER_LIST) && items?.length === 0;
console.log(hasPostResponseForFirstRequest);
console.log(JSON.stringify(filterList));

const checkDefaultFilter = (filter) => {
  const defaultIncludedLength = DEFAULT_FILTER_LIST.includedKeyword.length;
  const defaultExcludedLength = DEFAULT_FILTER_LIST.excludedKeyword.length;

  if (filter.order !== DEFAULT_FILTER_LIST.order) return false;
  if (
    filter.includedKeyword.length !== defaultIncludedLength ||
    filter.excludedKeyword.length !== defaultExcludedLength
  )
    return false;
  if (filter.isAd !== DEFAULT_FILTER_LIST.isAd) return false;

  return true;
};

checkDefaultFilter(filterList);
```
