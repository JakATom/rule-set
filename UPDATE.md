- 2026-03-03：
  * 新增几个自己常用的规则集：
  * 1️⃣
  * 在`- name: Download surge ruleset`步骤
  * ```
    # 1. surge_lists中增加 'AliPay' 'XiaoMi'

    # 2. 在 `cp "${bm7_surge}/${list}/${list}.list" "download/surge/${list}.list"`循环外增加
    # 这一步本该和第1步在一起，但是alibaba这个规则集目录下的文件内容和其他的不一样。所以独立处理
    surge_alibaba='Alibaba'
    cp "${bm7_surge}/${surge_alibaba}/Alibaba_All.list" "download/surge/${surge_alibaba}.list"

    # 3. 在files中增加如下，其中 video-cn warp tor 是自用的规则，WeChat原本应该和第1步一起，但是surge目录下的规则有很多异常。
    'video-cn.list https://github.com/JakATom/DE_SSSProfile/raw/refs/heads/newone/newone/DESSS/Video_CN.list'
    'warp.list https://github.com/JakATom/DE_SSSProfile/raw/refs/heads/newone/newone/DESSS/warp.list'
    'tor.list https://github.com/JakATom/DE_SSSProfile/raw/refs/heads/newone/newone/DESSS/tor.list'
    'WeChat.list https://github.com/blackmatrix7/ios_rule_script/raw/refs/heads/master/rule/Loon/WeChat/WeChat.list'
    ```
  * 2️⃣
  * 在`- name: Merge httpdns file`下，新增生成 warp 和 tor 的独立`规则名称`
    ```
          - name: Merge warp file
        run: |
          cat 'download/surge/warp.list' \
          > meta/warp.list

      - name: Merge tor file
        run: |
          cat 'download/surge/tor.list' \
          > meta/tor.list
    ```
  * 3️⃣
  * 在`- name: Merge socialmedia-cn file`下将如下假如到 `socialmedia-cn` 规则名称下。
    ```
              'download/surge/WeChat.list' \
              'download/surge/AliPay.list' \
              'download/surge/XiaoMi.list' \
              'download/surge/Alibaba.list' \
              'download/surge/video-cn.list' \
    ```
