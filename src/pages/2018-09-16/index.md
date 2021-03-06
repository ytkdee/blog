---
title: 【OpenGL】OpenGL APIのエラーハンドリングについて
date: "2018-09-16"
---

![Bear](./bear.jpg)  

---

## OpenGL APIのエラーハンドリングについて

ほとんどのOpenGLの関数では戻り値がvoidであり、成功/失敗の判定が出来ない。  
例え失敗していたとしても、 *あたかもAPIが呼び出されていないかの様な挙動* となる。  
エラーチェックは、以下のAPIを使う事により確認が可能である。  

```c
GLenum glGetError();
```

OpenGLエラーは、上記API呼び出しによりエラーが実際に処理されるまでキューに格納される。  
つまり、定期的に上記APIを使って確認してないと、  
どのAPI呼び出し時にどの様なエラーを引き起こしたのかを知るすべがない。  

エラーキューが空の場合、```GL_NO_ERROR```を返す。  
それ以外の場合は、エラー列挙子が返され、そのエラーがキューから削除される。

エラーチェック処理をしていないをしていない箇所があることも想定し、
各OpenGL API をコールした前 or 後に現在キューにある全てのエラーを破棄 or 取得する様にするのが良い。  

以下の様な処理となる。

```c
GLenum err;
while ((err = glGetError()) != GL_NO_ERROR ) {
  // エラーを処理/ロギングします。
}
```

```glGetError()```によって返却されるエラーコードとそれが指す状態については以下を参照してください。

|エラーコード |値 |説明 |
|---|---|---|
|GL_NO_ERROR |0 |エラーキューが空の場合 |
|GL_INVALID_ENUM |0x0500 |呼んだ関数の列挙型の引数がその関数で使えない場合 |
|GL_INVALID_VALUE |0x0501 |呼んだ関数の引数の値が無効な値もしくは範囲外の場合 |
|GL_INVALID_OPERATION |0x0502 |現在のステートで無効な操作をしている場合、もしくは廃止された関数を呼び出した場合(*1) |
|GL_STACK_OVERFLOW |0x0503 |スタックのプッシュ操作がスタックのサイズの上限を超える場合 |
|GL_STACK_UNDERFLOW |0x0504 |スタックがすでに最下点にあるため、スタックのポッピング操作を実行できない場合 |
|GL_OUT_OF_MEMORY |0x0505 |実行するのにメモリが足りない場合(このエラーを返した場合そのOpenGL関数の動作は未定義) |
|GL_INVALID_FRAMEBUFFER_OPERATION |0x0506 |完了していないフレームバッファから読み込みまたは書き込みをしようとした場合 |
|GL_CONTEXT_LOST |0x0507 |グラフィックカードがリセットされたためにOpenGLのコンテキストが失われた場合 |

 (*1) 例えば、廃止されたAPIを呼び出した場合。

しかし、上記の通り各OpenGL API のコール前後に現在キューにある全てのエラーを処理するとパフォーマンスが大幅に低下する。  
その理由は以下の二点。

* エラー状態をチェックして返すだけでなく、OpenGL API コール自体のオーバーヘッドも発生する。
* マルチスレッドを使用するドライバの場合、glGetError()をコールする事によりドライバ内のスレッド間で同期が発生する。

その為、glGetError()のコール自体をデバッグビルドに限定した方が良いかと思われる。

参考：  
[glGetError - OpenGL 4 Reference Pages](https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/glGetError.xhtml)  
[Common Mistakes - OpenGL Wiki](https://www.khronos.org/opengl/wiki/Common_Mistakes#Checking_for_OpenGL_Errors)
