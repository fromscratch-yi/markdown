<div class="mokuji">

  〜目次〜

- [iOSアプリの構造](#sec1)
  - [Cocoa Touchとは](#sec1-1)
  - [UIkitとは](#sec1-2)
  - [Delegateとは](#sec1-3)
  - [MVCとは](#sec1-4)
- [iOSアプリのライフサイクル](#sec2)
  - [iOSアプリの状態](#sec2-1)
- [iOSアプリの画面構成](#sec3)
- [まとめ](#sec4)
</div>

## <span class="h_link" id="sec1">iOSアプリの構造</span>
<div class="section_inner">
`Cocoa Touch`, `UIkit`などについて少し掘り下げて、iOSアプリの構造をみていきたいと思います。また、Cocoa TouchやUIKitで用いられる設計モデル( `MVCモデル`)や デザインパターン( `Delegate`)などについても、簡単に説明したいと思います。

  ### <span class="h_link" id="sec1-1">Cocoa Touchとは</span>
  <div class="section_inner">
    <p>Cocoa Touchは、iOS上で動くフレームワークで、Objective-CのFoundationフレームワークの上に、iOSの固有機能をまとめたUIKitというフレームワークを搭載しています。</p>
    <div class="memo">
      <p class="memo_ttl">Cocoaとは</p>
      <p class="memo_desc">macOS用のアプリケーションを構築するためのフレームワーク (API) で、Cocoa TouchはCocoaをタッチインターフェースを前提に作り直したもので、開発環境もほぼ同様のものを用いています。</p>
    </div>
  </div>

  ### <span class="h_link" id="sec1-2">UIKitとは</span>
  <div class="section_inner">
    <p>UIKitは、iOSアプリのユーザインターフェイスの構築と管理に必要なクラスを提供します。</p>
    <div class="memo">
      <p class="memo_ttl">AppKitとは</p>
      <p class="memo_desc">AppKitは、Mac OS XでCocoaアプリケーションのユーザインターフェイスを担うフレームワークで、iPhone OSのCocoa touchアプリケーションにおけるUIKitに相当します。</p>
    </div>
  </div>

  ### <span class="h_link" id="sec1-3">Delegateとは</span>

  <div class="section_inner">
    <p>Delegateはデザインパターンの1つです。<br>「委譲」という意味があり、あるオブジェクトの状態や設定を、そのオブジェクトが決めるのではなく、他のオブジェクトに決定してもらうような形で動作する、ということになります。<br>もう少し噛み砕いて説明すると、「あるクラスは、他のクラスのインスタンスに、処理を任せることができる。」というものです。</p>
    <p>＜処理を委譲する側＞</p>
    <pre class="hljs"><code><div>  <span class="hljs-comment">// 委譲する処理を定義</span>
  protcol <span class="hljs-type">SampleButtonDelegate</span>: <span class="hljs-class"><span class="hljs-keyword">class</span> </span>{
    <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">onTapped</span><span class="hljs-params">()</span></span>
  }
  <span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">SampleButton</span> </span>{
    <span class="hljs-comment">// 委譲先</span>
    week <span class="hljs-keyword">var</span> delegate: <span class="hljs-type">SampleButtonDelegate</span>? = <span class="hljs-literal">nil</span>
  <span class="hljs-comment">// OSから呼ばれるとする</span>
    <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">callTappedFromOS</span><span class="hljs-params">()</span></span> {
      <span class="hljs-comment">// 委譲先のonTapped()を呼び出す</span>
      <span class="hljs-keyword">self</span>.delegate?.onTapped()
    }
  }
  </div></code></pre>
  <p>＜処理を委譲される側＞</p>
  <pre class="hljs"><code><div>  <span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">Screen</span>: <span class="hljs-title">SampleButtonDelegate</span> </span>{
    <span class="hljs-keyword">let</span> sampleButton: <span class="hljs-type">SampleButton</span> = <span class="hljs-type">SampleButton</span>()
    <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">initialize</span><span class="hljs-params">()</span></span> {
      <span class="hljs-comment">// SampleButtonが委譲してくれる処理を本クラスが実行するために</span>
      <span class="hljs-comment">// 本クラスへの参照をSampleButtonに設定する。</span>
      <span class="hljs-keyword">self</span>.sampleButton.delegate = <span class="hljs-keyword">self</span>
    }
    <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">onTapped</span><span class="hljs-params">()</span></span> {
      <span class="hljs-built_in">print</span>(<span class="hljs-string">"SampleButton Tapped."</span>)
    }
  }
  </div></code></pre>
  <div class="memo">
      <p class="memo_ttl">Protcolとは</p>
      <p class="memo_desc">delegateとほぼ対になって言及されるswiftの機能に、「protcol」があります。<br>Javaでいうinterfaceのようなもので、簡単に言うとクラスの挙動を決めた設計図みたいなものになります。<br>クラス自体にも設計図という側面がありますが、クラスがその属性や挙動を細部に渡って記述するのに対して、プロトコルでは外部へのインターフェースのみを定義します。そして実際の挙動はそのプロトコルを採用するクラスで記述することになります。</p>
    </div>
  </div>

  ### <span class="h_link" id="sec1-4">MVCとは</span>
  <div class="section_inner">
    <p>Cocoa、およびUIKitの構造は、MVC(Model-View-Controller)に基づいています。<br>MVCとは、ソフトウェアの設計モデルの一つで、機能を「Model」（モデル）、「View」（ビュー）、「Controller」（コントローラ）の三つの役割に分離して実装し、それらが連携して処理を進めるという設計モデルです。</p>
    <p class="img_wrap"><img src="//images.ctfassets.net/eebw0y2sorkq/5R8NU1ogGa66MXkvs6cJL5/29cb0b957031cf151f6b7add3218310a/model_view_controller_2x.png" alt="MVC"></p>
    <dl>
      <dt>Model</dt>
      <dd>
        <ul>
          <li>アプリ固有のデータをカプセル化し、データの操作を行う。</li>
          <li>データベースの更新や通信処理などアプリのビジネスロジックを担当する。</li>
        </ul>
      </dd>
      <dt>View</dt>
      <dd>
        <ul>
          <li>実際に画面に表示されるもの(LabelやButtonなど)</li>
          <li>ユーザ操作(タップなど)を受け付け処理する。</li>
        </ul>
      </dd>
      <dt>Controller</dt>
      <dd>
        <ul>
          <li>Viewから通知されるイベントを受け取り、Modelの処理を実行する。</li>
          <li>Modelから通知される処理結果を受け取り、Viewを更新する。</li>
        </ul>
      </dd>
    </dl>
    <p class="img_wrap"><img src="//images.ctfassets.net/eebw0y2sorkq/48RNscnCjzqa5SnGkv8d9E/30c7d335e7d1b1ac6b81ab51fb60e305/uikit-mvc.png" alt="UIKit MVC"></p>
    <dl>
      <dt>UIApplication</dt>
      <dd>
        <ul>
          <li>イベントループやアプリの動作を管理する。</li>
          <li>アプリの状態移行やPush通知などをデリゲートに通知する。</li>
        </ul>
      </dd>
      <dt>Application Delegate</dt>
      <dd>
        <ul>
          <li>UIApplicationから通知されるアプリの状態移行やPush通知を処理する。</li>
          <li>アプリの初期化などを行う。</li>
        </ul>
      </dd>
      <dt>Documents / Data Objects</dt>
      <dd>
        <ul>
          <li>アプリごとに異なる処理を行う（ビジネスロジックを担当）。</li>
        </ul>
      </dd>
      <dt>ViewController</dt>
      <dd>
        <ul>
          <li>Viewの操作を行う。</li>
        </ul>
      </dd>
      <dt>UIWindow</dt>
      <dd>
        <ul>
          <li>画面上に1つ以上のViewを表示する。</li>
          <li>iOSアプリの画面はUIWindow上に表示される。</li>
          <li>基本的に1アプリに1つしかない。</li>
        </ul>
      </dd>
      <dt>View and UI Objects</dt>
      <dd>
        <ul>
          <li>LabelやButtonなどのView</li>
        </ul>
      </dd>
    </dl>
    <div class="memo">
      <p class="memo_ttl">レガシーなMVC</p>
      <p class="memo_desc">iOSにおけるMVCとレガシーなMVCにつきましては、多少考え方が違うようです。<br>詳しくはまとめの「iOSのMVCと、レガシーなMVC」をご覧ください。</p>
    </div>
  </div>
</div>

## <span class="h_link" id="sec2">iOSアプリのライフサイクル</span>
<div class="section_inner">
  <p class="img_wrap"><img src="//images.ctfassets.net/eebw0y2sorkq/1GL6aBy1ImF0BoKwNjxuHL/befb4d1c810545d74676c5775d478e70/ios_event.png" alt="iOSイベントフロー"></p>
  <p>iOSアプリはMain Run Loopという実行ループがアプリ内のメインスレッドで実行されることで様々なイベントを処理します。</p>

  - タッチイベント
  - リモートコントロールイベント
  - モーションイベント
  - 加速度イベント

  <p>iOS内で発生する様々なイベントはUIKitによって設定されたポートを介してアプリに通知され、通知されたアプリ内のキューに格納され、実行ループに1つずつディスパッチされます。</p>

  ### <span class="h_link" id="sec2-1">iOSアプリの状態</span>
  <div class="section_inner">
    <p class="img_wrap"><img src="//images.ctfassets.net/eebw0y2sorkq/5S0L9QTd4YC9FRcShpH2Qz/4e23dc2bc9528db3f15571e168dbb40f/ios_status.png" alt="iOSアプリの状態"></p>
    <p>iOSアプリには上記の状態があり、いかなる時点でもどれかの状態に当てはまります。</p>
    <dl>
      <dt>NotRunnnig</dt>
      <dd>
        <ul>
          <li>アプリが起動していない状態</li>
          <li>システムからアプリが終了された状態</li>
        </ul>
      </dd>
      <dt>InActive</dt>
      <dd>
        <ul>
          <li>アプリはフォアグラウンドで実行中だが、イベントを受信していない状態</li>
          <li>アプリが別の状態に移行する際に、一時的にこの状態になる</li>
        </ul>
      </dd>
      <dt>Active</dt>
      <dd>
        <ul>
          <li>アプリがフォアグラウンドで実行中で、イベントを受信できる状態</li>
        </ul>
      </dd>
      <dt>Background</dt>
      <dd>
        <ul>
          <li>アプリがバックグラウンドで実行中の状態</li>
        </ul>
      </dd>
      <dt>Suspended</dt>
      <dd>
        <ul>
          <li>アプリがバックグラウンドで実行中でない状態</li>
          <li>システムから自動的にこの状態にアプリの状態を移行する</li>
          <li>アプリは実行されていないが、メモリは保持された状態となる</li>
        </ul>
      </dd>
    </dl>
  </div>
</div>

## <span class="h_link" id="sec3">iOSアプリの画面構成</span>
<div class="section_inner">
  <p>iOSアプリの画面は以下の3つで構成される。</p>
  <dl>
    <dt>UIWindow</dt>
    <dd>基本的にアプリに1つしか存在せず、アプリの画面を構成するViewControllerはUIWindow上に表示する。</dd>
    <dt>UIViewController</dt>
    <dd>基本的にアプリの画面を指す。</dd>
    <dt>UIView</dt>
    <dd>アプリの画面に表示される各パーツ(LabelやButton)のこと</dd>
  </dl>
</div>

## <span class="h_link" id="sec4">まとめ</span>
<div class="section_inner">

<p>今回は、iOSアプリの構造について、少し詳しく説明していきました。<br>delegateなどは、実際に使ってみてイメージしやすいこともあるので、今時点ではそういうものがあるのかぁくらいのスタンスで大丈夫です。<br>今回も参考文献を載せていますのでぜひ！</p>

- <a class="refer" href="https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html" target="_blank" rel="noopener">Cococa MVC</a>
- <a class="refer" href="https://developer.apple.com/documentation/uikit/about_app_development_with_uikit" target="_blank" rel="noopener">UIKit</a>
- <a class="refer" href="https://sites.google.com/a/gclue.jp/swift-docs/" target="_blank" rel="noopener">Swift docs</a>
- <a class="refer" href="http://d.hatena.ne.jp/sankumee/20090402/1238643076" target="_blank" rel="noopener">iOSのMVCと、レガシーなMVC</a>
- <a class="refer" href="https://dev.classmethod.jp/smartphone/iphone/ios-delegate/" target="_blank" rel="noopener">iOSのdelegate</a>
</div>