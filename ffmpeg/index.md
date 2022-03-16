# FFMpeg雑記

## インストール
* 公式サイトから
  * https://www.ffmpeg.org/download.html
* chocolatey
  * `choco install ffmpeg`

## 動画の情報を取得する
ffprobe

## 動画を変換する

|| 属性 || オプション || コマンド例 ||
|| 画面サイズ || -vf scale 設定値 || ffmpeg -i in.mp4 -vf scale=1920:1080 out.mp4 ||
|| フレームレート || -r  設定値 || ffmpeg -i in.mp4 -r 30 out.mp4 ||
|| 動画ビットレート || -b:v 設定値 || ffmpeg -i in.mp4 -b:v 5000k out.mp4 ||
|| 音声ビットレート || -b:a 設定値 || ffmpeg -i in.mp4 -b:a  256k out.mp4 ||

## 動画オプション
https://ffmpeg.org/ffmpeg.html#Video-Options

## 音声オプション
https://ffmpeg.org/ffmpeg.html#Audio-Options

