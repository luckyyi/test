# Errors
- Parse error: syntax error, unexpected end of file in '...'
  - 如果你使用了标签, 那在你的 php.ini 里的这一项, 把 `off` 改成 `on`
    - short_open_tag = Off
- 如果找不到Soap时
  - 打开php.ini，修改下面这行，把;去掉
  - ;extension=php_soap.dll


- <? $j=1; ?>这种不生效
  - 写成<?php $j=1; ?>这样才行。
  - 是因为没有开启短标识，需要在php.ini中修改short_open_tag = On打开短标识。但是不推荐这样做，因为用<?php ?>你永远不会出问题;而用<? ?>会可能出问题，例如：配置文件没有开启短标识，例如<?xml version="1.0" ?>会被当作php，而且，PHP本来是计划在PHP6中去掉短标识的，所以以后的版本可能会不支持短标识。


- QA环境
  - nginx + php
  - 重启php用  /etc/init.d/php-fpm restart
