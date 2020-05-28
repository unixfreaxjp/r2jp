## radare2 for servers support (r2jp community)

The UNIX server compatibility test result and support information for year 2020 (r2jp).

今まで互換性テスト結果を加え、2020年に対応すると対応しないUNIXサーバのバーションです。

2019年12月(SECCON-2019で)にpancakeさんと本内容について打ち合わせのでcommitすることとなります。
```
FreeBSD 9 :  unsupported, see: https://twitter.com/malwaremustd1e/status/1211930394628509697
FreeBSD 10 : unsupported , see: https://twitter.com/malwaremustd1e/status/1211930394628509697
FreeBSD 12 : core : ok , r2ghidra: NG, r2dec NG 
FreeBSD 11 : core : ok , r2ghidra: NG, r2dec NG 
Debian Wheezy: unsupported, see: https://twitter.com/malwaremustd1e/status/1215954152137740288
Debian Jessie: core : ok , r2ghidra: NG, r2dec OK 
Debian Stretch core : ok , r2ghidra: NG, r2dec OK 
Debian Buster: core: ok, r2ghidra: PENDING, r2dec PENDING 
```

**テストの結論/詳細内容↓**

- 上記のテスト用にサポートされているバージョンはすべてx64ビットCPU用で、 x32ビットCPUのサーバーは現在非コミットの状態です。
- r2ghidraはdebianのコンパイルに失敗し、 "isnan"、 "isinf" <  amiguousとのエラーの内容が出ています。
- CPPライブラリ互換性のBSDプラットフォームでr2 ghidraが失敗しました
- BSDテストスキーム全体で、r2decには「duktape」のビルドに関する問題が発生しています。
- FreeBSDx32は現在サポートされていません。報告しましたの内容(https：//twitter.com/malwaremustd1e/status/1211930394628509697)をご参照してください。
- Debian Stretch x32のテストはもうコミットされていませんが、最新の結果は下記のとおりです↓
  Debian Stretch x86 core : ok , r2ghidra: NG, r2dec OK
- OpenBSDは未だテスト中です。情報を改めて報告します。
- NetBSDの最新バージョンも後でお知らせします。

**最新の安定バージョン↓**
```
~/radare2-STABLE]$ r2 -v
radare2 4.2.0-git 23842 @ freebsd-x86-64 git.4.1.1-128-g3c788a496
commit: 3c788a49674d2e1c0e8ddbe6cce52ab4a9bcf818 build: 2020-01-16__14:06:39
```

**安定したOS組み込みバーション↓**

Tsurugi [SECCON 2019 Special Edition](https://blog.0day.jp/p/20191218.html)


**EOLの確認について下記のそれぞれUNIXディストリビューションのリンクをご確認ください↓**

- [FreeBSD supported versons](https://www.freebsd.org/releases/)
- [Linux Debian supported versions:](https://wiki.debian.org/LTS/Extended)
- [OpenBSD supported versions](https://marc.info/?l=openbsd-announce) | [or Web site](https://www.openbsd.org/)
- [NetBSD supported versions](https://www.netbsd.org/releases/formal.html)
- [Tsurugi Linux check versions](https://tsurugi-linux.org/documentation_tsurugi_linux_changelog.php#)

---
Thu Jan 16 14:30:32 JST 2020 @unxifreaxjp
