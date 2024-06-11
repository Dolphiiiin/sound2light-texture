# sound2light-texture
Sound2Light for cluster


# About
このプロジェクトはSound2Lightをグレースケールテクスチャをグレースケールの画像情報へリアルタイムに変換し、画面共有機能を通じて、cluster上のワールドにオーディオリアクティブ演出を実装するためのものです。

# 導入手順
## Unityプロジェクトのセットアップ
### 必須コンポーネントの導入
以下のコンポーネントが導入されていることを確認してください。
- Cluster CreatorKit
- Shader Graph
- Post Processing
### Unityパッケージのインポート
[releases](https://github.com/Dolphiiiin/sound2light-texture/releases)から、Unityパッケージをダウンロードして、インポートしてください。
## Sound2Light
[Sound2Light](https://github.com/ETCLabs/Sound2Light/releases)をダウンロードして、インストールしてください。
### Sound2Lightの設定
Sound2Lightを開き、画面左中央のSettingsを開き、以下に設定を変更します。
| 項目 | 設定値 |
| --- | --- |
| OSC IP Address | 127.0.0.1 |
| OSC Protcool | UDP |
| OSC UDP Tx Port | 3333 |
| OSC UDP Rx Port | 無視 |
| Console Type | 無視 |
| Input | ソースにする音源があ流れる音声デバイス |

> IPアドレス、ポートに関しては環境によって変更してください。
>
画面下のOSC Messageの列で、左からChannnelNumberを`Channnel 1` `Channel 2`の順に設定し、それぞれのModeを`Level`に設定してください。  
![image](https://github.com/Dolphiiiin/sound2light-texture/assets/42102311/63f33f00-df66-43b6-b7c6-7f853f20e557)

## sound2light-textureの準備
[releases](https://github.com/Dolphiiiin/sound2light-texture/releases)から、sound2light-texture.zipをダウンロードして解凍してください。  
`Sound2LightTexture.exe`を起動して、Sound2Lightに設定されたマイクに音声を流すことで、sound2light-textureはSound2Lightの送信するoscを受信し、画面に反映します。  
ソフトの終了には、Alt+F4を押します。  
![image](https://github.com/Dolphiiiin/sound2light-texture/assets/42102311/a8e55051-1109-4d5c-90b5-f6942e832845)
同梱の`config.json`で各種設定をします。(設定の変更後は、ソフトを再起動してください。)
```
{
  "scroll": 20, (スクロールの速度 ms)
  "port": 3333, (Sound2Lightのポート)
  "address": "127.0.0.1" (Sound2Lightのアドレス)
}
```

# サンプルファイルの使用方法
Unityの`Assets/Sound2LightTexture`にサンプルファイル群が入っています。  
まずは、`Assets/Sound2LightTexture/Sound2Light Texture Core.prefab`を、シーン上に配置してください。
> * ワールド上のあまり遠すぎないユーザーから見えない場所に配置してください
>
ワールドをアップロードして、cluster上で、`sound2light-texture`のウィンドウ単体でを画面共有することで、`Assets/Sound2LightTexture/Texture`に保存されているレンダーテクスチャから、sound2light-textureによる各帯域ののテクスチャを取得できます。

## サンプルシェーダーの使用方法
`Assets/Sound2LightTexture/Shaders/Sound2Light_SimpleExmission.shadergraph`にShader Graphで作成された、サンプルシェーダーが入っています。
このシェーダーを各帯域ごとにマテリアルとしてセットアップしたものは、`Assets/Sound2LightTexture/Materials`に入っています。
### パラメーター
| 項目 | 説明 |
| --- | --- |
| MainTex | 描画するベーステクスチャを指定します |
| Intensity Multiply | 光の強さ |
| Sector Tex | 取得したい帯域のレンダーテクスチャを指定 |
| Exposure | 光の強度 |
| Color | ベースカラー |
| Use Pre Frame | レンダーテクスチャの2列目以降の値を使用するか、一番上の最新の値のみを使用するか |

# 免責事項
このツールはクラスター社のかかわらない非公式のツールです。
このツールを使用したことによって生じた責任を作者は一切受けません。
予告なく動作が不可能になる可能性もあります。
