# google-search

> [https://ahrefs.com/blog/google-advanced-search-operators/](https://ahrefs.com/blog/google-advanced-search-operators/)

| 示例                                                       | 描述                           |
| -------------------------------------------------------- | ---------------------------- |
| <p>X <strong>OR</strong> Y<br>X <strong>|</strong> Y</p> | 匹配`X`或`Y`                    |
| X **AND** Y                                              | 同时满足`X`和`Y`                  |
| X -Y                                                     | 满足`X`、不满足`Y`                 |
| X **\*** Y                                               | `*` 作为通配符，匹配任意单词             |
| (X OR Y) Z                                               | 组合使用                         |
| ipad $329                                                | 搜索价格                         |
| cache:apple.com                                          | 返回网页的最新缓存版本                  |
| <p>filename filetype:pdf<br>filename ext:pdf</p>         | 结果限定为特定文件类型                  |
| site:apple.com                                           | 结果限定为特定站点内                   |
| related:apple.com                                        | 与指定站点相关                      |
| intitle:keyword                                          | 网页title标签内包含给定的单词            |
| allintitle:keyword1 keyword2                             | 网页title标签内包含所有给定的单词          |
| inurl:keyword                                            | url内包含给定的单词                  |
| allinurl:keyword1 keyword2                               | url内包含给定的单词                  |
| intext:keyword                                           | 网页内包含给定的单词                   |
| allintext:keyword1 keyword2                              | 网页内包含所有给定的单词                 |
| X AROUND(4) Y                                            | X 和 Y之间不超过四个单词的间隔            |
| weather:location                                         | 查询某个地点的天气                    |
| stocks:company                                           | 查询某个公司的股票                    |
| map:location                                             | 查询某个地点的地图信息                  |
| movie:keyword                                            | 包含指定关键词的电影                   |
| $1 in chinese yuan                                       | 使用 `in` 关键字进行单位转换（货币，重量，维度等） |
| keyword source:organization                              | 在谷歌news中查找来自某个来源的新闻结果        |
