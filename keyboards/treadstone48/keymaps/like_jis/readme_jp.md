# JISキーボードライクなキーマップ

## 概要

　デフォルトキーマップの記号類をJISライクな配置に揃えなおしたものです。  

## キーマップの見かた

qmk_firmware\tmk_core\common\keycode.h  
に基本的なキーコードがあります。また、Keymap.cの上部にカスタムしたKC_で始まるものを登録しています。  
キーマップに書くときは「KC_」を省略して書いています。
例：KC_A → A  

Leyer Tap、Mod Tap、Tap DanceというQMKの機能を使っています。  

Layer Tapはタップで指定したキー、長押しで指定したレイヤーに移動します。  
例：LT(RAISE, KC_V) → タップでV、長押しでRAISEレイヤー移動

Mod Tapはタップで視程したキー、長押しで視程したレイヤーに移動します。  
例：LSFT_T(KC_Z) → タップでZ、長押しで左シフト

Tap Danceは指定した二つのキーをシングルタップ、ダブルタップで切り替えられます。  
例：[TD_CODO] = ACTION_TAP_DANCE_DOUBLE(KC_COMM, KC_DOT) → シングルタップでCOMM、ダブルタップでDOT

もう少し詳しい内容についてはQMK Documentをお読みいただくかネットを検索すれば情報が載っていますので別途検索してみてください。  

## 機能

　QWERTYキーマップをベースにしていて、LowerレイヤーとRaiseレイヤーに他のキーを配置しています。  
　LowerとRaiseを同時押しでAdjustレイヤーを使うことが出来ます。  
　DOTの横、SLROと書いてあるのはシングルタップで/記号、ダブルタップで\記号が入力出来るようになっています。
　Lの横、SCCLと書いてあるのはシングルタップで;記号、ダブルタップで:記号が入力出来るようになっています。
　マウスキーの割り当てがありますので、もし使用したい場合はrules.mkでMOUSEKEY_ENABLE = yesにしてmakeすると使用することができます。  

## 48キー目について

　このキーボードはEnterキーの上の2Uキーを1Ux2個にして使用する事が出来るようになっています。  使用する場合はキーマップの書き換えが必要です。  

　各レイヤーの最下段の

```c
      XXXXX \
  // ExtraKey: Split backspace key or it is below the enter key.
```

　のXXXXXに任意のキーを入れることでPの右隣のキーとして動作するようになっています。その右隣りに従来のキーが配置されています。  

## OS切り替え方法

　Adjustレイヤーにあります。LowerとRaiseを同時押しでAdjustレイヤーを使うことが出来ます。  

- KNRM: QMKのノーマル状態です。macだと正常に使える（はず）です
- KSWP: ノーマル状態のままWindowsで使用するとALTキーとGUI（win）キーが逆ですので、それを入れ換えます。Windowsユーザーはこちらのモードにしてください

## NUMPADモードについて

　Lower + DLNPキーを一度押下するとNumpadモードになります。通常モードに戻す場合はDLBSキーを押下してください。  

## IME切り替え方法

　Winの場合、LowerレイヤーにKANJIキー（半角/全角　漢字）がありますので、Lower+KANJIで切り替えてください。  

## ソフトウェアリセットについて

　キーボードにはハードウェアのリセットボタンが付いていますが、ソフトウェアリセットをかけられます。  
　LowerとRaiseを同時押しでAdjustレイヤーを使うことが出来、AdjustレイヤーのRSTを押下するとリセットがかかります。  

## LEDの点灯切り替え方法

　Adjustレイヤーにあります。LowerとRaiseを同時押しでAdjustレイヤーを使うことが出来ます。  

- LRST: LEDのリセット
- LTOG: LEDのON/OFF切り替え
- LMOD: LEDの光り方の変更
- LHUI: Hue+ 色合いを変更
- LHUD: Hue- 色合いを変更
- LSAI: Saturation+ 色の濃さを変更
- LSAD: Saturation- 色の濃さを変更
- LVAI: Value+ 明るさを変更
- LVAD: Value- 明るさを変更

```c

const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
  [_BASE] = LAYOUT_ALPHA_kc( \
  //,------------------------------------------------------------------------------------------.
        ESC,     Q,     W,     E,     R,     T,     Y,     U,     I,     O,     P,         MINS,\
  //|------+------+------+------+------+------|------+------+------+------+------+-------------|
       TBSF,     A,     S,     D,     F,     G,     H,     J,     K,     L,  SCCL,          ENT,\
  //|------+------+------+------+------+------|------+------+------+------+------+------+------|
       LSFT,     Z,     X,     C,     V,     B,     N,     M,  COMM,   DOT,  SLRO,    UP,       \
  //|------+------+------+------+------+------|------+------+------+------+------+------+------|
      LCTRL,  LALT,  LGUI, LOWER,         BSPC,          SPC, RAISE,  ALAP,  LEFT,  DOWN,  RGHT,\
  //`------------------------------------------------------------------------------------------'
      XXXXX \
  // ExtraKey: Split backspace key or it is below the enter key.
  ),

  [_LOWER] = LAYOUT_ALPHA_kc( \
  //,------------------------------------------------------------------------------------------.
      _____,    F1,    F2,    F3,    F4,    F5,  MINS,   EQL,  JYEN,  LBRC,  RBRC,          DEL,\
  //|------+------+------+------+------+------|------+------+------+------+------+-------------|
      _____,    F6,    F7,    F8,    F9,   F10, XXXXX, XXXXX,  SCLN,  QUOT,  BSLS,        _____,\
  //|------+------+------+------+------+------|------+------+------+------+------+------+------|
      _____,   F11,   F12, XXXXX, KANJI,   ENT, XXXXX,  COMM,   DOT,  SLSH,    RO,  PGUP,       \
  //|------+------+------+------+------+------|------+------+------+------+------+------+------|
      _____, _____, _____, _____,          DEL,        _____, _____, XXXXX,  HOME,  PGDN,   END,\
  //`------------------------------------------------------------------------------------------'
      XXXXX \
  // ExtraKey: Split backspace key or it is below the enter key.
  ),

  [_RAISE] = LAYOUT_ALPHA_kc( \
  //,------------------------------------------------------------------------------------------.
      _____,     1,     2,     3,     4,     5,     6,     7,     8,     9,     0,        XXXXX,\
  //|------+------+------+------+------+------|------+------+------+------+------+-------------|
      _____, XXXXX, XXXXX, XXXXX, XXXXX, XXXXX, XXXXX,     4,     5,     6,  QUOT,        _____,\
  //|------+------+------+------+------+------|------+------+------+------+------+------+------|
      _____, XXXXX, XXXXX, XXXXX, XXXXX, XXXXX, XXXXX,     1,     2,     3,    RO, XXXXX,       \
  //|------+------+------+------+------+------|------+------+------+------+------+------+------|
      _____, _____, _____, _____,        _____,        _____, _____,     0,   DOT,  COMM,  SLSH,\
  //`------------------------------------------------------------------------------------------'
      XXXXX \
  // ExtraKey: Split backspace key or it is below the enter key.
  ),

  [_ADJUST] = LAYOUT_ALPHA_kc( \
  //,------------------------------------------------------------------------------------------.
      XXXXX,   RST,  LRST,  KNRM,  KSWP, XXXXX, XXXXX,  WH_L,  WH_U,  HOME,  PGUP,        XXXXX,\
  //|------+------+------+------+------+------|------+------+------+------+------+-------------|
      XXXXX,  LTOG,  LHUI,  LSAI,  LVAI, XXXXX, XXXXX,  WH_R,  WH_D,   END,  PGDN,        XXXXX,\
  //|------+------+------+------+------+------|------+------+------+------+------+------+------|
      _____,  LMOD,  LHUD,  LSAD,  LVAD, XXXXX, XXXXX, XXXXX,  BTN1,  BTN2, XXXXX,  MS_U,       \
  //|------+------+------+------+------+------|------+------+------+------+------+------+------|
      _____, _____, _____, _____,        XXXXX,        XXXXX, _____, XXXXX,  MS_L,  MS_D,  MS_R,\
  //`------------------------------------------------------------------------------------------'
      XXXXX \
  // ExtraKey: Split backspace key or it is below the enter key.
  )
};

```
