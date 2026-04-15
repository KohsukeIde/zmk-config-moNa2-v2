# zmk-config-moNa2

<img src="keymap-drawer/mona2_01.svg">

# ファームウェアのダウンロード / Firmware Download

ファームウェアは GitHub Actions によって自動的にビルドされます。以下の手順でダウンロードできます。

The firmware is automatically built by GitHub Actions. Follow these steps to download it:

1. このリポジトリの [**Actions**](../../actions) タブを開きます。  
   Open the [**Actions**](../../actions) tab of this repository.
2. 最新の成功した **build** ワークフローをクリックします。  
   Click the latest successful **build** workflow run.
3. ページ下部の **Artifacts** セクションから `firmware` をダウンロードします。  
   Download `firmware` from the **Artifacts** section at the bottom of the page.
4. ZIP を展開して `.uf2` ファイルをキーボードに書き込みます。  
   Extract the ZIP and flash the `.uf2` file to your keyboard.

# COROPITを使用するへ

COROPITを使用する方は以下のようにコードを編集してください。

mona2_r.overlay

修正前
```
  trackball_central: trackball_central@0 {
        status = "okay";
        compatible = "pixart,pmw3610";  //トラボセンサ用のドライバとバインド
        reg = <0>;
        spi-max-frequency = <2000000>;
        irq-gpios = <&gpio0 2 (GPIO_ACTIVE_LOW | GPIO_PULL_UP)>; //P0.02を指定(MOTION)
        cpi = <600>;
        //swap-xy;
        //invert-x; //COROPIT版ではコメントアウトを外す
        //invert-y; //COROPIT版ではコメントアウトを外す
        evt-type = <INPUT_EV_REL>;
        x-input-code = <INPUT_REL_X>;
        y-input-code = <INPUT_REL_Y>;
    };
};

```
**修正後**
```
  trackball_central: trackball_central@0 {
        status = "okay";
        compatible = "pixart,pmw3610";  //トラボセンサ用のドライバとバインド
        reg = <0>;
        spi-max-frequency = <2000000>;
        irq-gpios = <&gpio0 2 (GPIO_ACTIVE_LOW | GPIO_PULL_UP)>; //P0.02を指定(MOTION)
        cpi = <600>;
        //swap-xy;
        invert-x; //COROPIT版ではコメントアウトを外す
        invert-y; //COROPIT版ではコメントアウトを外す
        evt-type = <INPUT_EV_REL>;
        x-input-code = <INPUT_REL_X>;
        y-input-code = <INPUT_REL_Y>;
    };
};

```
