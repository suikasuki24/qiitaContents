---
title: 【Windows】 WordPress+LocalにてZip形式のテーマが「一時フォルダーが見つかりません。」となってインストールできないとき
tags:
  - WordPress
private: false
updated_at: '2023-10-01T07:09:21+09:00'
id: 3d0e96fc989c9569462b
organization_url_name: null
slide: false
ignorePublish: false
---
# 原因
ググると色々な原因があるようですが、自分の場合は以下が原因でした。
同じような状況の方は確認してみると良いかもです。

以下のファイルの先頭に
```
Local Sites/[projectname]/conf/php/php.ini.hbs
```
以下のような記述があり、
```:php.ini.hbs
{{#if os.windows}}
extension_dir="{{extensionsDir}}"
sys_temp_dir="C:\Windows\TEMP"
{{/if}}
```
自分はSSD交換時にOSパーティションのクローンを行っており、OSのインストールパーティションのドライブ文字がHだったため、
```
sys_temp_dir="H:\Windows\TEMP"
```
と修正し、Local上で`Stop site` -> `Start site`とすることでZip形式のテーマがインストールできました。
