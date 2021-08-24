

# Android开发之Dialog

## 一、Dialog源码分析

### 1.1 主要属性：

```java
	//宿主Activity
	private Activity mOwnerActivity;

	//window管理者
    private final WindowManager mWindowManager;

	//上下文环境
    final Context mContext;

	//window
    final Window mWindow;

	//顶级视图
    View mDecor;

	//操作栏
    private ActionBar mActionBar;

    protected boolean mCancelable = true;

    private String mCancelAndDismissTaken;

    private Message mCancelMessage;
    private Message mDismissMessage;
    private Message mShowMessage;

    private OnKeyListener mOnKeyListener;

    private boolean mCreated = false;
    private boolean mShowing = false;
    private boolean mCanceled = false;

    private final Handler mHandler = new Handler();

    private static final int DISMISS = 0x43;
    private static final int CANCEL = 0x44;
    private static final int SHOW = 0x45;

    private final Handler mListenersHandler;

    private SearchEvent mSearchEvent;

    private ActionMode mActionMode;

    private int mActionModeTypeStarting = ActionMode.TYPE_PRIMARY;

    private final Runnable mDismissAction = this::dismissDialog;
```



View	Decor

Decor默认会有40px的内边距

## 二、dialog弹窗动画

### 1.从底部向上弹出

进入动画

```xml
<?xml version="1.0" encoding="utf-8"?>
<translate xmlns:android="http://schemas.android.com/apk/res/android"
    android:duration="150"
    android:fromXDelta="0"
    android:fromYDelta="100%"
    android:toXDelta="0"
    android:toYDelta="0">
</translate>
```

退出动画

```xml
<?xml version="1.0" encoding="utf-8"?>
<translate xmlns:android="http://schemas.android.com/apk/res/android"
    android:duration="150"
    android:fromXDelta="0"
    android:fromYDelta="0"
    android:toXDelta="0"
    android:toYDelta="100%">
</translate>
```

2.放大缩小动画

进入动画

```xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
 
    <scale
        android:duration = "300"
        android:fromXScale="1.2"
        android:toXScale="1.0"
        android:fromYScale="1.2"
        android:toYScale="1.0"
        android:pivotX="50%"
        android:pivotY="50%"/>
 
    <alpha
        android:duration="300"
        android:fromAlpha="0.0"
        android:toAlpha="1.0" />
</set>
```

退出动画

```xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
 
    <scale
        android:duration="300"
        android:fromXScale="1.0"
        android:fromYScale="1.0"
        android:pivotX="50%"
        android:pivotY="50%"
        android:toXScale="1.2"
        android:toYScale="1.2" />
 
    <alpha
        android:duration="300"
        android:fromAlpha="1.0"
        android:toAlpha="0.0" />
 
 
</set>
```

