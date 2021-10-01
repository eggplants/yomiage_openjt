# yomiage

- OpenJTalkくんの研究
- Debianのみで動作
  - よしなに書き換えれば他distroでも動くはず
  - `src/prepare_openjt.sh`のaptとかね

## はじめに

```bash
# open_jtalkコマンドのインストール
./prepare_openjt.sh
# 様々なボイスモデルをインストール(任意)
./down_akihito.sh
```

## 依存

```shellsession
$ grep -r "  chkcmd"|awk '{for(i=3;i<=NF;)print$(i++)}'|sort|uniq|xargs
aplay apt curl open_jtalk sox unar unzip wget
```

## お試し

```bash
# インストールしたボイスモデルを全部試す
./allvoice_test.sh
# yahooトップページニュース読み上げ
./read_yahoo.sh
# テキスト読み上げ
./read.sh - 白狐舞 <<< こんにちは
./read.sh - 唱地ヨエ <<< おはよう
# ファイル読み上げ
./read.sh beginner.txt 白狐舞
# 音声保存
./read.sh -s beginner.txt 白狐舞
```

## 正規化(正常に読んでもらうためのコツ)

- 改行コードをCR+LFをLFに置換(`\r`を削る)
- 改行をいったん全て削り、句点のあとに改行(`\n`)を挿入

```bash
cat hoge_file.txt | tr -d \\n\\r | sed -r 's/。/&\n/g'
```

## ソース

- UTF-8でないと動かん
- beginner.txt
  - <http://kurata.x.fc2.com/sizihyou-dansei-syokyu.html>

- mid.txt
  - <http://kurata.x.fc2.com/sizihyou-dansei-tyuukyu.html>
