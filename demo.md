# NowShowTime JS 订阅开发完整规范

本规范适用于所有为 NowShowTime App 开发 JS 订阅脚本的开发者，涵盖所有支持的标准方法、参数、返回值、特殊说明，确保脚本能被 App 正确识别和调用。

---

## 1. 必须/可选实现的 JS 方法一览

| 方法名                  | 说明                                   | 适用场景           |
|------------------------|----------------------------------------|--------------------|
| getWebsiteInfo         | 返回网站基本信息（名称、icon等）        | 必须               |
| getCategories          | 返回分类列表                           | 必须（有分类时）   |
| getSortOptions         | 返回排序选项                           | 可选               |
| getVideoList           | 获取首页/推荐视频列表                   | 必须           |
| getVideosByCategory    | 获取指定分类下视频列表                  | 建议实现           |
| getVideoDetail         | 获取视频详情及分辨率                    | 必须               |
| getPlayUrl             | 解析真实播放地址（如需二次解析时实现）   | 可选               |
| search                 | 搜索视频                               | 建议实现           |

---

## 2. 方法参数与返回值规范

### getWebsiteInfo
- 返回：
```js
{
  name: "站点名称",
  description: "描述",
  icon: "https://.../favicon.ico",
  homepage: "https://..."
}
```

### getCategories
- 返回：
```js
[
  { id: '1', name: '分类A', ext: { url: 'https://.../catA' } },
  { id: '2', name: '分类B', ext: { url: 'https://.../catB' } }
]
```

### getSortOptions
- 返回：
```js
{
  key: 'sort',
  name: '排序',
  init: 'default',
  value: [
    { n: '最新', v: 'new' },
    { n: '最热', v: 'hot' }
  ]
}
```

### getVideoList(page)
- 参数：page（页码，数字）
- 返回：
```js
[
  {
    id: '唯一ID',
    title: '标题',
    cover: '封面URL',
    url: '详情页URL',
    description: '描述',
    createTime: 1234567890
  }
]
```

### getVideosByCategory(categoryId, page, sort)
- 参数：categoryId（分类ID，字符串），page（页码，数字），sort（排序key，字符串，可选）
- 返回：同 getVideoList

### getVideoDetail(videoId, url)
- 参数：videoId（视频ID，字符串），url（可选，详情页URL）
- 返回：
```js
{
  id: videoId,
  title: '标题',
  cover: '封面URL',
  description: '描述',
  resolutions: [
    { id: 'auto', name: '自动', url: 'm3u8地址', size: '未知' },
    { id: '720p', name: '720P', url: 'm3u8地址', size: '未知' }
  ]
}
```

### getPlayUrl(episodeUrl)
- 参数：episodeUrl（分辨率url或集数页面url）
- 返回：
  - 字符串（最终可播直链）或
  - 对象：{ url: '...' }

### search(keyword, page)
- 参数：keyword（关键词，字符串），page（页码，数字）
- 返回：同 getVideoList

---

## 3. 其它开发规范

- 所有方法必须为 async/Promise 风格，返回 JS 基础类型（对象/数组/字符串/数字）。
- 网络请求统一用 $fetch.get/$fetch.post，支持自定义 headers。
- 推荐使用 cheerio 解析 HTML。
- User-Agent 建议模拟 iPhone Safari。
- 分类、排序等可用脚本内变量缓存，避免重复请求。
- 所有网络请求需加异常处理，避免抛出未捕获异常导致 App 崩溃。
- 多分类/并发搜索可参考并发 Promise 实现。

---

## 4. 参考模板（已脱敏）

```js
const UA = 'Mozilla/5.0 (iPhone; CPU iPhone OS 17_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.0 Mobile/15E148 Safari/604.1';
const cheerio = createCheerio();
const SITE = 'https://example.com'; // 站点根地址

// 分类缓存
let tabsCache = null;

// 基础请求头
const baseHeaders = {
  'User-Agent': UA,
  'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8',
  'Referer': SITE + '/',
  'Origin': SITE,
};

// 获取站点信息
async function getWebsiteInfo() {
  return {
    name: "示例站点",
    description: "示例描述",
    icon: SITE + "/favicon.ico",
    homepage: SITE
  };
}

// 获取分类
async function getCategories() {
  if (tabsCache) return tabsCache;
  const tabs = [
    { name: '分类1', ext: { url: SITE + '/cat1' } },
    { name: '分类2', ext: { url: SITE + '/cat2' } }
  ];
  tabsCache = tabs.map((tab, idx) => ({
    id: String(idx + 1),
    name: tab.name,
    ext: tab.ext,
  }));
  return tabsCache;
}

// 排序选项
async function getSortOptions() {
  return {
    key: 'sort',
    name: '排序',
    init: 'default',
    value: [
      { n: '最新', v: 'new' },
      { n: '最热', v: 'hot' }
    ],
  };
}

// 获取视频列表
async function getVideosByCategory(categoryId, page, sort) {
  const categories = await getCategories();
  const category = categories.find(item => item.id === String(categoryId));
  const categoryUrl = category && category.ext ? category.ext.url : SITE + '/cat1';
  return getVideoList(page, categoryUrl, sort);
}

async function getVideoList(page, categoryUrl, sort) {
  const currentPage = page || 1;
  let baseUrl = categoryUrl || `${SITE}/cat1`;
  baseUrl += `?sort=${sort || 'new'}&page=${currentPage}`;
  const { data } = await $fetch.get(baseUrl, { headers: baseHeaders, userAgent: UA });
  const $ = cheerio.load(data || '');
  let list = [];
  $('.video-item').each((_, e) => {
    const href = $(e).find('a').attr('href');
    const title = $(e).find('.title').text().trim();
    const cover = $(e).find('img').attr('src');
    list.push({
      id: href,
      title: title || '未知标题',
      cover: cover || '',
      url: href,
      description: '',
      createTime: Date.now()
    });
  });
  return list;
}

// 获取视频详情
async function getVideoDetail(videoId) {
  const url = videoId;
  const { data } = await $fetch.get(url, { headers: baseHeaders, userAgent: UA });
  const $ = cheerio.load(data || '');
  const title = $('h1').text().trim() || '视频标题';
  const cover = $('video').attr('poster') || '';
  let resolutions = [
    { id: 'auto', name: '自动', url: 'm3u8地址', size: "未知" }
  ];
  return {
    id: videoId,
    title,
    cover,
    description: '',
    resolutions
  };
}

// 搜索
async function search(keyword, page) {
  const text = encodeURIComponent(keyword);
  const currentPage = page || 1;
  const searchUrl = `${SITE}/search/${text}?page=${currentPage}`;
  const { data } = await $fetch.get(searchUrl, { headers: baseHeaders, userAgent: UA });
  const $ = cheerio.load(data || '');
  let list = [];
  $('.video-item').each((_, e) => {
    const href = $(e).find('a').attr('href');
    const title = $(e).find('.title').text().trim();
    const cover = $(e).find('img').attr('src');
    list.push({
      id: href,
      title: title || '未知标题',
      cover: cover || '',
      url: href,
      description: '',
      createTime: Date.now()
    });
  });
  return list;
}
```

---

## 5. 常见问题

- **必须实现哪些方法？**
  - getWebsiteInfo、getVideoDetail 必须实现。
  - 有分类时必须实现 getCategories。
  - 其它方法建议实现，能提升体验。
- **getPlayUrl 必须实现吗？**
  - 仅当播放地址需二次解析时实现，否则可省略。

---

如有疑问请联系主项目维护者。
