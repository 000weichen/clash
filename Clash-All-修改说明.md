# Clash-All.ini 修改说明

## 原文件主要问题

1. **原文件只有一行**
   - 原文件从 GitHub Raw 读取时显示 `Total lines: 1`。
   - 这会导致注释、规则、策略组全部挤在一起，subconverter 很容易解析失败。

2. **缺少 `[custom]` 段头**
   - subconverter 外部配置通常需要 `[custom]` 段。
   - 已在文件最前面补上。

3. **开头是 `;1、域名组`**
   - `;` 在 ini 里是注释符。
   - 原文件整行都被压在这个注释后面，等于后续内容存在被当注释吞掉的风险。

4. **部分 ruleset 多了一个逗号**
   - 原来类似：
     ```ini
     ruleset=✨ AI,,https://...
     ```
   - 已改成：
     ```ini
     ruleset=✨ AI,https://...
     ```

5. **策略组名称有多余空格和异常符号**
   - 原来有：
     ```ini
     ruleset= GitHub,...
     custom_proxy_group= GitHub`select`...
     ```
   - 已改成：
     ```ini
     ruleset=GitHub,...
     custom_proxy_group=GitHub`select`...
     ```

6. **HBO / 虚拟币规则被注释，但策略组仍启用**
   - 原来 HBO 和虚拟币规则是注释状态，但策略组还在。
   - 我把对应策略组也先注释掉，避免生成无用策略组。
   - 如果你后续要启用 HBO 或虚拟币，规则集和策略组要一起取消注释。

7. **节点正则里有重复空条件**
   - 原来有很多类似：
     ```ini
     Hong Kong||HongKong
     Tai Wan|||TaiWan
     ```
   - 已清理为：
     ```ini
     Hong Kong|HongKong
     Tai Wan|TaiWan
     ```

## 你订阅链接建议同步修改

FlClash 建议不要用：

```txt
target=clashr
```

建议改成：

```txt
target=clash
```

也就是你的订阅转换链接里，把：

```txt
target=clashr
```

替换为：

```txt
target=clash
```

## 文件使用方式

把 `Clash-All-fixed.ini` 上传到你的 GitHub 仓库，替换原来的 `Cash-All.ini` 或 `Clash-All.ini`。

然后订阅链接里的 `config=` 指向新的 Raw 地址，例如：

```txt
config=https%3A%2F%2Fraw.githubusercontent.com%2F000weichen%2Fclash%2Frefs%2Fheads%2Fmain%2FCash-All.ini
```

如果你重命名成 `Clash-All.ini`，那就把最后文件名也改掉。
