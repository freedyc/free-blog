---
title: HardSourceWebpackPlugin 内存溢出
date:  2020-12-11 11:08:59
tags: nodejs
comments: true
---


# HardSourceWebpackPlugin 内存溢出

开发模式下经过一天的 dev 最终突然无法访问了， 后一看命令行报如下错误，发现内存溢出了

```bash

[hardsource:19a950bb] Using 326 MB of disk space.
94% after seal[hardsource:19a950bb] Could not freeze ./assets/stylesheets/zddi.scss: Cannot read property 'hash' of undefined
[hardsource:19a950bb] Could not freeze ./node_modules/@dengyongchao/modal/modal.scss: Cannot read property 'hash' of undefined
95% emitting HtmlWebpackPlugin
<--- Last few GCs --->

[52718:0x10286b000] 13503751 ms: Mark-sweep 1364.3 (1403.4) -> 1364.2 (1403.4) MB, 493.1 / 0.1 ms  (average mu = 0.248, current mu = 0.000) last resort GC in old space requested
[52718:0x10286b000] 13504247 ms: Mark-sweep 1364.2 (1403.4) -> 1364.2 (1403.4) MB, 495.7 / 0.1 ms  (average mu = 0.142, current mu = 0.000) last resort GC in old space requested


<--- JS stacktrace --->

==== JS stack trace =========================================

    0: ExitFrame [pc: 0x2d8c53e878a1]
Security context: 0x155e5e79e6c1 <JSObject>
    1: byteLength(aka byteLength) [0x155ebfdfa7b9] [buffer.js:~509] [pc=0x2d8c54ca5567](this=0x155e775026f1 <undefined>,string=0x155e86cb5ee9 <Very long string[10165335]>,encoding=0x155e5e7be9b1 <String[4]: utf8>)
    2: arguments adaptor frame: 3->2
    3: from [0x155e607a0d59] [buffer.js:~199] [pc=0x2d8c54cf8c6c](this=0x155ebfdd4181 <JSFunction Buffer (sfi...

FATAL ERROR: CALL_AND_RETRY_LAST Allocation failed - JavaScript heap out of memory
 1: 0x100d68631 node::Abort() (.cold.1) [/usr/local/bin/node]
 2: 0x10003aeb2 node_module_register [/usr/local/bin/node]
 3: 0x10003b073 node::OnFatalError(char const*, char const*) [/usr/local/bin/node]
 4: 0x1001a9197 v8::Utils::ReportOOMFailure(v8::internal::Isolate*, char const*, bool) [/usr/local/bin/node]
 5: 0x1001a9131 v8::internal::V8::FatalProcessOutOfMemory(v8::internal::Isolate*, char const*, bool) [/usr/local/bin/node]
 6: 0x100593692 v8::internal::Heap::FatalProcessOutOfMemory(char const*) [/usr/local/bin/node]
 7: 0x10059ce55 v8::internal::Heap::AllocateRawWithRetryOrFail(int, v8::internal::AllocationSpace, v8::internal::AllocationAlignment) [/usr/local/bin/node]
 8: 0x10056f6f3 v8::internal::Factory::NewRawTwoByteString(int, v8::internal::PretenureFlag) [/usr/local/bin/node]
 9: 0x1006a8952 v8::internal::String::SlowFlatten(v8::internal::Handle<v8::internal::ConsString>, v8::internal::PretenureFlag) [/usr/local/bin/node]
10: 0x1001c97c0 v8::String::Utf8Length() const [/usr/local/bin/node]
11: 0x10004c9e0 node::Buffer::(anonymous namespace)::ByteLengthUtf8(v8::FunctionCallbackInfo<v8::Value> const&) [/usr/local/bin/node]
12: 0x2d8c53e878a1
13: 0x2d8c54ca5567
14: 0x2d8c53e8a5c3
error Command failed with signal "SIGABRT".
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.


Version: webpack 4.44.2
Time: 4624ms
Built at: 2020-12-11 10:44:07 AM
                                    Asset      Size  Chunks                                      Chunk Names
                                   app.js  4.43 MiB     app  [emitted]                    [big]  app
     fc7b2a59864448e6c572.hot-update.json  48 bytes          [emitted] [immutable] [hmr]
master.fc7b2a59864448e6c572.hot-update.js  4.12 KiB  master  [emitted] [immutable] [hmr]         master
                                master.js  9.71 MiB  master  [emitted]                    [big]  master
 + 3 hidden assets
Entrypoint app [big] = app.css app.js
[./assets/javascripts/zddi/am/dhcp_like/views/main.js] 2.67 KiB {master} [built]
    + 3749 hidden modules
ℹ ｢wdm｣: Compiled successfully.
ℹ ｢wdm｣: Compiling...
[hardsource:19a950bb] Using 326 MB of disk space.
94% after seal[hardsource:19a950bb] Could not freeze ./assets/stylesheets/zddi.scss: Cannot read property 'hash' of undefined
[hardsource:19a950bb] Could not freeze ./node_modules/@dengyongchao/modal/modal.scss: Cannot read property 'hash' of undefined
ℹ ｢wdm｣: Hash: d41d03944d509d378704
Version: webpack 4.44.2
Time: 5698ms
```
---
解决方案

v8 对内存限制约为 1.7 GB

可以手动设置限制大小， 我采用的方案

```bash
node --max-old-space-size=4096 a.js
```