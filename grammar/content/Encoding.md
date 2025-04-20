### Python 支持的文本编码格式

Python 自带了许多内置的编解码器，它们的实现或者是通过 C 函数，或者是通过映射表。 以下表格是按名称排序的编解码器列表，并提供了一些常见别名以及编码格式通常针对的语言。 别名和语言列表都不是详尽无遗的。 请注意仅有大小写区别或使用连字符替代下划线的拼写形式也都是有效的别名；因此，`'utf-8'` 是 `'utf_8'` 编解码器的有效别名。

| 编码            | 别名                                                         | 语言                                               |
| :-------------- | :----------------------------------------------------------- | :------------------------------------------------- |
| ascii           | 646, us-ascii                                                | 英语                                               |
| big5            | big5-tw, csbig5                                              | 繁体中文                                           |
| big5hkscs       | big5-hkscs, hkscs                                            | 繁体中文                                           |
| cp037           | IBM037, IBM039                                               | 英语                                               |
| cp273           | 273, IBM273, csIBM273                                        | 德语*3.4 新版功能.*                                |
| cp424           | EBCDIC-CP-HE, IBM424                                         | 希伯来语                                           |
| cp437           | 437, IBM437                                                  | 英语                                               |
| cp500           | EBCDIC-CP-BE, EBCDIC-CP-CH, IBM500                           | 西欧                                               |
| cp720           |                                                              | 阿拉伯语                                           |
| cp737           |                                                              | 希腊语                                             |
| cp775           | IBM775                                                       | 波罗的海语言                                       |
| cp850           | 850, IBM850                                                  | 西欧                                               |
| cp852           | 852, IBM852                                                  | 中欧和东欧                                         |
| cp855           | 855, IBM855                                                  | 保加利亚语，白俄罗斯语，马其顿语，俄语，塞尔维亚语 |
| cp856           |                                                              | 希伯来语                                           |
| cp857           | 857, IBM857                                                  | 土耳其语                                           |
| cp858           | 858, IBM858                                                  | 西欧                                               |
| cp860           | 860, IBM860                                                  | 葡萄牙语                                           |
| cp861           | 861, CP-IS, IBM861                                           | 冰岛语                                             |
| cp862           | 862, IBM862                                                  | 希伯来语                                           |
| cp863           | 863, IBM863                                                  | 加拿大语                                           |
| cp864           | IBM864                                                       | 阿拉伯语                                           |
| cp865           | 865, IBM865                                                  | 丹麦语/挪威语                                      |
| cp866           | 866, IBM866                                                  | 俄语                                               |
| cp869           | 869, CP-GR, IBM869                                           | 希腊语                                             |
| cp874           |                                                              | 泰语                                               |
| cp875           |                                                              | 希腊语                                             |
| cp932           | 932, ms932, mskanji, ms-kanji                                | 日语                                               |
| cp949           | 949, ms949, uhc                                              | 韩语                                               |
| cp950           | 950, ms950                                                   | 繁体中文                                           |
| cp1006          |                                                              | 乌尔都语                                           |
| cp1026          | ibm1026                                                      | 土耳其语                                           |
| cp1125          | 1125, ibm1125, cp866u, ruscii                                | 乌克兰语*3.4 新版功能.*                            |
| cp1140          | ibm1140                                                      | 西欧                                               |
| cp1250          | windows-1250                                                 | 中欧和东欧                                         |
| cp1251          | windows-1251                                                 | 保加利亚语，白俄罗斯语，马其顿语，俄语，塞尔维亚语 |
| cp1252          | windows-1252                                                 | 西欧                                               |
| cp1253          | windows-1253                                                 | 希腊语                                             |
| cp1254          | windows-1254                                                 | 土耳其语                                           |
| cp1255          | windows-1255                                                 | 希伯来语                                           |
| cp1256          | windows-1256                                                 | 阿拉伯语                                           |
| cp1257          | windows-1257                                                 | 波罗的海语言                                       |
| cp1258          | windows-1258                                                 | 越南语                                             |
| euc_jp          | eucjp, ujis, u-jis                                           | 日语                                               |
| euc_jis_2004    | jisx0213, eucjis2004                                         | 日语                                               |
| euc_jisx0213    | eucjisx0213                                                  | 日语                                               |
| euc_kr          | euckr, korean, ksc5601, ks_c-5601, ks_c-5601-1987, ksx1001, ks_x-1001 | 韩语                                               |
| gb2312          | chinese, csiso58gb231280, euc-cn, euccn, eucgb2312-cn, gb2312-1980, gb2312-80, iso-ir-58 | 简体中文                                           |
| gbk             | 936, cp936, ms936                                            | 统一汉语                                           |
| gb18030         | gb18030-2000                                                 | 统一汉语                                           |
| hz              | hzgb, hz-gb, hz-gb-2312                                      | 简体中文                                           |
| iso2022_jp      | csiso2022jp, iso2022jp, iso-2022-jp                          | 日语                                               |
| iso2022_jp_1    | iso2022jp-1, iso-2022-jp-1                                   | 日语                                               |
| iso2022_jp_2    | iso2022jp-2, iso-2022-jp-2                                   | 日语，韩语，简体中文，西欧，希腊语                 |
| iso2022_jp_2004 | iso2022jp-2004, iso-2022-jp-2004                             | 日语                                               |
| iso2022_jp_3    | iso2022jp-3, iso-2022-jp-3                                   | 日语                                               |
| iso2022_jp_ext  | iso2022jp-ext, iso-2022-jp-ext                               | 日语                                               |
| iso2022_kr      | csiso2022kr, iso2022kr, iso-2022-kr                          | 韩语                                               |
| latin_1         | iso-8859-1, iso8859-1, 8859, cp819, latin, latin1, L1        | 西欧                                               |
| iso8859_2       | iso-8859-2, latin2, L2                                       | 中欧和东欧                                         |
| iso8859_3       | iso-8859-3, latin3, L3                                       | 世界语，马耳他语                                   |
| iso8859_4       | iso-8859-4, latin4, L4                                       | 波罗的海语言                                       |
| iso8859_5       | iso-8859-5, cyrillic                                         | 保加利亚语，白俄罗斯语，马其顿语，俄语，塞尔维亚语 |
| iso8859_6       | iso-8859-6, arabic                                           | 阿拉伯语                                           |
| iso8859_7       | iso-8859-7, greek, greek8                                    | 希腊语                                             |
| iso8859_8       | iso-8859-8, hebrew                                           | 希伯来语                                           |
| iso8859_9       | iso-8859-9, latin5, L5                                       | 土耳其语                                           |
| iso8859_10      | iso-8859-10, latin6, L6                                      | 北欧语言                                           |
| iso8859_11      | iso-8859-11, thai                                            | 泰语                                               |
| iso8859_13      | iso-8859-13, latin7, L7                                      | 波罗的海语言                                       |
| iso8859_14      | iso-8859-14, latin8, L8                                      | 凯尔特语                                           |
| iso8859_15      | iso-8859-15, latin9, L9                                      | 西欧                                               |
| iso8859_16      | iso-8859-16, latin10, L10                                    | 东南欧                                             |
| johab           | cp1361, ms1361                                               | 韩语                                               |
| koi8_r          |                                                              | 俄语                                               |
| koi8_t          |                                                              | 塔吉克*3.5 新版功能.*                              |
| koi8_u          |                                                              | 乌克兰语                                           |
| kz1048          | kz_1048, strk1048_2002, rk1048                               | 哈萨克语*3.5 新版功能.*                            |
| mac_cyrillic    | maccyrillic                                                  | 保加利亚语，白俄罗斯语，马其顿语，俄语，塞尔维亚语 |
| mac_greek       | macgreek                                                     | 希腊语                                             |
| mac_iceland     | maciceland                                                   | 冰岛语                                             |
| mac_latin2      | maclatin2, maccentraleurope, mac_centeuro                    | 中欧和东欧                                         |
| mac_roman       | macroman, macintosh                                          | 西欧                                               |
| mac_turkish     | macturkish                                                   | 土耳其语                                           |
| ptcp154         | csptcp154, pt154, cp154, cyrillic-asian                      | 哈萨克语                                           |
| shift_jis       | csshiftjis, shiftjis, sjis, s_jis                            | 日语                                               |
| shift_jis_2004  | shiftjis2004, sjis_2004, sjis2004                            | 日语                                               |
| shift_jisx0213  | shiftjisx0213, sjisx0213, s_jisx0213                         | 日语                                               |
| utf_32          | U32, utf32                                                   | 所有语言                                           |
| utf_32_be       | UTF-32BE                                                     | 所有语言                                           |
| utf_32_le       | UTF-32LE                                                     | 所有语言                                           |
| utf_16          | U16, utf16                                                   | 所有语言                                           |
| utf_16_be       | UTF-16BE                                                     | 所有语言                                           |
| utf_16_le       | UTF-16LE                                                     | 所有语言                                           |
| utf_7           | U7, unicode-1-1-utf-7                                        | 所有语言                                           |
| utf_8           | U8, UTF, utf8, cp65001                                       | 所有语言                                           |
| utf_8_sig       |                                                              | 所有语言                                           |