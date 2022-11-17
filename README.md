# azure-tts-lexicon-cn

![ci](https://github.com/wxxxcxx/azure-tts-lexicon-cn/actions/workflows/ci.yaml/badge.svg)

适用于 Azure Text to Speech 服务的简体中文词典。

Azure TTS 服务的声音真的非常接近真实的人类了，但是对于中文的一些多音字还是识别的不够准确。幸运的是可以使用自定义词典来弥补这个缺陷。

Azure TTS 服务支持在 SSML 标记中嵌入词典文件链接的方式使用词典。但是这要求词典文件必须可以被互联网访问，考虑到微软服务器的延迟，想来想去还是放在 Github 上比较合适。这样也方便于同大家一起来丰富词典的内容。

## 使用

词典文件的链接为：
```
https://raw.githubusercontent.com/wxxxcxx/azure-tts-lexicon-cn/main/lexicon.xml
```

在 SSML 中使用词典文件：
``` xml
<speak version="1.0" xmlns="http://www.w3.org/2001/10/synthesis"
          xmlns:mstts="http://www.w3.org/2001/mstts"
          xml:lang="en-US">
    <voice name="zh-CN-XiaoxiaoNeural">
        <lexicon uri="https://raw.githubusercontent.com/wxxxcxx/azure-tts-lexicon-cn/main/lexicon.xml"/>
        等一会儿，朱重八！
    </voice>
</speak>
```

更多细节请参考：https://learn.microsoft.com/zh-cn/azure/cognitive-services/speech-service/speech-synthesis-markup#use-custom-lexicon-to-improve-pronunciation。


## 贡献

如果发现 TTS 有哪个词发音不对的话可以通过 issue 的方式告诉我，我看到了会加上去的。

考虑到作者合并PR和更新可能不是那么及时，有自定义词典需求的用户可以考虑 Fork 一份自己修改。

需要修改的文件为 [lexicon.xml](lexicon.xml)。规则应该还算比较好懂，看看现有的例子应该就能明白。

更多细节也可以参考微软官方的文档：https://learn.microsoft.com/zh-cn/azure/cognitive-services/speech-service/speech-synthesis-markup#use-custom-lexicon-to-improve-pronunciation。

需要注意的是使用自己 Fork 的时词典别忘了将链接中的`<用户名>`为修改为你自己的。
```
https://raw.githubusercontent.com/<用户名>/azure-tts-lexicon-cn/main/lexicon.xml
```

另外欢迎提交 PR 哦。

### Tips

- 每次修改词典文件并提交后，可以留意下 Github Action 中的集成测试是否验证通过了词典文件（显示小绿点）。如果显示的是小红点的话，可以根据错误的步骤的提示进行修改。

- 根据文档说明，为了防止每次请求都要重新下载词典文件，微软服务器会缓存词典文件15分钟。如果测试时希望立即更新缓存，可以在链接末尾加上类似于 `?asdjl` 以问号开头的随机字符串。
