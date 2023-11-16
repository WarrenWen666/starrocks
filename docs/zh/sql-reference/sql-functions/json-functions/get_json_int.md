---
displayed_sidebar: "Chinese"
---

# get_json_int

## description

### Syntax

```Haskell
INT get_json_int(VARCHAR json_str, VARCHAR json_path)
```

解析并获取 json 字符串内指定路径的整型内容。
其中 json_path 必须以 $ 符号作为开头，使用 . 作为路径分割符。如果路径中包含 . ，则可以使用双引号包围。
使用 [ ] 表示数组下标，从 0 开始。
path 的内容不能包含 ", [ 和 ]。
如果 json_string 格式不对，或 json_path 格式不对，或无法找到匹配项，则返回 NULL。

## example

1. 获取 key 为 "k1" 的 value

    ```Plain Text
    MySQL > SELECT get_json_int('{"k1":1, "k2":"2"}', "$.k1");
    +--------------------------------------------+
    | get_json_int('{"k1":1, "k2":"2"}', '$.k1') |
    +--------------------------------------------+
    |                                          1 |
    +--------------------------------------------+
    ```

2. 获取 key 为 "my.key" 的数组中第二个元素

    ```Plain Text
    MySQL > SELECT get_json_int('{"k1":"v1", "my.key":[1, 2, 3]}', '$."my.key"[1]');
    +------------------------------------------------------------------+
    | get_json_int('{"k1":"v1", "my.key":[1, 2, 3]}', '$."my.key"[1]') |
    +------------------------------------------------------------------+
    |                                                                2 |
    +------------------------------------------------------------------+
    ```

3. 获取二级路径为 k1.key -> k2 的数组中，第一个元素

    ```Plain Text
    MySQL > SELECT get_json_int('{"k1.key":{"k2":[1, 2]}}', '$."k1.key".k2[0]');
    +--------------------------------------------------------------+
    | get_json_int('{"k1.key":{"k2":[1, 2]}}', '$."k1.key".k2[0]') |
    +--------------------------------------------------------------+
    |                                                            1 |
    +--------------------------------------------------------------+
    ```

## keyword

GET_JSON_INT,GET,JSON,INT