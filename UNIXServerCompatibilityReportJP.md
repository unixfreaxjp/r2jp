## radare2 for servers support (r2jp community)

今まで互換性テスト結果を加え、2020年に対応すると対応しないUNIXサーババーションの報告です。

2019年12月(SECCON-2019で)にpancakeさんと本内容について打ち合わせを行い、以下の内容をcommitすることになります。

**今現在対応しているバーションと対応していないバーションのテスト結果**
```
FreeBSD 9 :  unsupported, see: https://twitter.com/malwaremustd1e/status/1211930394628509697
FreeBSD 10 : unsupported , see: https://twitter.com/malwaremustd1e/status/1211930394628509697
FreeBSD 11 : core : ok , r2ghidra: NG, r2dec NG 
FreeBSD 12 : core : ok , r2ghidra: NG, r2dec NG 
Debian Wheezy: unsupported, see: https://twitter.com/malwaremustd1e/status/1215954152137740288
Debian Jessie: core : ok , r2ghidra: NG, r2dec OK 
Debian Stretch core : ok , r2ghidra: NG, r2dec OK 
Debian Buster: core: ok, r2ghidra: PENDING, r2dec PENDING 
NetBSD と OpenBSD (TBA)
```

**テストの結論/詳細内容↓ (v4.3.0 ～ v4.4.0 base/core)**

- 上記のテスト用にサポートされているバージョンはすべてx64ビットCPU用で、 x32ビットCPUのサーバーは現在非コミットの状態です。
- r2ghidraはdebianのコンパイルに失敗し、 "isnan"、 "isinf" <  ambiguousエラーが出ています。
- CPPライブラリ互換性のBSDプラットフォームでr2 ghidraが失敗しました
- BSDテストスキーム全体で、r2decには「duktape」のビルドに関する問題が発生しています。
- FreeBSDx32は現在サポートされていません。報告しましたの内容(https：//twitter.com/malwaremustd1e/status/1211930394628509697)をご参照してください。
- Debian Stretch x32のテストはもうコミットされていませんが、最新の結果は下記のとおりです↓
  Debian Stretch x86 core : ok , r2ghidra: NG, r2dec OK
- OpenBSDは未だテスト中です。情報を改めて報告します。
- NetBSDの最新バージョンも後でお知らせします。

**最新の安定しているバージョンの情報について**

(1)下記のバーション以降はx64ビットの対応となりますが、x32サーバ版の対応が不可能です。
```
~/radare2-STABLE]$ r2 -v
radare2 4.2.0-git 23842 @ freebsd-x86-64 git.4.1.1-128-g3c788a496
commit: 3c788a49674d2e1c0e8ddbe6cce52ab4a9bcf818 build: 2020-01-16__14:06:39
```
上記のバーションのpdc、r2decとr2ghidraは「現在対応しているバーション」のセクションに書いたとおり、本STABLEバーションの[パッケージはこちらになります](https://github.com/radareorg/radare2/releases/tag/4.2.0)

(2) サーバ版特にFreeBSD/OpenBSDのx32ビットについて、下記のradare2のバーションをインストールしてください。
```
radare2 4.0.0-git 23215 @ linux-x86-32 git.3.9.0-20-gd112883
commit: d112883c5ad7309ca577373639281bb8e57d9988 build: 2019-09-20__21:47:04

radare2 4.0.0-git 23226 @ freebsd-x86-32 git.3.9.0-20-gd112883
commit: d112883c5ad7309ca577373639281bb8e57d9988 build: 2019-09-20__21:55:04

radare2 4.0.0-git 23449 @ linux-x86-64 git.3.9.0-20-gd112883
commit: d112883c5ad7309ca577373639281bb8e57d9988 build: 2019-09-20__21:38:58

radare2 4.0.0-git 22926 @ freebsd-x86-64 git.3.9.0-20-gd112883c5
commit: d112883c5ad7309ca577373639281bb8e57d9988 build: 2019-09-20__12:53:49
```
↑本バーションにはpdcとr2dec迄のプラグインにしか対応をしておりません。本バーションの[パッケージはこちらになります](https://github.com/radareorg/radare2/releases/tag/4.0.0)

**安定したOS組み込みバーション↓**

- Tsurugi [SECCON 2019 Special Edition](https://blog.0day.jp/p/20191218.html)
```
radare2 4.1.0-git 24455 @ linux-x86-64 git.4.0.0-235-g982be50
commit: 982be504999364c966d339c4c29f20da80128e14 build: 2019-12-17__10:29:05
```
- (core : OK , r2ghidra: OK, r2dec OK, 実績: SECCON2019、HACKLU2019、MMD-0065-2020とMMD-0066-2020の解析)

**今までのradare2のバーションとr2jpでのテストステータスについて**

- [r2リリース一覧](https://github.com/radareorg/radare2/releases) | [テスト最中/ 現在 ⇒ radare2_4.5.0-git](https://github.com/radareorg/radare2/releases/tag/continuous)
- 4.4.0 (性能試験の結果が良くない(重い)、4.5.0のリリースでバグフィックス)
- 4.3.0 (ビルドのバグがあり、4.5.0のリリースでバグフィックス)


**EOLの確認について下記のそれぞれUNIXディストリビューションのリンクをご確認ください↓**

- [FreeBSD supported versons](https://www.freebsd.org/releases/)
- [Linux Debian supported versions:](https://wiki.debian.org/LTS/Extended)
- [OpenBSD supported versions](https://marc.info/?l=openbsd-announce) | [or Web site](https://www.openbsd.org/)
- [NetBSD supported versions](https://www.netbsd.org/releases/formal.html)
- [Tsurugi Linux check versions](https://tsurugi-linux.org/documentation_tsurugi_linux_changelog.php#)

＊）上記の内容を定期的に更新を行いますので変更される可能性もあります。

---
unixfreaxjp@tsurugiseccon:~$ date
Sat May 30 06:04:32 JST 2020
